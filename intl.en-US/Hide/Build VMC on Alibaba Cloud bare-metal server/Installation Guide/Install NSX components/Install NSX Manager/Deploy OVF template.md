# Deploy OVF template {#task_zxl_ql2_kgb .task}

The NSX Manager is a powerful and centralized network management component of NSX, providing an aggregated system view. It can be installed as a virtual appliance on your ESXi hosts within the vCenter Server environment. This topic guides you through how to deploy NSX Manager by importing an OVF \(Open Virtualization Format\) template.

You must have:

-   Downloaded the OVF template from VWware official website. For more information. see [Download vCenter and NSX components](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Download components.md#).
-   Started the Windows instance with vCenter installed.
-   Allowed the inbound access from port HTTPS 443 to the Windows instance firewall. For more information about how to remove the access limit, see [Add a security group rule](../../../../../intl.en-US/User Guide/Security groups/Add security group rules.md#).
-   Added the bare-metal hosts in the vCenter.

1.  Open the Internet IP address of the Windows instance in a browser, such as Chrome. 
2.  Log in to VMware vSphere Web Client. 
3.  Right-click the IP of the host that provides network management utilities and then select **Deploy OVF Template...**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835683_en-US.png)

4.  On the Select template page, click **Browse** and navigate or link to the .ova file, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835685_en-US.png)

5.  Enter a name for the NSX Manager, and select a folder or vCenter Server datacenter , and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835687_en-US.png)

6.  In the **Browse** area of the Select a resource page, select a host on which to deploy the NSX Manager appliance, and then click **Next**. Normally, you would place the NSX Manager in a host or cluster that provides network management utilities. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835688_en-US.png)

7.  On the **Review details** tab, check the template details thoroughly and click **Next**. 
8.  Select a configuration size: small, medium, or large. The system requirements vary depending on the configuration size. Here, we take Medium as an example. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835692_en-US.png)

9.  Select a datastore to store the NSX Manager virtual appliance files, and then click **Next**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/93420/154708748836881_en-US.png) 
10. Select the port group or destination network for the NSX Manager. You can change the settings after the NSX Manager is deployed. So the destination network is temporarily set to **VM Network**, and click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748836589_en-US.png)

11. On the **Customize template** page, set the password for the **CLI admin user** according to the rules highlighted in the following figure. 

    **Note:** The core services on the appliance do not start until a password with sufficient complexity has been set.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835881_en-US.png)

    1.  If you are notified to correct the invalid settings, operate according to the wizard display. 
    2.  Configure the following deployment settings for the OVF templates. Make sure that you have entered the fields by using the parameter values provided by Alibaba Cloud. For details about how to acquire the values, run the ipconfig within the Windows instance, for more information, see [the following notice](#HowToObtainTheValues). 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835877_en-US.png)

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835878_en-US.png)

12. On the Customize template page, set a password for the System Root user according to the password complexity rules. 

    **Note:** The core services on the appliance do not start until a password with sufficient complexity has been set.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748836591_en-US.png)

13. NSX Manager is in the same network as the Windows instance on which the vCenter has been installed. Execute command `ipconfig/all` in the Windows command console, find the DNS IP addresses, the default IPv4 gateway IP address, and the management network netmask IP address, then specify those settings in corresponsing fields. Set the **Hostname** to nsx-manager. Select an unused secondary management ENI binded to the host that provids network management utilies, find its IP address on the Network Interfaces page of the ECS console and specify the setting of the **Management Network IPv4 Address**. Accept the nsx-manager role. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835877_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835878_en-US.png)

14. In the **Services Configuration** area of the Customize template page, select **Allow root SSH logins** and **Enable SSH**, and then click **Next**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748835879_en-US.png)

15. If you enabled SSH, make sure that you can SSH to your NSX Manager. 
    -   You can ping your NSX Manager.
    -   NSX Manager can ping its default gateway.
    -   NSX Manager can ping the hypervisor hosts that are in the same network as the NSX Manager.
    -   NSX Manager can ping its DNS server and its NTP server.
16. On the Ready to complete page, confirm the configuration data, and then click **Finish**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748935750_en-US.png)

17. Check the status of the NSX Manager deploying process in the **Recent Tasks** list. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708748936617_en-US.png)


