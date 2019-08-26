# Configure user data {#concept_pth_dbx_wgb .concept}

This topic describes how to configure generated user data for an instance in the ECS console, and how to view and modify existing user data.

## Limits {#section_abk_ckm_qgb .section}

The user data function has the following limits:

-   User data can be configured for instances in a VPC only.
-   For [phased-out instance types](reseller.en-US/Instances/Instance type families/Phased-out instance types.md#), only I/O-optimized instance types support user data. For other [instance type families](../../../../reseller.en-US/Instances/Instance type families.md#), all instance types support user data.
-   User data must be Base64-encoded before it is configured for instances. Additionally, the original user data cannot exceed 16 KB.
-   An instance must use a public image or a custom image that is created from a public image. Furthermore, the following table describes the operating systems that are supported.

    |Platform|Operating system|
    |:-------|:---------------|
    |Windows|Windows Server 2008 R2 or newer|
    |Linux|     -   CentOS
    -   Ubuntu
    -   SUSE Linux Enterprise
    -   OpenSUSE
    -   Debian
    -   Aliyun Linux
 |


## Configure user data for an instance {#SetUserDataExample .section}

**Note:** The following procedure takes a Linux instance running CentOS as an example.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Create a Linux instance by following the instructions in [Step 2. Create an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

    **Note:** During instance creation, enter user data in the **user data** box below **Advanced \(based on instance RAM roles or cloud-init\)**. If your user data is Base64-encoded, select the **The text is Base64-encoded** check box.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130417/155609981943603_en-US.png)

3.  After the instance starts, connect to it by following the instructions in [Overview of connecting to an ECS instance](reseller.en-US/Instances/Connect to instances/Overview.md#).
4.  Check the startup results against the configured user data. If exceptions occur, check the log files. The following output is from a CentOS instance which is configured with user data through an Upstart Job script:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130417/155609981943606_en-US.png)

    As shown in the preceding output, a startup task file part-001.conf is created in the folder /etc/init of the instance.


You can also set user data by calling [RunInstances](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) through Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK. The relevant parameter is UserData.

## View user data {#linuxCustomData .section}

You can view user data through the dedicated server 100.100.100.200. To do so, follow these steps:

1.  Connect to the instance. For more information, see [Overview of connecting to an ECS instance](reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Run the following commands in the instance:
    -   For Linux, run curl http://100.100.100.200/latest/user-data.
    -   For Windows, run Invoke-RestMethod http://100.100.100.200/latest/user-data/.

You can also view user data by calling [DescribeUserData](../../../../reseller.en-US/API Reference/Instances/DescribeUserdata.md#) through Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

## Modify user data {#linuxCustomData2 .section}

You must stop the target instance before you modify its user data. After the modification, you need to check if the modified user data needs to be run according to the script type and module type. For more information, see [User data](reseller.en-US/Instances/Manage instances/User-defined data/User data.md#).

**Note:** For Pay-As-You-Go VPC instances, if you need to restart an instance immediately after modifying its user data, we recommend that you turn off the option of No fees for stopped instances.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target instance, and in the **Actions** column, select **Instance Settings** \> **Set User Data**.
5.  In the displayed dialog box, enter the relevant information and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130417/155609981943608_en-US.png)


You can also modify user data by calling [ModifyInstanceAttribute](../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#) through Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

