# Configure the VMKernel network interface {#task_ilh_jz1_hgb .task}

This topic describes how to configure the VMKernel network interface for NSX Edge.

Log on to the Windows instance where VMware vCenter Server is installed.

1.  Log on to VMware vSphere Web Client. 
2.  Right-click the NSX-edge appliance and click **Edit settings...**. 
3.  Delete two redundant default network adapters. 
4.  Change the settings for the other two network adapters. 

    1.  From the **New adapter 1**drop-down list, select **Show more networks...**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035938_en-US.png)

    2.  Select **ext-DPortGroup**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035939_en-US.png)

    3.  Add vtep-DPortGroup referring to the preceding steps. 
    Two network adapters are specified as follows.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035942_en-US.png)

5.  Select **PCI device** from the **New device** drop-down list to add a PCI device to the NSX edge appliance. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035943_en-US.png)

    From the **New PCI device**drop-down list, select the secondary management ENI assigned to NSX Edge duing the edge installation. Refer to [Creation of vmc vm Network Unit via NSX-Manager \(not yet done with this architecture, a little bit more content\)](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Installation Guide/Install NSX components/Install NSX Manager/Configure the NSX Manager.md#) to choose the right PCI device.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035945_en-US.png)

6.  Refer to [Creation of vmc vm Network Unit via NSX-Manager \(not yet done with this architecture, a little bit more content\)](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Installation Guide/Install NSX components/Install NSX Manager/Configure the NSX Manager.md#) to figure out the correct MAC addresses of the vtep uplink port and ext uplink port, and then change the MAC addresses of the two VMKernel network adapters. 
    1.  Unfold **Network adapter 1** and then select **Manual** button to change the **MAC Address**. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035949_en-US.png)

    2.  Change the MAC address for the other network adapter referring to the preceding step. 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744035954_en-US.png)

7.  Reboot the host that provides network management utilities.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708744036870_en-US.png)

 

