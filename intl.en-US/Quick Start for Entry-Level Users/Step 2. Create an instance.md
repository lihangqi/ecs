# Step 2. Create an instance {#task_zjx_p1f_5db .task}

This topic uses an entry-level instance as an example to describe how to quickly create an instance on the ECS console.

Instances are the core components of ECS and embody the computing capability of ECS. To help you get familiar with the ECS console, this topic describes how to create a Pay-As-You-Go, Pay-By-Traffic entry-level ECS instance on the ECS console. For more information, see [Create an instance by using the wizard](../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). You can also call the [RunInstances](../reseller.en-US/API Reference/Instances/RunInstances.md#) action to create an instance.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  On the Instances page, click **Create Instance** to enter the Custom Launch purchase page.
4.  Follow these steps to finish Basic Configurations. 
    1.  Select a billing method. In this example, **Pay-As-You-Go** is selected.
    2.  Select a region, such as **China \(Hangzhou\)**. The system randomly allocates a zone by default. 

        **Note:** After an instance is created, you cannot change its region or zone.

    3.  Select an instance type and specify the quantity of instances. The available [instance type family](instance type family../DNECS19100341/EN-US_TP_9548.dita#concept_sx4_lxv_tdb) is determined by the region you selected. In this example, choose **All Generations** \> **x86-Architecture** \> **Entry-Level \(Shared\)** \> **Compact Type xn4**.
    4.  Select an image. In this example, a CentOS 7.6 public image is selected.
    5.  Select a storage space. In this example, only a system disk is used, and a 40 GiB Ultra Cloud Disk is selected by default.
5.  Click **Next: Networking** to finish the networking and security group configuration. 
    1.  Select **VPC** as the network type. In this example, the default VPC and VSwitch are used.
    2.  Set the network billing method. In this example, **Assign public IP** and **Pay-By-Traffic** are selected.
    3.  Select a security group. You can use the default security group if you do not create one.
    4.  Add an Elastic Network Interface \(ENI\). Skip this step if the selected instance type does not support ENI.
6.  Click **Next: System Configurations**. Set parameters as needed. We recommend that you set **Logon Credentials** and **Instance Name**. In this example, **Password** is selected for **Logon Credentials** and the instance name is set to **ecs-01**.
7.  Click **Next: Grouping**. You can set the options as needed. In the case of multiple instances, we recommend that you add labels for ease of instance management.
8.  Click **Next: Preview**. Confirm the selected configuration. You can also click the edit icon to modify the configurations.
9.  Read and confirm **Terms of Service**, and then click **Create Instance**.

Click **Console** to return to the ECS console. It usually takes one to two minutes to complete instance creation. Click the refresh button to check if the instance is created. If the newly created ECS instance is in a **Running** status, the instance is created successfully.

After a Windows instance is created, you need to initialize the operating system of the instance. This operation usually takes two to three minutes. Do not restart the instance during initialization. You can [connect to the instance](connect to the instanceEN-US_TP_9602.dita#task_728112) only after the initialization is complete. If you create a non-I/O-optimized Windows instance, it takes 10 minutes to complete the initialization.

