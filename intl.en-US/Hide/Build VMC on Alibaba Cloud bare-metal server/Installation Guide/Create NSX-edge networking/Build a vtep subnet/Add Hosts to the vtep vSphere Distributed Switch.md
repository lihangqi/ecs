# Add Hosts to the vtep vSphere Distributed Switch {#task_ct4_hj1_hgb .task}

This topic introduces the steps to add a host to the vtep vSphere Distributed Switch.

1.  You have created a vtep-VDS.
2.  Log on to the Windows instance on which the vCenter has been installed.
3.  Obtain and record the vmnic names of the two vtep ENIs of the host that provides network management utilities. The procedure is as follows:
    1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
    2.  In the left-side navigation pane, click **Network and Security** \> **ENI**.
    3.  In the **ENI** list, find and record the MAC addresses corresponded to the two vtep ENIs you have created for the host that provides network management utilities.
    4.  Open an SSH session to the host that provides network management utilities. Run the esxcli network nic list command. Find and record the two name values corresponded to the MAC addresses of the two vtep ENIs, as shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84992/154705653935589_en-US.png)


1.   Log on to the **vSphere Web Client**. In the left-side navigation pane, click **vtep-vds**, and then click **Actions** \> **Add and Manage Hosts**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935572_en-US.png)

 
2.   On the Select task page, select **Add hosts**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935573_en-US.png)

 
3.   On the **Select hosts** page, click **New hosts**, check the IP of the host that provides network management utilities, and then click **OK**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935574_en-US.png)

 
4.   On the Select hosts page, you can see the host checked in the previous step. Click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935575_en-US.png)

 
5.   On the Select network adapter tasks page, check**Manage physical adapters** and **Manage VMkernal adapters**, as shown in the following figure. Click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935576_en-US.png)

 
6.   On the Manage physical network adapters page, add an uplink for any vmnic value recorded in step 3 of the prerequisites, as shown in the following figure.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935577_en-US.png)

 
7.   On the Manage VMkernal network adapters page, you can choose to add a VMKernel adapter now or later. Click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935578_en-US.png)

 
8.   Review whether this configuration change might impact some network dependent services. Click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935579_en-US.png)

 
9.   On the Ready to complete page, you can view the details of your configurations. Click Finish to confirm the configurations.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84968/154705653935580_en-US.png)

 

