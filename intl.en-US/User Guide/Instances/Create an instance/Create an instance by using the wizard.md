# Create an instance by using the wizard {#task_vwq_5g4_r2b .task}

This topic describes how to create an instance by using the ECS console wizard. If you want to create a custom image from a snapshot of your system disk, and then use the custom image to create an ECS instance, see how to create an instance from a custom image.

-   Before creating an ECS instance, you must complete the [preparation work](../../../../reseller.en-US/Quick Start for Entry-Level Users/Preparations.md#).
-   To specify an SSH key pair when creating a Linux instance, you must [create an SSH key pair](reseller.en-US/User Guide/Key pairs/Create an SSH key pair.md#) in the target region.
-   To set the user-defined data, you must prepare the [User Data](reseller.en-US/User Guide/Instances/User-defined data and metadata/User data.md#).
-   To authorize an instance to assume a role, you must [create an instance RAM role and grant it permissions](reseller.en-US/User Guide/Instances/Instance RAM roles/Use the instance RAM role in the console.md#).

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs). 
2.  In the left-side navigation pane, click **instances**. 
3.  On the Instances list page, click **Create Instance**. 
4.  Complete the Basic Configurations as follows: 
    1.  Select a **Billing Method**: **Subscription**, **Pay-As-You-Go** or [Preemptible Instance](../../../../reseller.en-US/Product Introduction/Instances/Preemptible instance.md#). 

        **Note:** For how to create preemptible instances, see [Create preemptible instances](reseller.en-US/User Guide/Instances/Create an instance/Create a preemptible instance.md#).

    2.  Select a region and zone. By default, a zone is assigned randomly. You can select a zone that better meets your needs. For more information about regions and zones, see [Regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#). 

        **Note:** 

        -   After an instance is created, you cannot change its region and zone.
        -   Note that some instance type families are not supported in all regions. For more information, see [Create a compute optimized instance with GPUs](reseller.en-US/User Guide/Instances/Create an instance/Create a compute optimized instance with GPUs.md#), [Create an f1 instance](reseller.en-US/User Guide/Instances/Create an instance/Create an f1 instance.md#), [Create an SCC server instance](reseller.en-US/User Guide/Instances/Create an instance/Create an SCC server instance.md#), and [Create an EBM instance](reseller.en-US/User Guide/Instances/Create an instance/Create an EBM instance.md#).
    3.  Select an instance type and specify the quantity of instances. The availability of an instance type family is determined by the selected region. For the scenarios of each instance type, see [Instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#). 

        **Note:** 

        -   The quota of Pay-As-You-Go or preemptible instances for your account is shown on the page.
        -   To use Elastic Network Interfaces \(ENIs\), select an enterprise-level instance type with at least two vCPU cores or an entry-level instance type with at least four vCPU cores. For more information about the maximum number of ENIs that can be attached to one instance, see [Instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#).
        -   To use an SSD Cloud Disk, select an I/O-optimized instance.
    4.  Select an image. You can select a public image, custom image, shared image, or Marketplace image. 

        **Note:** 

        -   To use an SSH key pair, select a Linux image.
        -   To set User Data, select an image as instructed in [User data](reseller.en-US/User Guide/Instances/User-defined data and metadata/User data.md#).
        -   Public images only include the initial system environment, and more images are available in the image Marketplace.
    5.  Select storage devices: 
        -   **System Disk**: Required. A system disk is required for installing the operating system. Specify the cloud disk category and size for the system disk:

            -   Cloud disk category: The available categories are determined by the selected region.
            -   Size: The default size is 40 GiB, with a maximum size of 500 GiB. If the selected image file is greater than 40 GiB, the size is defaulted to the image file size. The available size range varies with the selected image, as shown in the following table.

                |Image|Available size range|
                |:----|:-------------------|
                |Linux \(excluding CoreOS\) FreeBSD|\[max\{20, ImageSize\}, 500\] GiB. Where, the public image size is 40 GiB for Ubuntu 14.04 32-bit, Ubuntu 16.04 32-bit, and CentOS 6.8 32-bit.|
                |CoreOS|\[max\{30, ImageSize\}, 500\] GiB|
                |Windows|\[max\{40, ImageSize\}, 500\] GiB|

        -   **Data Disk**: Optional. If you create a cloud disk as a data disk at this time, you must select the disk type, size, and quantity, and set whether to [encrypt](../../../../reseller.en-US/Product Introduction/Block storage/ECS disk encryption.md#) it. You can create an empty data disk or create a data disk from a snapshot. Up to 16 data disks can be added.

            **Note:** 

            The data disks added here have the following features:

            -   The billing method is the same as that of the instance.
            -   A Subscription data disk must be released at the same time as its corresponding instance, while a Pay-As-You-Go data disk can be released separately or at the same time as the corresponding instance.
        -   If you have selected an instance type family that has local disks \(such as i1, d1, or d1ne\), the local disk information is displayed. You cannot specify the quantity or category of local disks, which are determined by the selected instance type. For information about the local disks corresponding to various instance types with local disk, see [Instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#).

5.  Click **Next: Networking** to finish the network and security group configuration: 
    1.  Select a network: 
        -   **VPC**: You must select a VPC and a VSwitch. If you do not have a VPC and a VSwitch, you can use the default ones.
        -   **Classic network**: If you purchased the ECS instance for the first time after June 16, 2016, 12:00 \(UTC + 8\), you can no longer select a classic network.
    2.  Configure the Network Billing Method: 
        -   To assign a public IP address to the instance, select **Assign public IP**. Then, select **Pay-By-Traffic** as the network billing method and specify the bandwidth. For public IP addresses assigned in this way, you cannot detach them from the instance. For more information about network billing, see [Billing of Internet bandwidth](../../../../reseller.en-US/Pricing/Billing of Internet bandwidth.md#).
        -   If your instances do not need to access the Internet or your VPC instances [use an Elastic IP \(EIP\) address to access the Internet](../../../../reseller.en-US/Quick Start/Create a VPC.md#), you do not need to assign a public IP address. You can detach an EIP address from an instance.
    3.  Select a security group. If you have not created a security group, you can use the default security group. For the rules of the default security group, see [Default security group rules](reseller.en-US/User Guide/Security groups/Default security group rules.md#). 
    4.  Add an Elastic Network Interface \(ENI\). If your selected instance type supports ENIs, you can add one and specify a VSwitch for it. 

        **Note:** By default, the ENI is released along with the instance. You can detach it from the instance in the [ECS console](reseller.en-US/User Guide/Elastic Network Interfaces/Detach an ENI from an instance.md#) or by using the [DetachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md#) interface.

6.  \(Optional\) Click **Next: System Configurations** to finish the following configuration: 
    -   Select and set logon credentials. You can choose [Set Later](reseller.en-US/User Guide/Instances/Reset an instance password.md#) or set it now. Select a credential based on the image:

        -   Linux: You can select a password or SSH key pair as a logon credential.
        -   Windows: You can only select a password as a logon credential.
    -   Specify the instance name, which is displayed in the ECS console, and the host name, which is displayed inside the guest operating system.

    -   Set the advanced options:

        -   Instance RAM role: Assign a RAM role to the instance.
        -   User Data: Customize the startup behaviors of an instance or pass data into an instance.
7.  \(Optional\) Click **Next: Grouping** to manage instances by group. You can add tags to instances to simplify future management. 
8.  Confirm the order: 
    -   In the **Configurations Selected** area, confirm all the configurations. You can also click the edit icon to re-edit the configuration.
        -   \(Optional\) Click **Save as launch template** to save your configuration as a launch template for future use. For more information, see [Instance launch template](../../../../reseller.en-US/Product Introduction/Instances/Launch templates.md#).
        -   \(Optional\) Click **View Open API** to acquire the API best practices about how to create instances. At the left side, **API Workflow** explains the related APIs and request parameter values for the current operation. At the right side, the programming language-specific samples are given for you to use. Currently, **Java** and **Python** samples are provided. For more information, see ECS API Reference [Overview](../../../../reseller.en-US/API Reference/Introduction.md#).
    -   \(Optional\) If the billing method is **Pay-As-You-Go**, you can set the **Auto Release Schedule**.
    -   \(Optional\) If the billing method is **Subscription**, you can set the duration and select whether to enable **Auto renewal**.
    -   Confirm the configuration costs. The billing methods for an instance and its Internet bandwidth determine the displayed cost information, as shown in the following table.

        |Instance billing method|Estimated fee|
        |:----------------------|:------------|
        |Pay-As-You-Go or preemptible instance|Internet traffic fee + configuration fee. The configuration fees include: the instance type \(vCPU and memory\), the system disk, data disks \(if any\), and local disks \(if any\).|
        |Subscription|Internet traffic fee + configuration fee. Configuration fees include: the instance type \(vCPU and memory\), the system disk, data disks \(if any\), and local disks \(if any\).|

    -   Read and confirm you agree to the **ECS Service Level Agreement**.
9.  Click **Create Instance**. 

After the instance is activated, click **Console** to view the instance details in the console. In the **Instances** list of the relevant region, you can view the information of the new instance, including the instance name, the Internet IP address, and the private IP address.

-   You can create an FTP site on the instance for transferring files. For more information, see [Build an FTP site on an ECS instance](https://partners-intl.aliyun.com/help/doc-detail/51998.htm).
-   To secure your instance after creation, we recommend that you perform security compliance inspection and configuration:
    -   Linux instances: See [Harden operating system security for Linux](https://partners-intl.aliyun.com/help/faq-detail/49809.htm) in Security Advisories.
    -   Windows instances: See [Harden operating system security for Windows](https://partners-intl.aliyun.com/help/faq-detail/49781.htm) in Security Advisories.
-   If a data disk is created along with the instance, you must partition and format the disk before use. For more information, see [Format a data disk for Windows instances](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#) or [Format a data disk for Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).

