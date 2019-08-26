# Create an NFS Datastore {#task_iyb_tm5_ggb .task}

This topic describes how to create an NFS Datastore.

1.  Log on to the [NAS console](https://nas.console.aliyun.com/#/ofs/list) to create a file system. For more information, see[Create a file system](../../../../../intl.en-US/Quick Start/Create a file system.md#) and [Add a mount point](../../../../../intl.en-US/Quick Start/Add a mount point.md#). 
2.  Click the name of the file system, and then go to the details page to view the server address of the file system. The address is used for creating a Datastore in an ESXi host. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83765/154705631235493_en-US.png) 
3.  Log on to the ESXi host through https to add a Datastore. 
4.  Right-click the first ESXi host, and select **Storage** \> **New Datastore...**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705631235472_en-US.png) 
5.  Select NFS for Type. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83765/154705631235486_en-US.png) 
6.  Select NFS 3 for the version. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83765/154705631235487_en-US.png) 
7.  Set the name and folder, and enter the server address of the file system. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83765/154705631235488_en-US.png) 
8.  Check the settings, and click**Finish**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83765/154705631335489_en-US.png) 

