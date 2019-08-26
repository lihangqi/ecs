# 创建多台ECS实例 {#task_bl2_bch_2fb .task}

本文介绍如何使用Terraform模块批量创建多台ECS实例。

1.  创建VPC网络和交换机。 
    1.  创建terraform.tf文件，输入以下内容，保存在当前的执行目录中。

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

3.  使用Module创建多台ECS实例。在本示例中，创建3台ECS实例。 
    1.  在terraform.tf文件中增加以下内容。

```
module "tf-instances" {
  source = "alibaba/ecs-instance/alicloud"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  group_ids = ["${alicloud_security_group.default.*.id}"]
  availability_zone = "cn-beijing-b"
  disk_category = "cloud_ssd"
  disk_name = "my_module_disk"
  disk_size = "50"
  number_of_disks = 7

  instance_name = "my_module_instances_"
  host_name = "sample"
  internet_charge_type = "PayByTraffic"
  number_of_instances = "3"
  password="User@123"
}
```

        **说明：** 

        -   在上述示例中，指定了`internet_max_bandwith_out = 10`，因此会自动为实例分配一个公网IP。
        -   详细的参数解释请参见 [参数说明](https://registry.terraform.io/modules/alibaba/ecs-instance/alicloud/1.2.2?tab=inputs)。
    2.  运行`terraform apply`开始创建。

    3.  运行`terraform show`查看已创建的ECS实例。

    4.  运行ssh root@<publicip\>，并输入密码来访问ECS实例。


```
provider "alicloud" {}

resource "alicloud_vpc" "vpc" {
  name       = "tf_test_foo"
  cidr_block = "172.16.0.0/12"
}

resource "alicloud_vswitch" "vsw" {
  vpc_id            = "${alicloud_vpc.vpc.id}"
  cidr_block        = "172.16.0.0/21"
  availability_zone = "cn-beijing-b"
}

resource "alicloud_security_group" "default" {
  name = "default"
  vpc_id = "${alicloud_vpc.vpc.id}"
}


resource "alicloud_security_group_rule" "allow_all_tcp" {
  type              = "ingress"
  ip_protocol       = "tcp"
  nic_type          = "intranet"
  policy            = "accept"
  port_range        = "1/65535"
  priority          = 1
  security_group_id = "${alicloud_security_group.default.id}"
  cidr_ip           = "0.0.0.0/0"
}

module "tf-instances" {
  source = "alibaba/ecs-instance/alicloud"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  group_ids = ["${alicloud_security_group.default.*.id}"]
  availability_zone = "cn-beijing-b"
  disk_category = "cloud_ssd"
  disk_name = "my_module_disk"
  disk_size = "50"
  number_of_disks = 7

  instance_name = "my_module_instances_"
  host_name = "sample"
  internet_charge_type = "PayByTraffic"
  number_of_instances = "3"
  password="User@123"
}
```

