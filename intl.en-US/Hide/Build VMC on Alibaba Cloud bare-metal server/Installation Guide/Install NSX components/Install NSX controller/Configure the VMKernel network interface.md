# Configure the VMKernel network interface {#task_cdg_lz1_hgb .task}

This topic describes how to configure the VMKernel network interface for NSX Controller.

1.  Log on to VMware vSphere Web Client. 
2.   In the **Hosts and Clusters** navigation pane, right-click NSX Controller, and then click **Edit Settings...**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85021/154708735336646_en-US.png)

 
3.   Clear the invalid network adapter.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85021/154708735335857_en-US.png)

 
4.  Add a PCI device to NSX Controller. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85021/154708735335858_en-US.png)

5.   From the **New PCI device**drop-down list, select the secondary management ENI assigned to NSX Controller duing the NSX Controller installation. Select the correct PCI device. For more information, see [Creation of vmc vm Network Unit via NSX-Manager \(not yet done with this architecture, a little bit more content\)](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Installation Guide/Install NSX components/Install NSX Manager/Configure the NSX Manager.md#).![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85021/154708735335860_en-US.png)

 

