# Deploy a Web cluster {#task_hkk_3dh_2fb .task}

When you deploy a website or application, you need to deploy a series of nodes, and allow them to scale up or down automatically according to the number of visits or resource usage. SLB distributes requests to respective nodes. This article describes how to deploy a Web cluster by using Terraform.

In this example, the entire application is deployed in one zone, and the "Hello, World" web page can be accessed only through port 8080.

1.  Create a VPC and a VSwitch. 
    1.  Create the terraform.tf file, enter the following, and save it to the current execution directory.

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

    2.  Run `terraform apply` to start the creation.

    3.  Run `terraform show` to view the VPC and VSwitch that have been created.

        You can also log on to the VPC console to view the attributes of the VPC and VSwitch.

2.  Create a security group and apply it to the VPC created in the previous step. 
    1.  In the file terraform.tf, add the following:

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

    2.  Run `terraform apply` to start the creation.

    3.  Run `terraform show` to view the security group and security group rules that have been created.

        You can also log on to the ECS console to view the security group and security group rules.

3.  Create a Server Load Balancer \(SLB\) instance and assign a public IP address to it. In this example, the SLB instance is configured with a mapping from front end port 80 to back end port 8080. In addition, it is configured to output the public IP address for subsequent testing. 
    1.  Create the file slb.tf and add the following.

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

    2.  Run `terraform apply` to start the creation.

    3.  Run `terraform show` to view the SLB instance that has been created.

        You can also log on to the SLB console to view the new SLB instance.

4.  Creates an Auto Scaling solution. 

    In this example, the following resources are created:

    -   Scaling group: specifies the minimum number of ECS instances as 2 in the template, and the maximum number as 10. Meanwhile, bind the scaling group to the newly created SLB instance. Due to the configuration requirements of the scaling group, SLB must have a listener configured accordingly. As a result, the order of deployment is specified with the depends\_on attribute in the template.
    -   Scaling group configuration: specifies the specific configuration of the ECS instance in the template. Generate a "hello World" web page in the initialization configuration \(user-data\), and provide services on port 8080. To simplify operations, in this example, the virtual machine is assigned a public IP address, and `force_delete=true` is set for subsequent deletion of the environment.
    -   Scaling rules: define specific scaling rules.
    1.  Create the file ess.tf and add the following to it:

```
resource "alicloud_ess_scaling_group" "scaling" {
  min_size = 2
  max_size = 10
  scaling_group_name = "tf-scaling"
  vswitch_ids=["${alicloud_vswitch.vsw. *.id}"]
  loadbalancer_ids = ["${alicloud_slb.slb. *.id}"]
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
  user_data = "#! /bin/bash\necho \"Hello, World\" > index.html\nnohup busybox httpd -f -p 8080&"
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

    2.  Run `terraform apply` to start the creation.

        After it is created successfully, the public IP address of the SLB is generated.

    3.  In about two minutes, Auto Scaling will automatically create the ECS instance.

    4.  Enter the command `curl http://<slb public ip>` for verification.

        If you see `Hello, World`, you have successfully accessed the web page provided by the ECS instance through an SLB instance.

5.  Run `terraform destroy` to delete the test environment. Once confirmed, the entire deployed environment will be deleted. 

    Terraform makes it easy to remove and redeploy an environment. If you want to redeploy, just run `terraform apply`.


