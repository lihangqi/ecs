# Add Hosts to the vMotion vSphere Distributed Switch {#task_wyj_r5s_ggb .task}

Add two ESXi hosts to the newly created vMotion VDS.

1.  View the corresponding vmnic values of the two vmotion ENIs. For more information about creating ENIs, see [Attach ENIs](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Attach Elastic Network Interfaces.md#). 
    1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home). 
    2.  In the left-side navigation pane, click **Network and Security** \> **ENI**. 
    3.  Find and record the corresponding MAC addresses of the two vmotion ENIs you have created. 
    4.  Open SSH sessions to the two ECS Bare Metal instances separately, and run the esxcli network nic list command. Find and record the values of the name column and MAC Address column from the response parameters. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645135626_en-US.png)

    5.  Compare the MAC address on the ENI page of the ECS console and that in the response parameters, and find the corresponding vmnic values. 
2.  In the left-side navigation pane, select the newly created vMotion VDS, and click **Actions** \> **Add and Manage Hosts...**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645135592_en-US.png)

3.  Select **Add hosts**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235593_en-US.png)

4.  Check both ESXi hosts, and click **OK**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235594_en-US.png)

5.  Check **Manage physical adapters** and **Manage VMkernel adapters**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235595_en-US.png)

6.  Select the vmnic of the ECS Bare Metal \(EBM\) instance working as the network node and computing node, and click **Assign uplink**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235596_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235597_en-US.png)

7.  Select the vmnic of the EBM instance working as the network node and computing node, and click **Assign uplink**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235598_en-US.png)

    **Assigned** is displayed besides the two EBM instances.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235600_en-US.png)

8.  Add vMotion VMkernel adapters separately to the two ESXi hosts. 
    1.  Click **New adapter**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235601_en-US.png)

    2.  Select the network. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235602_en-US.png)

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235603_en-US.png)

    3.  Set the port properties, and check **vMotion**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235605_en-US.png)

    4.  Select **Obtain IPv4 settings automatically**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235606_en-US.png)

    5.  Confirm the settings. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235607_en-US.png)

    6.  Repeat the previous steps to add an adapter for the other ESXi host. The result is displayed as follows. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645235608_en-US.png)

9.  Confirm the possible impacts. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645335609_en-US.png)

10. The configuration is completed. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83715/154705645335610_en-US.png)


