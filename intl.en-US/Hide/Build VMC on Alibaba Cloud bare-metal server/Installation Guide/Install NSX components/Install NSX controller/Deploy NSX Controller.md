# Deploy NSX Controller {#task_xcw_lz1_hgb .task}

This topic describes how to deploy NSX Controller by using the OVF template.

1.  Log on to the Windows instance where VMware vCenter Server is installed.
2.  Log on to VMware vSphere Web Client.
3.  Download and purchase the OVA file to install NSX Controller. For more information, see [Download vCenter and NSX components](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Download components.md#).

1.  Right-click the IP address of the host that provides network management utilities, and then select **Deploy OVF Template...**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734135837_en-US.png)

2.  On the Select template page, click **Browse** and navigate or link to the .ova file, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734135839_en-US.png)

3.  Enter a name for NSX Controller, select a folder or vCenter Server datacenter, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734135840_en-US.png)

4.  On the **Browse** tab page of the Select a resource page, select a host on which you want to deploy the NSX Controller appliance, and then click **Next**. 

    **说明：** We recommend that you deploy NSX Controller in a host or cluster that provides network management utilities.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734135841_en-US.png)

5.  On the Review details page, confirm the template details, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235842_en-US.png)

6.  Select a configuration size: small, medium, or large. In this example, select **Medium**. 

    **说明：** The system requirements vary with the configuration size.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235843_en-US.png)

7.  Select a datastore to store the NSX Controller virtual appliance files, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235844_en-US.png)

8.  Select the port groups or networks on which you want to deploy the NSX Controller interface, and then click **Next**. 

    **说明：** You can change the networks after NSX Controller is deployed. In this example, the destination network is temporarily set to **VM Network**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235846_en-US.png)

9.  On the Customize template page, set the password of the CLI admin User according to the rules highlighted in the following figure. 

    **说明：** The core services on the appliance do not start until a password with sufficient complexity is set.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83722/154708734235536_en-US.png)

10. On the Customize template page, set the password of the System Root User according to the password complexity rules. 

    **说明：** The core services on the appliance do not start until a password with sufficient complexity is set.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235848_en-US.png)

11. Run the `ipconfig/all` command in the Windows command console, find the DNS IP addresses, the default IPv4 gateway IP address, and the management network netmask IP address, and then make these settings in the corresponding fields. 

    **说明：** NSX Controller is in the same network as the Windows instance on which the vCenter is installed.

12.  Set the **Hostname** to nsx-controller. Select an unused secondary management ENI attached to the host that provides network management utilities, find its IP address on the Network Interfaces page of the ECS console, and set the **Management Network IPv4 Address**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235850_en-US.png)

  
13.  In the **Services Configuration** area of the Customize template page, select **Allow root SSH logins** and **Enable SSH**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85017/154708734235916_en-US.png)

  

    If you enable SSH, make sure that you can log on to your NSX Controller through SSH.

    -   You can ping your NSX Controller.
    -   NSX Controller can ping its default gateway.
    -   NSX Controller can ping the hypervisor hosts that are in the same network as NSX Controller.
    -   NSX Controller can ping its DNS server and NTP server.
14. Confirm the configuration data, and then click **Finish**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235852_en-US.png)

15.  Verify that the NSX Controller deployment process is completed in the **Recent Tasks** list.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85022/154708734235853_en-US.png)

 

