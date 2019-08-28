# Connect to a Windows instance by using the Management Terminal {#concept_frf_pkw_wgb .concept}

This topic describes how to connect to a Windows instance by using the Management Terminal \(also known as VNC\) in the ECS console and how to complete some related operations.

## Scenarios {#section_mfy_mmx_wdb .section}

You can access your Windows instance by using the Management terminal in the ECS console when other remote access software \(such as PuTTy, Xshell, or SecureCRT\) does not work properly.

The Management Terminal can be used to:

-   Check the status of your instance if it boots slowly \(for example, self-check upon startup\).
-   Reconfigure your instance \(for example, disable the firewall\) if a remote connection fails due to incorrect settings.
-   Terminate abnormal processes that consume excessive CPU or bandwidth.

## Prerequisites {#section_u1y_rmx_wdb .section}

-   An ECS instance is created.
-   The logon password for the ECS instance is set. If not, you can [reset the password](reseller.en-US/Instances/Manage instances/Reset an instance logon password.md#).

## Procedure {#section_ary_smx_wdb .section}

The following figure illustrates how to use the Management Terminal to connect to an ECS instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9619/15667883265162_en-US.png)

1.  Select the target region.
2.  In the instance list, find the target instance. Then, click **Connect** in the **Actions** column.
3.  Connect to the Management Terminal:
    -   If you connect to the Management Terminal with the master account for the first time, follow these steps:
        1.  In the VNC Connection Password dialog box, copy the password.

            **Note:** 

            -   The VNC password appears only once. You must save the password immediately and store it securely for future use.
            -   If you connect to the Management Terminal as a RAM user for the first time, you will not see this dialog box.
        2.  Click **Close**.
        3.  In the Enter VNC Password dialog box, paste the VNC connection password that you have copied, and click **OK** to connect to the **Management Terminal**.
    -   If you connect to the Management Terminal as a RAM user for the first time, or if you have forgotten your VNC connection password, follow these steps:
        1.  [Change the VNC connection password](#ol_r41_1nc_ydb).
        2.  In the upper left corner of the Management Terminal page, select **Send Remote Command** \> **Connect to Management Terminal**.
        3.  In the Enter VNC Password dialog box, enter the new password.
        4.  Click **OK** to connect to the Management Terminal.
    -   If you connect to the Management Terminal again as a RAM user or by using the master account, enter the password in the Enter VNC Password dialog box, and click **OK** to connect to the Management Terminal.
4.  Enter the user name and password to log on to the ECS instance.

    **Note:** In the upper left corner of the Management Terminal page, choose **Send Remote Command** \> **CTRL+ALT+DELETE** to enter the logon interface of your Windows instance.


## Change the VNC connection password {#section_nmj_5mx_wdb .section}

If you want a simple password or forget about your password, follow these steps to change the password:

**Note:** To connect to a non-I/O-optimized instance, you must restart your instance in the ECS console to activate the new VNC password. The restart operation stops your instance and interrupts your services. Therefore, proceed with caution.

1.  Open the Management Terminal page.
2.  Close the VNC Password or Enter VNC Password dialog box that displays.
3.  In the upper right corner of the Management Terminal page, click **Modify VNC Password**.
4.  In the Modify VNC Password dialog box that displays, enter a new password, and click **OK** to close the dialog box.
5.  Activate the new password:
    -   For an I/O-optimized instance, the new password takes effect immediately.
    -   For a non-I/O-optimized instance, [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console.

## Input commands {#section_f1z_2qk_pgb .section}

To connect to a Windows instance, you can use the **Input Commands** function to enter long texts, such as a complex command or a URL.

1.  Open the Management Terminal page.
2.  In the upper right corner of the Management Terminal page, click **Input Commands**.
3.  In the Input Commands dialog box that displays, enter a command, and click **OK** to copy the command to the command line interface of your Windows instance.

## References {#section_kj2_zmx_wdb .section}

-   If you are using a PC, following instructions in [Connect to a Windows instance](reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
-   If you are using a mobile device, following instructions in [Connect to a Windows instance on a mobile device](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance on a mobile device.md#).

