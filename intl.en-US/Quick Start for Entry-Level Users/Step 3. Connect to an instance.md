# Step 3. Connect to an instance {#task_728112 .task}

After creating an ECS instance, you can connect to it by using different methods. This topic describes how to connect and manage your ECS instance by using the **Management Terminal** in the ECS console.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the upper-left corner, select the target region. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123261/156229503450161_en-US.png)

4.  In the instances list, find the ecs-01 instance that has been created. In the **Actions** column, click **Connect**.
5.  In the displayed VNC Password dialog box, copy the password, then click **Close**. 

    **Note:** The VNC password appears only once. Remember the password so that you can use it to connect to the Management Terminal later.

6.  In the displayed Enter VNC Password dialog box, paste the password, and then click **OK**.
7.  Log on to the ECS instance. Do the following according to your operating system: 
    -   For a Linux instance, enter the username **root** and the instance logon password that is set when you [create an instance](intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).
    -   For a Windows instance, in the upper-left corner of the Management Terminal interface, choose **Send Remote Call** \> **CTRL+ALT+DELETE** to enter the logon interface. Enter the password set when you [create an instance](intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) to log on.

If you forget your instance logon password, [reset the instance password](../intl.en-US/Instances/Manage instances/Reset an instance logon password.md#).

