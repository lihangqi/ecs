# Add Edge Cluster {#task_asp_hz1_hgb .task}

This topic describes how to add Edge Cluster.

1.  Log on to the Windows instance where VMware vCenter Server is installed.
2.  Log on to NSX Manager through https://\(Need to check with Gaoxin\).

1.   Select **Fabric** \> **nodes**. On the**Edge Clusters** tab, click **ADD**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136008_en-US.png)

 
2.   Enter an edge cluster name and profile, and then click**ADD**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136009_en-US.png)

 
3.  Add two hosts. 
    1.  On the Hosts tab, click **ADD**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136010_en-US.png) 
    2.  Complete the configurations. 

        The parameters are described as follows:

        |Parameter|Description|Example|
        |:--------|:----------|:------|
        |Name|Indicates the host name.|esxi-host1|
        |IP Addresses|Indicates ESXi host IP address.|192.168.10.12|
        |Operating System|Select **ESXi**.|ESXi|
        |Username|Use **root**|root|
        |Password|Indicates the logon password that set for this ESXi host.|N/A|

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136011_en-US.png) 

    3.  In the Invalid Thumbprint dialog box, click **ADD**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136012_en-US.png) 
    4.  In the Invalid Thumbprint dialog box, click **ADD**. 
    5.  Repeat the preceding steps to add the other ESXi host. 
4.  Go back to the Hosts tab, and the two hosts are displayed. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85016/154708746136016_en-US.png) 

