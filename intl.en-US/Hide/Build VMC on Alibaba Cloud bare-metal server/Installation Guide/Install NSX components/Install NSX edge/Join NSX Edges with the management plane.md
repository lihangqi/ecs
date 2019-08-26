# Join NSX Edges with the management plane {#task_vtx_jz1_hgb .task}

This topic describes how to join NSX Edges with the management plane.

-   You must log on to the Windows instance where VMware vCenter Server is installed.
-   You have obtained the Certificate Thumbprint of the NSX Manager in the [preceding topics](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Installation Guide/Install NSX components/Install NSX controller/Configure the VMKernel network interface.md#).

1.  Right-click the NSX edge virtual appliance and then click **Power** \> **Power on** to launch the NSX edge. 
2.   Right-click the NSX edge virtual appliance and then click **Open Console**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708745035865_en-US.png)

 
3.  Enter the CLI admin username and password to log in to the NSX edge. 
4.  Run the `join management-plane` command. 

    Provide the following information:

    -   Hostname or IP address of the NSX edge with an optional port number.
    -   Username of the NSX Manager.
    -   Certificate thumbprint of the NSX Manager.
    -   Password of the NSX Manager.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708745135866_en-US.png)

5.  Verify the result by running the `get managers` command on your NSX Edge. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85018/154708745136871_en-US.png)

6.   In the NSX Manager UI, select **Fabric** \> **Nodes**, and the NSX Edge appears on the Edges tab. MPA connectivity should be **Up**. If MPA connectivity is not **Up**, try refreshing the browser screen.![](images/36872_en-US.png)

 

