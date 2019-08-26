# Create an ECS instance {#task_x2l_yxg_2fb .task}

This article describes how to create an ECS instance by using Terraform.

1.  Create a VPC and a switch. 
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
          nic_type          = "intranet"
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

3.  Creates an ECS instance. 
    1.  In the file terraform.tf, add the following:

        ```
        resource "alicloud_instance" "instance" {
          # cn-beijing
          availability_zone = "cn-beijing-b"
          security_groups = ["${alicloud_security_group.default. *.id}"]
        
          # series III
          instance_type        = "ecs.n2.small"
          system_disk_category = "cloud_efficiency"
          image_id             = "ubuntu_140405_64_40G_cloudinit_20161115.vhd"
          instance_name        = "test_foo"
          vswitch_id = "${alicloud_vswitch.vsw.id}"
          internet_max_bandwidth_out = 10
          password = "<replace_with_your_password>"
        }
        ```

        **Note:** 

        -   In the above example, `internet_max_bandwidth_out = 10` is specified. Therefore, the instance is assigned a public IP automatically.
        -   For a detailed explanation of the parameters, see the [Alibaba Cloud parameter descriptions](https://www.terraform.io/docs/providers/alicloud/r/instance.html).
    2.  Run `terraform apply` to start the creation.
    3.  Run `terraform show` to view the ECS instance that has been created.
    4.  Run ssh root@<publicip\> and enter the password to access the ECS instance.

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


resource "alicloud_instance" "instance" {
  # cn-beijing
  availability_zone = "cn-beijing-b"
  security_groups = ["${alicloud_security_group.default. *.id}"]

  # series III
  instance_type        = "ecs.n2.small"
  system_disk_category = "cloud_efficiency"
  image_id             = "ubuntu_140405_64_40G_cloudinit_20161115.vhd"
  instance_name        = "test_foo"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  internet_max_bandwidth_out = 10
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
```

