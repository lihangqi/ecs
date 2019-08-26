# Create a VMFS Datastore {#task_u2t_x5s_ggb .task}

From the Windows instance where vCenter Server resides, access the private IP addresses of the two ESXi hosts \(the private IP addresses of the Elastic Bare Metal Instances\), and then create a Datastore respectively.

1.  Right-click the first ESXi host, and then select **Storage** \> **New Datastore...**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235472_en-US.png) 
2.  Select VMFS for Type. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235473_en-US.png) 
3.  Enter the Datastore name. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235474_en-US.png) 
4.  Select VMFS 5 for the VMFS version. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235475_en-US.png) 
5.  Configure the partition. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235476_en-US.png) 
6.  Check the settings, and then click **Finish**. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629235477_en-US.png) 
7.  Repeat the preceding steps to create a datastore for the second host. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83719/154705629335478_en-US.png) 

