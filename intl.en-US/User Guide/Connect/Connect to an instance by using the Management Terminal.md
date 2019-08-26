# Connect to an instance by using the Management Terminal {#concept_sdk_1jx_wdb .concept}

You can use the Management Terminal, also known as VNC, to connect to an ECS instance. Specifically, when the remote access software programs that you are using, such as PuTTy, Xshell, or SecureCRT, do not work.

## Scenarios {#section_mfy_mmx_wdb .section}

The Management Terminal can be used to:

-   Check the status of an ECS instance if it starts slowly.
-   Reconfigure the firewall if a remote connection fails because of any software error within the ECS instance.
-   End abnormal processes that consume excessive CPU usage or bandwidth.

**Note:** The Management Terminal can be used to connect to an instance even if no public IP address is assigned to your instance.

## Prerequisites {#section_u1y_rmx_wdb .section}

-   You have an ECS instance. For more information, see [Create an ECS instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).
-   You have set the logon password of the ECS instance. If not, use the [Reset Password](intl.en-US/User Guide/Instances/Reset an instance password.md#) feature to set a password.

## Procedure {#section_ary_smx_wdb .section}

The following figure illustrates how to use the Management Terminal to connect to an ECS instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9619/5162_en-US.png)

To connect to the ECS instance by using the Management Terminal, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  In the instance list, find your instance, and in the **Actions** column, click **Connect**.
5.  In the Management Terminal page, follow the instructions to connect to the Management Terminal:
    -   If you log on as an Alibaba Cloud account to connect to the Management Terminal for the first time, follow these steps:

        1.  In the VNC Connection Password dialog box, copy the password and click **Close**.

            **Note:** 

            -   The VNC password appears only once. You must save and secure password immediately for future use. If you need to change the VNC password, see [Change the VNC connection password](#password).
            -   If you log on as a RAM user to connect to the Management Terminal for the first time, you will not see this dialog box.
        2.  In the Enter VNC Password dialog box, paste the VNC connection password that you have copied, and click **OK**.
    -   If you log on as a RAM user to connect to the Management Terminal for the first time or in case you have forgotten your VNC connection password, follow these steps to connect to the Management Terminal:
        -   [Change the VNC connection password](#password).
        -   In the upper-left corner of the Management Terminal page, select **Send Remote Command** \> **Connect to Management Terminal**.
        -   In the Enter VNC Password dialog box, enter the new password and click **OK**.
    -   If this is not your first connection to the Management Terminal, enter the VNC connection password in the Enter VNC Password dialog box and click **OK**.
6.  To log on to the ECS instance, follow these steps according to the operating system:
    -   For a Linux instance: Enter the user name \(root\) and the logon password.

        **Note:** 

        -   If you forget the logon password of your instance, [reset the password](intl.en-US/User Guide/Instances/Reset an instance password.md#).
        -   The logon password input is invisible.
        -   If you want to do different operations within the instance, in the upper-left corner of the Management Terminal page, select **Send Remote Command** \> **CTRL + ALT + Fx**, of which **Fx** can be any key from **F1** to **F10**, to switch the interfaces for different operations.
        -   In case you see a black screen, the Linux instance may be in sleep mode. To exit sleep mode, click the mouse or press any key.
    -   For a Windows instance: In the upper-left corner of the Management Terminal page, select **Send Remote Command** \> **CTRL+ALT+DELETE**. The Windows logon interface is displayed. Enter the user name \(Administrator\) and the logon password.

        **Note:** If you forget the logon password of your instance, [reset the password](intl.en-US/User Guide/Instances/Reset an instance password.md#).


## Other Operations {#section_nmj_5mx_wdb .section}

**Change the VNC connection password**

If you forget the VNC connection password, follow these steps to change the password.

**Note:** If the instance that you are connecting to is not I/O optimized, you must restart your instance in the ECS console to apply new VNC password. The restart operation stops your instance and interrupts your business operations. Therefore, proceed with caution.

1.  Open the Management Terminal page.
2.  Close the VNC Connection Password dialog box or the Enter VNC Password dialog box.
3.  In the upper-right corner of the Management Terminal page, click **Modify Management Terminal Password**.
4.  Enter a new password, which must be six characters in length and may contain uppercase letters, lowercase letters, and digits. Special characters are not supported.
5.  A new password can be effective in the following events:
    -   For an I/O-optimized instance, the new password takes effect immediately.
    -   For a non-I/O-optimized instance, [restart the instance](intl.en-US/User Guide/Instances/Restart an instance.md#) in the ECS console.

        **Note:** Restarting the operating system does not apply the new password.


**Input commands**

If you are connecting to a Linux instance, use the **Input Commands** feature to type long text, such as a complex command or a URL.

Follow these steps:

1.  Open the Management Terminal page.
2.  In the upper-right corner of the Management Terminal page, click **Input Commands**.
3.  In the Copy Commands dialog box, enter the commands and click **OK**.
4.  Press the **Enter** key to run the commands.

## FAQ {#section_bty_xmx_wdb .section}

-   Can multiple users simultaneously connect to the Management Terminal?

    No. Only one user can connect to the Management Terminal at a time.

-    Why am I unable to connect to an instance by using the Management Terminal even after changing the password?

    Make sure that you enter the correct VNC password. If the instance that you are connecting to is not I/O optimized, you must restart the instance in the ECS console. This action helps the new VNC password to take effect.

-   Why do I see a black screen after logging on to my instance?

    A black screen indicates that the instance is in sleep mode.

    For a Linux instance, click mouse or press any key to activate the screen.

    For a Windows instance, click **Send remote command** \> **CTRL+ALT+DELETE** to view logon interface.

-   Why am I unable to access the Management Terminal?

    To resolve logon issues, open your browser and connect to the Management Terminal. Press **F12** to open the developer tool. The Management Terminal information can be analyzed to locate errors under the Console tab.

-   Can I use IE or Firefox to access the Management Terminal?

    You can access the Management Terminal only if you have IE10 or later versions installed. Only certain versions of Firefox are supported. You can resolve this issue by updating or changing your browser to a recommended version.

    **Note:** We recommend that you use Google Chrome because it offers the best support for the Management Terminal function.


