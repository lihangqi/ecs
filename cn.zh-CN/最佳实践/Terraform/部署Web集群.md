# 部署Web集群 {#task_hkk_3dh_2fb .task}

部署一个网站或者API应用时，需要部署一系列的节点，并根据访问数量或者资源使用的情况来自动伸缩，SLB对各个节点分配请求。本文介绍如何使用Terraform部署Web集群。

在本示例中，整个应用部署在一个可用区，并且只提供8080端口访问hello world网页。

1.  创建VPC网络和交换机。 
    1.  创建terraform.tf文件，输入以下内容，并保存在当前的执行目录中。

        ```
        resource "alicloud_vpc" "vpc" {
          name       = "tf_test_foo"
          cidr_block = "172.16.0.0/12"
        }
        
        resource "alicloud_vswitch" "vsw" {
          vpc_id            = "${alicloud_vpc.vpc.id}"
          cidr_block        = "172.16.0.0/21"
          availability_zone = "cn-beijing-b"
        }
        ```

    2.  运行`terraform apply`开始创建。

    3.  运行`terraform show`查看已创建的VPC和VSwitch。

        您也可以登录VPC控制台查看VPC和VSwitch的属性。

2.  创建安全组，并将安全组作用于上一步创建的VPC中。 
    1.  在terraform.tf文件中增加以下内容。

```
resource "alicloud_security_group" "default" {
  name = "default"
  vpc_id = "${alicloud_vpc.vpc.id}"
}

resource "alicloud_security_group_rule" "allow_all_tcp" {
  type              = "ingress"
  ip_protocol       = "tcp"
  nic_type          = "internet"
  policy            = "accept"
  port_range        = "1/65535"
  priority          = 1
  security_group_id = "${alicloud_security_group.default.id}"
  cidr_ip           = "0.0.0.0/0"
}
```

    2.  运行`terraform apply`开始创建。

    3.  运行`terraform show`查看已创建的安全组和安全组规则。

        你也可以登录ECS控制台查看安全组和安全组规则。

3.  创建负载均衡实例，为其分配公网IP。在本示例中，为负载均衡实例配置了从前端80端口到后端8080端口的映射，并输出公网IP用于后续测试。 
    1.  创建slb.tf文件，并增加以下内容。

```
resource "alicloud_slb" "slb" {
  name       = "test-slb-tf"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  internet = true
}
resource "alicloud_slb_listener" "http" {
  load_balancer_id = "${alicloud_slb.slb.id}"
  backend_port = 8080
  frontend_port = 80
  bandwidth = 10
  protocol = "http"
  sticky_session = "on"
  sticky_session_type = "insert"
  cookie = "testslblistenercookie"
  cookie_timeout = 86400
  health_check="on"
  health_check_type = "http"
  health_check_connect_port = 8080
}

output "slb_public_ip"{
  value = "${alicloud_slb.slb.address}"
}
```

    2.  运行`terraform apply`开始创建。

    3.  运行`terraform show`查看已创建的负载均衡实例。

        你也可以登录SLB控制台查看新建的负载均衡实例。

4.  创建弹性伸缩。 

    在本示例中，将创建以下资源：

    -   伸缩组：在模版中指定伸缩最小为2，最大为10，并将伸缩组与新建的负载均衡实例绑定。由于伸缩组的配置要求SLB必须有相应配置的监听器，因此模版中用depends\_on属性指定了部署顺序。
    -   伸缩组配置：在模版中指定ECS实例的具体配置。在初始化配置（user-data）中生成一个Hello World的网页，并在8080端口提供服务。为简化操作，本示例中会为虚拟机分配公网IP，并且设置`force_delete=true`用于后续删除环境。
    -   伸缩规则：定义具体的伸缩规则。
    1.  创建ess.tf文件，并增加以下内容。

```
resource "alicloud_ess_scaling_group" "scaling" {
  min_size = 2
  max_size = 10
  scaling_group_name = "tf-scaling"
  vswitch_ids=["${alicloud_vswitch.vsw.*.id}"]
  loadbalancer_ids = ["${alicloud_slb.slb.*.id}"]
  removal_policies   = ["OldestInstance", "NewestInstance"]
  depends_on = ["alicloud_slb_listener.http"]
}

resource "alicloud_ess_scaling_configuration" "config" {
  scaling_group_id = "${alicloud_ess_scaling_group.scaling.id}"
  image_id = "ubuntu_140405_64_40G_cloudinit_20161115.vhd"
  instance_type = "ecs.n2.small"
  security_group_id = "${alicloud_security_group.default.id}"
  active=true
  enable=true
  user_data = "#!/bin/bash\necho \"Hello, World\" > index.html\nnohup busybox httpd -f -p 8080&"
  internet_max_bandwidth_in=10
  internet_max_bandwidth_out= 10
  internet_charge_type = "PayByTraffic"
  force_delete= true

}

resource "alicloud_ess_scaling_rule" "rule" {
  scaling_group_id = "${alicloud_ess_scaling_group.scaling.id}"
  adjustment_type  = "TotalCapacity"
  adjustment_value = 2
  cooldown = 60
}
```

    2.  运行`terraform apply`开始创建。

        创建成功后，会输出SLB的公网IP。

    3.  等待大约两分钟，弹性伸缩将自动创建ECS实例。

    4.  输入命令`curl http://<slb public ip>`进行验证。

        如果看到`Hello，World`，表示成功通过负载均衡实例访问ECS实例提供的网页。

5.  运行`terraform destroy`删除测试环境。经确认后，整个部署的环境将被删除。 

    使用Terraform可以便捷地删除和重新部署一个环境。如果您想重新部署，运行`terraform apply`即可。


