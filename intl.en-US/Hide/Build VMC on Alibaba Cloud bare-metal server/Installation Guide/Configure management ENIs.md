# Configure management ENIs {#task_mpb_1vs_ggb .task}

Check the corresponding relations among the ENI \(MAC address and IP address\), host PCI, and vmnic, and set the management ENI to the **Passthrough capable** mode.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home). 
2.  In the left-side navigation pane, click **Network and Security** \> **ENI**. 
3.  Find and record the MAC addresses corresponded to the three secondary management network interfaces have created. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83721/154705640535525_en-US.png)

4.  Open an SSH session to the host that provides network management utilities. 
5.  Enter the esxcli network nic list command. Find and record the PCI Device values corresponded to the MAC addresses of the three secondary management network interfaces from the response parameters. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83721/154705640535517_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83721/154705640635518_en-US.png)

6.  Connect to your Windows instance where vCenter Server resides, and use the browser on the instance to access the private IP address of the host that provides network management utilities. 
7.  Enter the username and password \(the username and password you set when creating ESXi image\) of the ESXi system to log on to the ESXi management page. 
8.  Go to the PCI device page, locate and check the PCI Device values you have recorded, and then click **Toggle passthrough**. Set the three secondary management network interfaces to the **Passthrough capable** mode. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83721/154705640635558_en-US.png)


