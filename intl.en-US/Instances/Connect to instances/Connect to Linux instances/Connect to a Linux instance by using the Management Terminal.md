# Connect to a Linux instance by using the Management Terminal {#concept_sdk_1jx_wdb .concept}

This topic describes how to connect to a Linux ECS instance by using the Management Terminal \(also known as VNC\) in the ECS console and how to complete some related operations.

## Scenarios {#section_mfy_mmx_wdb .section}

You can access your Linux instance by using the Management terminal in the ECS console when other remote access software \(such as PuTTy, Xshell, or SecureCRT\) does not work properly

The Management Terminal can be used to:

-   Check the status of your instance if it boots slowly \(for example, self-check upon startup\).
-   Reconfigure your instance \(for example, disable the firewall\) if a remote connection fails due to incorrect settings.
-   Terminate abnormal processes that consume excessive CPU or bandwidth.

**Note:** The Management Terminal can be used to connect to an instance even if no public IP address is assigned to your instance.

## Prerequisites {#section_u1y_rmx_wdb .section}

-   An ECS instance is created.
-   The logon password for the ECS instance is set. If not, you can [reset the password](reseller.en-US/Instances/Manage instances/Reset an instance logon password.md#).

## Procedure {#section_ary_smx_wdb .section}

The following figure illustrates how to use the Management Terminal to connect to an ECS instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9619/15667884085162_en-US.png)

To connect to the ECS instance by using the Management Terminal, follow these steps:

1.  In the instance list, find your instance and then, in the **Actions** column, click **Connect**.
2.  In the Management Terminal page, follow the instructions to connect to the Management Terminal:
    -   If you log on as an Alibaba Cloud account to connect to the Management Terminal for the first time, follow these steps:

        1.  In the VNC Connection Password dialog box, copy the password and click **Close**.

            **Note:** 

            -   The VNC password appears only once. You must save the password immediately and store it securely for future use. If you need to change the VNC password, see [change the VNC connection password](#).
            -   If you log on as a RAM user to connect to the Management Terminal for the first time, you will not see this dialog box.
        2.  In the Enter VNC Password dialog box, paste the VNC connection password that you have copied, and click **OK**.
    -   If you log on as a RAM user to connect to the Management Terminal for the first time, or if you have forgotten your VNC connection password, follow these steps:
        -   [Change the VNC connection password](#).
        -   In the upper-left corner of the Management Terminal page, select **Send Remote Command** \> **Connect to Management Terminal**.
        -   In the Enter VNC Password dialog box, enter the new password and click **OK**.
    -   If this is not your first connection to the Management Terminal, enter the VNC connection password in the Enter VNC Password dialog box and click **OK**.
3.  To log on to the ECS instance, follow these steps according to the operating system:
    -   For a Linux instance: Enter the user name \(root\) and the logon password.

        **Note:** 

        -   The logon password input is invisible.
        -   If you want to perform additional operations within the instance, in the upper-left corner of the Management Terminal page, choose **Send Remote Command** \> **CTRL + ALT + Fx**, of which **Fx** can be any key from **F1** to **F10**, to switch the interfaces for different operations.
        -   If a black screen prompts, the Linux instance may be in sleep mode. To exit sleep mode, click your mouse or press any key.

## Change the VNC connection password {#section_v18_hcp_u3t .section}

If you want a simple password or forget about your password, follow these steps to change the password:

**Note:** To connect to a non-I/O-optimized instance, you must restart your instance in the ECS console to activate the new VNC password. The restart operation stops your instance and interrupts your services. Therefore, proceed with caution.

1.  Open the Management Terminal page.
2.  Close the VNC Password or Enter VNC Password dialog box that displays.
3.  In the upper right corner of the Management Terminal page, click **Modify VNC Password**.
4.  In the Modify VNC Password dialog box that displays, enter a new password, and click **OK** to close the dialog box.
5.  Activate the new password:
    -   For an I/O-optimized instance, the new password takes effect immediately.
    -   For a non-I/O-optimized instance, [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console.

## Input commands {#section_228_kmr_5b4 .section}

To connect to a Linux instance, you can use the **Input Commands** function to enter long texts, such as a complex command or a URL.

1.  Open the Management Terminal page.
2.  In the upper right corner of the Management Terminal page, click **Input Commands**.
3.  In the Input Commands dialog box that displays, enter a command, and click **OK** to copy the command to the command line interface of your Linux instance.

## References {#section_08u_wmj_2sj .section}

-   If you are using a PC, following instructions in
    -   [Connect to a Linux instance by using an SSH key pair](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md#).
    -   [Connect to a Linux instance by using a password](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md#).
-   If you are using a mobile device, following instructions in [Connect to an instance on a mobile device](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance on a mobile device.md#).

