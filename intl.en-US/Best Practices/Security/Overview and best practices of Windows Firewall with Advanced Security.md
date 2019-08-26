# Overview and best practices of Windows Firewall with Advanced Security {#concept_b1w_sxr_gfb .concept}

This topic describes Windows Firewall with Advanced Security \(WFAS\), its application scenarios, and common operations.

## Overview {#section_sfs_3zr_gfb .section}

As an important part of the hierarchical security model, WFAS was launched after Windows NT6.0 by Microsoft. WFAS blocks unauthorized traffic that flows in or out of local computers by providing bi-directional filtering based on the current connection status. WFAS also uses Network Location Awareness \(NLA\) to apply the corresponding firewall profile to the computer based on its current connection status. The security rules of Windows Firewall and Internet Protocol Security \(IPsec\) are configured in the Microsoft Management Console \(MMC\) snap-in, and WFAS is also an important part of the network isolation policy.

## Application Scenario {#section_trz_jzr_gfb .section}

More and more O&M personnel are reporting that servers are attacked and passwords are cracked, which in most cases, are due to the “backdoor” left open to “intruders”. Intruders scan open ports on your computers and penetrate them through vulnerable ports, for example, the remote port 3389 in Windows and the remote port 22 in Linux. Now that we know where the problem is, we can take the effective countermeasure. Specifically, we can close these “backdoors” by modifying the default remote ports and restricting remote access. So how do we restrict remote access? Now let's demonstrate how to restrict the remote desktop connection by taking an ECS instance \(Windows Server 2008 R2\) for example.

## Procedure {#section_ifj_mzr_gfb .section}

1.  **View the Windows Firewall status** 

    Windows Firewall of the ECS instance is disabled by default. You can press **Win+R** to open the Run window, enter firewall.cpl, and then press **Enter** to open the Windows Firewall console, as shown below.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183712791_en-US.png)

    Enable or disable Windows Firewall.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183712792_en-US.png)

    As shown below, Windows Firewall is disabled by default.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183712793_en-US.png)

2.  **Enable Windows Firewall** 

    Enable Windows Firewall through the previous steps, as shown below.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183712794_en-US.png)

    Before enabling Windows Firewall, make sure the remote port is open in the inbound rules, or you cannot establish the remote connection even yourself. WFAS, however, opens RDP port 3389 in its inbound rules by default. Select Advanced settings.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812795_en-US.png)

    Select Inbound Rules. We can see that the Open RDP Port 3389 rule is enabled by default.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812796_en-US.png)

3.  **Configure WFAS** 

    Press Win+R to open the Run window, enter wf.msc, and then press Enter to open the WFAS window, as shown below.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812797_en-US.png)

    1.  **Create an inbound rule manually**

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812798_en-US.png)

        In the New Inbound Rule Wizard window, select Port and click Next.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812799_en-US.png)

        Select TCP and set Specific Local Ports to 3389.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812800_en-US.png)

        Click Next and select Allow the connection.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812801_en-US.png)

        Click Next and keep the default configurations.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812802_en-US.png)

        Click Next and enter the rule name \(for example, "RemoteDesktop"\), and click Finish.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9799/156013183812803_en-US.png)

        The new rule is shown in the Inbound Rule list.

        ![](images/12804_en-US_source.png)

        With the above steps, the remote port is added to WFAS, but access restriction is still not implemented. Let's implement it now.

    2.  **Configure the IP address scope** 

        Right-click the just created inbound rule, and select Properties in the context menu. In the displayed dialog box, click the Scope tab. Then add the remote IP addresses that can access this ECS instance. Note that once the IP address settings here are enabled, other IP addresses will be unable to access this ECS instance.

        ![](images/12805_en-US_source.png)

        Add remote IP addresses.

        ![](images/12806_en-US_source.png)

    3.  **Validate the IP address scope** 

        Let's add an IP address arbitrarily in the Remote IP address box and see what happens to the remote connection.

        ![](images/12807_en-US_source.png)

        The remote connection is down.

        ![](images/12808_en-US_source.png)

        If the remote connection is still up, we can just disable the Open RDP Port 3389 rule.

        ![](images/12809_en-US_source.png)

        If the remote connection is down, it means that the IP address scope has taken effect. However, we cannot connect to the ECS instance ourselves now. What should we do? We now can turn to the ECS console. Log on to the ECS console, and replace the remote IP address previously configured in the Scope tab with our own address \(enter the Internet address unless your work environment is connected to Alibaba Cloud\). You can connect to the ECS instance again now.

        Enter the ECS console, find the corresponding instance, and then connect to it.

        ![](images/12810_en-US_source.png)

        Log on to the ECS instance.

        ![](images/12811_en-US_source.png)

        Modify the remote IP address in the Scope tab of the RemoteDesktop rule in the same way. Specifically, replace 1.1.1.1 with our own IP address.

        ![](images/12812_en-US_source.png)

        Now we can connect to the ECS instance normally after adding our IP address. If you do not know your Internet address, you can [click here](http://ip.taobao.com/) to view it.

        ![](images/12813_en-US_source.png)

        The above steps implement remote access restriction on an ECS instance through WFAS. For other services and ports, restrictions can be implemented in the same way, for example, disabling ports 135, 137, 138, and 445 that are not used frequently, limiting access to FTP and related services, and more, thus maximizing the protection of ECS instances.


## Command line operations {#section_dcj_lns_gfb .section}

1.  Export the firewall configurations to a file.

    ``` {#codeblock_zc6_xu9_u4c}
    netsh advfirewall export c:\adv.pol
    ```

2.  Import the firewall configuration file to the system.

    ``` {#codeblock_i3o_7cq_zh7}
    netsh advfirewall import c:\adv.pol
    ```

3.  Restore the default firewall settings.

    ``` {#codeblock_g5i_6so_nsk}
    Netsh advfirewall reset
    ```

4.  Disable the firewall.

    ``` {#codeblock_4qi_ure_hbq}
    netsh advfirewall set allprofiles state off
    ```

5.  Enable the firewall.

    ``` {#codeblock_qxh_okq_1p0}
    netsh advfirewall set allprofiles state on
    ```

6.  Configure to block inbound traffic and allow outbound traffic by default in all configuration files.

    ``` {#codeblock_sq0_73u_hex}
    netsh advfirewall set allprofiles firewallpolicy blockinbound,allowoutbound
    ```

7.  Delete the rule named “ftp”.

    ``` {#codeblock_5ub_9u7_z07}
    netsh advfirewall firewall delete rule name=ftp
    ```

8.  Delete all inbound rules for local port 80.

    ``` {#codeblock_drz_zcv_glw}
    netsh advfirewall firewall delete rule name=all protocol=tcp localport=80
    ```

9.  Add the RemoteDesktop rule to allow port 3389.

    ``` {#codeblock_mio_gxu_oi5}
    netsh advfirewall firewall add rule name=RemoteDesktop (TCP-In-3389) protocol=TCP dir=in localport=3389 action=allow
    ```


