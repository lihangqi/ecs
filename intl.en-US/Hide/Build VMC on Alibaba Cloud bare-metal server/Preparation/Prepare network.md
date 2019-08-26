# Prepare network {#task_fzn_k5s_ggb .task}

This topic guides you through how to create private network in Alibaba Cloud. You will create one VPC and six VSwitch for further use.

1.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/). 
2.  Select the region of the VPC. The VPC and the cloud resources to deploy must be located in the same region. 
3.  Refer to the VPC document [Manage a VPC](../../../../../intl.en-US/User Guide/Manage a VPC.md#) to create a VPC. 

    **Note:** In this tutorial, a VPC named "vmware-on-xdragon" is created, and the **IPv4 CIDR Block** is set to 192.168.0.0/16.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83713/154705612635457_en-US.png)

4.  Go back to the VPC console, and select the region of the VPC to which the VSwitch belongs. 
5.  In the left-side navigation pane, click **VSwitches**. 
6.  Refer to the VPC document [Manage VSwitches](../../../../../intl.en-US/User Guide/Manage VSwitches.md#) to create six VSwitches. In this tutorial, the necessary fields are entered as follows: 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83713/154705612635458_en-US.png)

    **Note:** 

    -   The VSwitch, EBM, and ESXi host must be located in the same **Zone**.
    -   The name and IPv4 CIDR block are as follows:

        |VSwitch name|IPv4 CIDR block|
        |:-----------|:--------------|
        |ecsvm|192.168.60.0/24|
        |external|192.168.50.0/24|
        |vtep\_overlay|192.168.40.0/24|
        |vsan|192.168.30.0/24|
        |vmotion|192.168.20.0/24|
        |management|192.168.10.0/24|


After you complete the operation, six VSwitches are created with the following **Name** and **IPv4 CIDR Block**. And they are all controlled by one VPC **vmware-on-xdragon**:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83713/154705612635498_en-US.png)

[Create bare-metal servers and ECS instance](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Create bare-metal servers and ECS instance.md#)

