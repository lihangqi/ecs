# Connect to a Windows instance from a mobile device {#concept_smr_xnw_wgb .concept}

This topic describes how to connect to a Windows instance from a mobile device \(iOS or Android\) by using Microsoft Remote Desktop.

## Prerequisites {#section_unw_brq_pgb .section}

-   The instance is in the **Running** state.
-   The instance has a public IP address and is accessible from the Internet.
-   The logon password for the instance is set. Moreover, if the password was lost, you can [reset the instance password](reseller.en-US/Instances/Manage instances/Reset an instance password.md#).
-   The security group of the instance has [the following security group rules](../../../../../reseller.en-US/Security/Security groups/Add security group rules.md#):

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration not required|Inbound |Allow |SSH \(22\)|22/22|CIDR block|0.0.0.0/0|1|
    |Classic  |Internet|


## Procedure {#windows .section}

Check that you have installed Microsoft Remote Desktop \(RD\).

1.  Start the RD Client. In the upper right corner, click **+**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927115327_en-US.PNG)

2.  On the Add New page, select **Desktop**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927115329_en-US.PNG)

3.  On the Edit Desktop page, enter the connection information and click **Save**. The following connection information is required:
    -   **PC Name**: Enter the public IP address of the Windows instance to be connected.
    -   **User Account**: Enter the account name **administrator** and the logon password of the Windows instance.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927125330_en-US.PNG)

4.  On the Remote Desktop page, click the icon of the target Windows instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927125331_en-US.PNG)

5.  On the confirmation page, confirm the message and click **Accept**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927125332_en-US.PNG)


If you have successfully connected to the Windows instance, the following screen is displayed. 

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15547927125333_en-US.PNG)

