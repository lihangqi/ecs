# Connect to a Linux instance by using an SSH key pair {#concept_ucj_wrx_wdb .concept}

This topic describes how to use an SSH key pair to log on to a Linux instance in the Windows and Linux operating systems.

## Prerequisites {#section_ypf_hh0_dfg .section}

Before you use an SSH key pair to connect to your Linux instance, the following conditions must be met:

-   An SSH key pair is created in the ECS console and the .pem private key file is downloaded. For more information, see [Create an SSH key pair](../reseller.en-US/Security/Key pairs/Use an SSH key pair.md#).
-   An SSH key pair is linked with a Linux instance. You can [allocate a key pair when creating an ECS instance](../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) or [attach an SSH key pair](../reseller.en-US/Security/Key pairs/Use an SSH key pair.md#section_d4l_ql1_ydb) to an existing instance.

    **Note:** If an ECS instance is in the **Running** state, you must restart it in the ECS console or by using the API to activate the key pair after attaching it to the instance.

-   Security group rules are added to the security groups to which the instance belongs. For more information, see [Add security group rules](../reseller.en-US/Security/Security groups/Add security group rules.md#). The following table describes the security group rules.

    |Network type|NIC type|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |------------|--------|--------------|--------------------|-------------|----------|------------------|--------------------|--------|
    |VPC|Not required|Inbound|Allow|SSH \(22\)|22/22|IP address segment–based access|0.0.0.0/0|1|
    |Classic network|Internet|


## Local Windows OS {#windows .section}

A private key file in .pem format is automatically generated after you create an SSH key pair in the ECS console. This section describes how to use PuTTYgen to convert the .pem private key file and how to use PuTTY to log on to a Linux instance through the SSH remote access tool on a Windows OS.

1.  Download and install PuTTYgen and PuTTY.

    The download links are as follows:

    -   [PuTTYgen](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
    -   [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
2.  Convert the .pem private key file to a .ppk key file.
    1.  Start PuTTYgen.

        PuTTYgen 0.71 is used as an example.

    2.  In the **Parameters** area, set **Type of key to generate** to **RSA** and then click **Load**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156678623251179_en-US.png)

    3.  Select **All Files \(\*.\*\)** from the drop-down list.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15667862335188_en-US.png)

    4.  Select the **.pem** private key file to be converted.
    5.  In the **PuTTYgen Notice** dialog box, click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156678623351191_en-US.png)

    6.  Click **Save private key**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156678623451197_en-US.png)

    7.  In the PuTTYgen Warning dialog box, click **Yes**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15667862345190_en-US.png)

    8.  Specify the name of the .ppk file and click **Save**.
3.  Start PuTTY.
4.  Configure the private file used for authorization.

    1.  In the left-side navigation pane, choose **Connection** \> **SSH** \> **Auth**.
    2.  In the right pane, click **Browse…**.
    3.  Select the .ppk private key file.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15667862355191_en-US.png)

5.  Configure information required for connecting to the Linux instance.

    1.  In the left-side navigation pane, click **Session**.
    2.  In the right pane, enter your account and the Internet IP address of the instance to be connected in the Host Name \(or IP address\) text box. The format is root@IP address.
    3.  In the Port text box, enter the port number 22.
    4.  Set **Connection type** to **SSH**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15667862355192_en-US.png)

6.  Click **Open** to start connecting to your Linux instance.

When the following message is displayed, you have successfully logged on to the instance by using the SSH key pair.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156678623651203_en-US.png)

## Local Linux OS or other OSs supporting SSH commands {#linux .section}

This section describes how to use an SSH key pair to log on to a Linux instance on a Linux OS or an OS supporting SSH commands, for example, Windows MobaXterm.

-   Configure required information and connect to the Linux instance by using commands.
    1.  Find the directory for saving the .pem private key file on your PC, for example, /root/mysshkey.pem.
    2.  Run the following command to modify the attribute of the private key file:

        ``` {#codeblock_vq9_t7g_5ba}
        chmod 400 [Directory for saving the .pem private key file on your local PC]
        ```

        For example,

        ``` {#codeblock_p0d_6r3_xgb}
        chmod 400 /root/mysshkey.pem
        ```

    3.  Run the following command to connect to the instance:

        ``` {#codeblock_62m_y4k_mmd}
        ssh -i [Directory for saving the .pem private key file on your local PC] root@[Internet IP address]
        ```

        For example,

        ``` {#codeblock_6c1_4qp_e2j}
        ssh -i /root/mysshkey.pem root@10.10.xx.xxx
        ```

-   Configure required information by using the config file and connect to the instance by running commands.
    1.  Go to the ssh directory in the root directory and do the following to modify the config file:

        ``` {#codeblock_u1v_gdy_p5r}
        Host ecs    // Set the name of your ECS instance.
        HostName 192. *. *. * // Enter the Internet IP address of your ECS instance.
        Port 22   / Enter the port number, which is 22 by default.
        User Root // Enter your logon account.
        IdentityFile ~/.ssh/ecs.pem // Enter the directory for saving the .pem private key file on your PC.
        ```

    2.  Save the config file
    3.  Restart SSH.
    4.  Run `ssh [ECS name]` to connect to your ECS instance, for example, `ssh ecs`.

## References {#section_osu_bqu_a33 .section}

For information about how to connect to a Linux instance, see [Connect to a Linux instance by using a password](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md#) and [Connect to an instance by using the Management Terminal](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#).

