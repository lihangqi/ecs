# Step 3: Connect to an instance {#concept_irq_dwd_wdb .concept}

After creating an ECS instance, you can connect to it by using different methods. This article introduces how to connect and manage your ECS instance using the **Management Terminal** in the ECS console. For more information, see [connect to instances](../../../../reseller.en-US/User Guide/Connect to instances/Overview.md#).

## Procedure {#section_orq_gwd_wdb .section}

1.  Log on to the [ECS Console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region. In this example, China East 1 is selected.
4.  In the instances list, find the ecs-01 instance that has been created. In the **Actions** column, click **Connect**.
5.  In the pop-up VNC Password dialog box, copy the password, then click **Close**.

    **Note:** The VNC password appears only once. Remember the password so that you can use it to connect to the Management Terminal later.

6.  In the pop-up Enter VNC Password dialog box, paste the password, and then click **OK**.
7.  Log on to the ECS instance. Do the following according to the operating system:

    -   For a Linux instance, enter the username **root** and the instance logon password that is set when you [create an instance](reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).
    -   For a Windows instance, in the upper left corner of the Management Terminal interface, click **Send Remote Call** \> **CTRL+ALT+DELETE** to enter the logon interface. Enter the password set when you [create an instance](reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) to log on.
    If you forget your instance logon password, [reset the instance password](../../../../reseller.en-US/User Guide/Instances/Reset an instance password.md#).


