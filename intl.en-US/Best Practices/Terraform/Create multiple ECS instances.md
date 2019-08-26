# Create multiple ECS instances {#task_bl2_bch_2fb .task}

This article describes how to create multiple ECS instances in batches by using Terraform.

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

3.  Use the Module to create multiple ECS instances. In this example, three ECS instances are created. 
    1.  In the file terraform.tf, add the following:

```
module "tf-instances" {
  source = "alibaba/ecs-instance/alicloud"
  vswitch_id = "${alicloud_vswitch.vsw.id}"
  group_ids = ["${alicloud_security_group.default. *.id}"]
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

        **Note:** 

        -   In the above example, `internet_max_bandwith_out = 10` is specified. Therefore, the instances are assigned public IP addresses automatically.
        -   For a detailed explanation of the parameters, see the [Parameter descriptions](https://registry.terraform.io/modules/alibaba/ecs-instance/alicloud/1.2.2?tab=inputs).
    2.  Run `terraform apply` to start the creation.

    3.  Run `terraform show` to view the ECS instances that have been created.

    4.  Run ssh root@<publicip\> and enter the password to access the ECS instances.


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
  group_ids = ["${alicloud_security_group.default. *.id}"]
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

