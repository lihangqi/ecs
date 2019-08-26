# Change the instance logon password by connecting to the instance {#concept_tkx_nxw_wgb .concept}

This topic describes how to change the logon password of an ECS instance by connecting to the instance through a remote connection. In this topic, a Linux instance running CentOS 6.8 and a Windows instance running Windows Server 2008 are used as examples.

## Change the logon password of a Linux instance {#section_yth_xd2_qgb .section}

1.  Log on to the target instance by using a remote connection. For information about the different methods you can use to remotely connect to a Linux instance, see [Overview](intl.en-US/Instances/Connect to instances/Overview.md#).
2.  Run the passwd command \(for example, passwd root\).
3.  Enter a new password.
4.  Enter the new password again for the password to take effect.
5.  Restart the instance in the ECS console or by calling the related API for the new password to take effect.

## Change the logon password of a Windows instance {#section_afp_xd2_qgb .section}

1.  Log on to the target instance by using a remote connection. For information about the different methods you can use to remotely connect to a Windows instance, see [Overview](intl.en-US/Instances/Connect to instances/Overview.md#).
2.  Choose **Start** \> **Run**, enter compmgmt.msc, and then press **Enter**.
3.  In the Computer Management tool window, choose **System Tools** \> **Local Users and Groups** \> **Users**.
4.  Right-click the username for which the password is to be changed \(for example, Administrator\).
5.  Click **Set Password**.
6.  In the Set Password for Administrator dialog box, click **Proceed**.
7.  In the displayed dialog box, enter a new password in the **New password** and **Confirm password** text boxes, and then click **OK** .
8.  Restart the instance in the ECS console or by calling the related API for the new password to take effect.

