# Quick reference {#concept_q3w_45w_wdb .concept}

This article is a quick reference guide for common features of Alibaba Cloud ECS instances and resources. It offers solutions for such scenarios as connecting to an instance, resizing a disk, upgrading or downgrading configurations, and using snapshots or images.

## Operation instructions and limits {#instructions .section}

To guarantee proper operation of your ECS instance, please read the [ECS operation instructions](reseller.en-US/User Guide/Instructions on using ECS.md#) and [limits](reseller.en-US/User Guide/Limits.md#) sections carefully before using your instance.

## Create and manage ECS instances {#section_fpl_wyw_wdb .section}

**Basic operations**

1.  [Create an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).
2.  Connect to the ECS instance. Depending on the operating system running on your ECS instance and your actual scenario, use one of the following methods:
    -   For any type of operating system, use the [Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#) for scenarios involving troubleshooting and maintenance.
    -   For Linux or Unix-like OSs, you can [connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#), or [connect to a Linux instance by using an SSH key pair](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using an SSH key pair.md#).
    -   For Windows OSs, you can [connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
3.  [Stop the ECS instance](reseller.en-US/User Guide/Instances/Start or stop an instance.md#).
4.  [Release the instance](reseller.en-US/User Guide/Instances/Release an instance.md#).

To use an ECS instance, follow these steps:

**Change configurations**

You can change the instance type, IP addresses, and network bandwidth of your instance.

-   Subscription instances: [Upgrade configurations of Subscription instances](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#) or [renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)
-   [Change configurations of Pay-As-You-Go instances](reseller.en-US/User Guide/Instances/Change configurations/Change configurations of Pay-As-You-Go instances.md#)

-   [Change public IP address](reseller.en-US/User Guide/Instances/Change IP addresses/Change public IP address.md#)

-   [Convert public IP address to EIP address](reseller.en-US/User Guide/Instances/Change IP addresses/Convert public IP address to EIP address.md#)


If the current operating system no longer meets your business needs, you can [change the operating system](reseller.en-US/User Guide/Instances/Change the operating system.md#).

**Billing**

You can [switch from Pay-As-You-Go to Subscription](../../../../reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#).

Select either of the following methods to renew your Subscription instances:

-   [Manual renewal](../../../../reseller.en-US/Pricing/Renew instances/Manual renewal.md#)
-   [Auto-renewal](../../../../reseller.en-US/Pricing/Renew instances/Auto-renewal.md#)

**Refined management of and control over ECS instances**

You can use the following features to refine your management of and control over ECS instances:

-   [User data](reseller.en-US/User Guide/Instances/User-defined data and metadata/User data.md#)

-   [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#), including [instance identity](reseller.en-US/User Guide/Instances/User-defined data and metadata/Instance identity.md#)

-   [Instance RAM roles](reseller.en-US/User Guide/Instances/Instance RAM roles/What is the RAM role of an instance.md#)


## Create and manage cloud disks {#section_h5j_dbx_wdb .section}

**Basic operations**

To use a cloud disk as a data disk, follow these steps:

1.  [Create a cloud disk](reseller.en-US/User Guide/Cloud disks/Create a cloud disk.md#).
2.  [Attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).
3.  [\(Linux\) Format and mount a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#) or [\(Windows\) Format a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
4.  [Create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) to back up data.
5.  [Detach a cloud disk](reseller.en-US/User Guide/Cloud disks/Detach a cloud disk.md#).
6.  [Release a cloud disk](reseller.en-US/User Guide/Cloud disks/Release a cloud disk.md#).

**Change configurations**

To adjust the capacity of your system disks or data disks, you can [increase the system disk size](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Increase system disk size.md#) or resize the data disks. For more information about resizing a data disk, see [Linux \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md) and [Windows \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows _ Resize a data disk.md#).

**Manage data on a cloud disk**

If data errors occur on a cloud disk, you can use a snapshot to [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) and restore data.

If you want to restore a cloud disk to its initial status after it is created, you can [reinitialize a cloud disk](reseller.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#).

If you want to copy data on an existing cloud disk to a new, empty cloud disk, you can [create a cloud disk from a snapshot](reseller.en-US/User Guide/Cloud disks/Create a cloud disk from a snapshot.md#).

## Create and manage snapshots {#section_bc5_3cx_wdb .section}

**Basic operations**

To use a snapshot, follow these steps:

1.  Create a snapshot by using either of the following methods:
    -   [Create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#).
    -   [Create and delete an automatic snapshot policy](reseller.en-US/User Guide/Snapshots/Create and delete an automatic snapshot policy.md#), and [apply automatic snapshot policies to disks](reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#), to enable automatic snapshot creation.
2.  [View a snapshot chain](reseller.en-US/User Guide/Snapshots/View a snapshot chain.md#).
3.  [Delete unnecessary snapshots](reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#) to reduce charges and free disk space

**Using snapshots**

To copy or back up data, you can use a snapshot to [create a cloud disk from a snapshot](reseller.en-US/User Guide/Cloud disks/Create a cloud disk from a snapshot.md#), or [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#).

To simplify deployment, you can use a system disk snapshot to [create a custom image using a snapshot](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#), and [create an instance from a custom image](reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

## Create and manage custom images {#section_mpg_qvw_wdb .section}

Only custom images can be operated in the ECS console.

You can run a custom image by using the following methods:

-   [Create a custom image using a snapshot](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#)
-   [Create a custom image by using an instance](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#)
-   [Use Packer to create a custom image](reseller.en-US/User Guide/Images/Open source tools/Use Packer to create a custom image.md#)
-   [Copy custom images](reseller.en-US/User Guide/Images/Copy images.md#) across different regions.
-   [Share custom images](reseller.en-US/User Guide/Images/Share images.md#) across different accounts.
-   [Import custom images](reseller.en-US/User Guide/Images/Import images/Import custom images.md#)
-   [Create and import custom images stored on an on-premises server by using Packer](reseller.en-US/User Guide/Images/Open source tools/Create and import on-premises images by using Packer.md#)

You can also [export custom images](reseller.en-US/User Guide/Images/Export custom images.md#) to back up your environment and delete custom images when they are no longer required.

## Create and manage security groups {#section_egt_qcx_wdb .section}

**Basic operations**

To use a security group, follow these steps:

1.  [Create a Security Group](reseller.en-US/User Guide/Security groups/Create a security group.md#).
2.  [Add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#).
3.  [Add to or remove from a security group](reseller.en-US/User Guide/Security groups/Add to or remove from a security group.md#)
4.  [Delete a security group rule](reseller.en-US/User Guide/Security groups/Delete a security group rule.md#).
5.  [Delete a security group](reseller.en-US/User Guide/Security groups/Delete a security group.md#).

**Manage security groups and their rules**

To simplify business deployment, you can [clone a security group](reseller.en-US/User Guide/Security groups/Clone a security group.md#) across regions or network types.

If new security group rules disrupt your online business application, you can  [restore security group rules](reseller.en-US/User Guide/Security groups/Restore security group rules.md#) fully or partially.

## Create and manage SSH key pairs {#section_vpg_qvw_wdb .section}

To use an SSH key pair, follow these steps:

1.  [Create an SSH key pair](reseller.en-US/User Guide/Key pairs/Create an SSH key pair.md#), or [import an SSH key pair](reseller.en-US/User Guide/Key pairs/Import an SSH key pair.md#).
2.  [Bind a SSH key pair](reseller.en-US/User Guide/Key pairs/Attach or remove an SSH key pair.md#), or bind the SSH key pair after a Linux instance is created or when you [create an instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md).
3.  [Connect to a Linux instance by using an SSH key pair](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using an SSH key pair.md#).
4.  [Unbind an SSH key pair](reseller.en-US/User Guide/Key pairs/Attach or remove an SSH key pair.md).
5.  [Delete a SSH key pair](reseller.en-US/User Guide/Key pairs/Delete an SSH key pair.md#).

## Create and manage ENIs {#section_zpg_qvw_wdb .section}

To use an ENI, follow these steps:

1.  [Create an ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Create an ENI.md#).
2.  [Attach an ENI to an instance](reseller.en-US/User Guide/Elastic Network Interfaces/Attach an ENI to an instance.md#), or  [attach an ENI when creating an instance](reseller.en-US/User Guide/Elastic Network Interfaces/Attach an ENI when creating an instance.md#).
3.  Optional. [Configure an ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Configure an ENI.md#).
4.  [Detach an ENI from an instance](reseller.en-US/User Guide/Elastic Network Interfaces/Detach an ENI from an instance.md#).
5.  [Delete an ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Delete an ENI.md#).

## Use tags {#section_dqg_qvw_wdb .section}

You can apply tags to group resources for easier resource organization. To use tags, follow these steps:

1.  [Add a tag to resources](reseller.en-US/User Guide/Tags/Add a tag to resources.md#).
2.  [Filter resources by tags](reseller.en-US/User Guide/Tags/Filter resources by tags.md#).
3.  [Delete a tag](reseller.en-US/User Guide/Tags/Delete a tag.md#).

