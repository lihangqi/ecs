# Join NSX Controller to NSX Manager {#task_arr_kz1_hgb .task}

This topic describes how to join NSX Controller to NSX Manager so that they can communicate with each other.

1.  Right-click the NSX Manager virtual appliance, and then click **Power** \> **Power on** in the vCenter Server. 
2.  Right-click the NSX Controller virtual appliance, and then click **Open Console**. 
3.  Enter the NSX Manager CLI admin username and password to log on to NSX Manager. 
4.  Run the `get certificate api thumbprint` command to obtain the certificate thumbprint of NSX Manager.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708736436860_en-US.png)

 
5.  Right-click the NSX Controller virtual appliance, and then click **Power** \> **Power on** in the vCenter Server. 
6.   Right-click the NSX Controller virtual appliance, and then click **Open Console**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708736435865_en-US.png)

 
7.  Enter the CLI admin username and password to log on to NSX Controller. 

    **说明：** If you have multiple NSX Controller appliances, you need to run the `join management-plane` command on each NSX Controller appliance. The command includes the following information:

    -   Hostname or IP address of the NSX Manager with an optional port number
    -   Username of NSX Manager
    -   Certificate thumbprint of NSX Manager
    -   Password of NSX Manager
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708736435866_en-US.png)

8.   Verify the result by running the `get managers` command on your NSX Controller.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708736435867_en-US.png)

 
9.   On the NSX Manager appliance, run the `get management-cluster status` command and verify that all your NSX Controllers are listed.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708736436850_en-US.png)

 

