# Manage Windows Server Semi-Annual Channel images and instances {#concept_ycn_j51_hhb .concept}

This topic describes the various methods you can use to manage an Alibaba Cloud ECS instance created from a Windows Server Semi-Annual Channel image.

## Image overview {#section_jx1_xv1_hhb .section}

ECS now supports Windows Server Semi-Annual Channel images. When creating an instance, you can find the Version 1809 Datacenter image in the list of Windows Server public images. Windows Server Semi-Annual Channel images are operating system images running in pure Server Core mode and do not provide a graphical user interface. Windows Server Semi-Annual Channel images have much looser requirements for hardware, thus reducing the update frequency and supporting remote management. Alibaba Cloud ECS currently supports the following Windows Server Semi-Annual Channel versions:

-   Windows Server 1809 Datacenter edition
-   Windows Server 1709 Datacenter edition

## Instance management tools {#section_s5z_qyn_hhb .section}

Instances that run Windows Server Semi-Annual Channel are not provided with the resource manager or control panel functions, or Windows Explorer, and do not support any .msc features \(such as devmgmt.msc\). However, you can manage Windows Server Semi-Annual Channel instances by using such tools as Sconfig, Server Manager, PowerShell, and Windows Admin Center.

Additionally, Windows Server Semi-Annual Channel instances run in Server Core mode. In this case, we recommend that you use PowerShell and Windows Admin Center to manage your instances. Procedures for the preceding management tools are provided in the following sections For more information, see [Manage a Server Core server](https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-manage).

## PowerShell {#section_et5_g14_hhb .section}

In the following example, assume that the public IP address of your instance is 172.16.1XX.183. To implement PowerShell for remote management, follow these steps:

1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Enter `PowerShell` in the command line of the target instance.
3.  Run the following command in PowerShell:

    ```
    Enable-PSRemoting -Force
    Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
    ```

4.  Add a rule to the security group of the target instance to allow access to the HTTP port 5985 and the HTTPS port 5986. For more information, see [Add security group rules](../../../../reseller.en-US/Security/Security groups/Add security group rules.md#).
5.  Enter `PowerShell` in the command line of your client.
6.  Run the following command in PowerShell:

    ```
    Set-Item WSMan:localhost\client\trustedhosts -value 172.16.1XX.183 -Force
    ```

    **Note:** 172.16.1XX.183 indicates that only your instance is trusted. You can also use `*` to indicate that all computers are trusted.

7.  Run `Enter-PSSession '172.16.1XX.183' -Credential:'administrator'` in PowerShell and enter the instance password as prompted.

Now you can manage your Windows instance on your client computer.

## Windows Admin Center {#section_y2t_3d4_hhb .section}

In the following examples, assume that the public IP address of your instance is 172.16.1XX.183. You can install Windows Admin Center either by using the command line or by downloading the installation package from the official website.

-   **Install Windows Admin Center through the command line** 
    1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
    2.  Add a rule to the security group of the target instance to allow access to the HTTP 5985 and the HTTPS port 5986. For more information, see [Add security group rules](../../../../reseller.en-US/Security/Security groups/Add security group rules.md#).
    3.  Enter `PowerShell` in the command line of the target instance.
    4.  Run the following command in PowerShell:

        ```
        Enable-PSRemoting -Force
        Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
        ```

    5.  Run the following command to download Windows Admin Center.

        ```
        wget -Uri http://download.microsoft.com/download/E/8/A/E8A26016-25A4-49EE-8200-E4BCBF292C4A/HonoluluTechnicalPreview1802.msi -UseBasicParsing -OutFile c:\HonoluluTechnicalPreview1802.msi
        msiexec /i c:\HonoluluTechnicalPreview1802.msi /qn /L*v log.txt SME_PORT=443 SSL_CERTIFICATE_OPTION=generate
        ```

    6.  Run the `cat log.txt` command to check the download progress. When the following information appears in the log file, Windows Admin Center is installed.

        ```
        MSI (s) (14:44) [09:48:37:885]: Product: Project 'Honolulu'(technical preview) -- Installation completed successfully. 
        MSI (s) (14:44) [09:48:37:885]: Windows Installer has installed this product. Product name: Project 'Honolulu'(technical preview). Product version: 1.1.10326.0. Language: 1033. Producer: Microsoft Corporation. Installation success or error status: 0.
        ```

-   **Download and install Windows Admin Center through a browser** 

    **Prerequisites**

    Make sure that you are using a browser in the target client where Windows Admin Center is to be downloaded. PowerShell is configured. For more information, see [PowerShell remote management](#section_et5_g14_hhb).

    **Procedure**

    1.  [Download](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) and install Windows Admin Center.
    2.  Open [https://localhost/](https://localhost/?spm=a2c4g.11186623.2.32.3da666b5wlBkBq).
    3.  Click **Add** to add the instance IP address in the displayed window.
    Now you can manage your instance through Microsoft Edge or Chrome from the client computer of Windows Admin Center.


## FAQ {#section_lpv_hg4_hhb .section}

**How do I copy files to a Windows Server Semi-Annual Channel instance?**

You can use RDP applications, PowerShell, or the Windows Admin Center to copy files from a client to a Windows Server Semi-Annual Channel instance.

-   Through RDP applications
    1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
    2.  On the client, copy the target files.
    3.  In the CMD utility of your instance, enter `notepad`.
    4.  Click **File** \> **Open**. In the displayed window, select the destination directory for the files, then right-click and choose **Paste**.
-   Through PowerShell
    1.  Start the target instance.
    2.  Open the CMD utility on the client, and enter `PowerShell`.
    3.  Access the target instance remotely through PowerShell. For more information, see [PowerShell remote management](#section_et5_g14_hhb).
    4.  Run the following command on the client:

        ```
        $session = New-PSSession -ComputerName 172.16.1XX.183
        Copy-Item -ToSession $session -Path C:\1.txt -Destination c:\2.txt
        ```

        **Note:** C:\\1.txt is the source file directory on the client computer, while C:\\2.txt is the target file directory on the Windows instance.

-   Through Windows Admin Center
    1.  Start the target instance.
    2.  Configure Windows Admin Center. For more information, see [Windows Admin Center](#section_y2t_3d4_hhb).
    3.  Open Windows Admin Center, and click the managed instance.
    4.  Click **File**, select the target files and then click **Upload**.

**How do I shut down or restart a Windows Server Semi-Annual Channel instance in the instance itself?**

-   Through RDP applications
    1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
    2.  In the CMD utility, enter `sconfig`. Then, enter `13` to restart your instance or `14` to shut it down, and press Enter.
-   Through PowerShell
    1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
    2.  In the CMD utility, enter `PowerShell`.
    3.  Enter one of the following commands to restart or shut down your instance:

        ```
        shutdown -r -t 00 :: # Restart your instance in 0 seconds through the command-line command
        shutdown -s -t 00 :: # Shut down your instance in 0 seconds through the command-line command
        Stop-Computer -Force # Shut down your instance immediately through the Powershell command
        Restart-Computer -Force # Restart your instance immediately through the Powershell command
        ```

-   Through PowerShell remote management
    1.  Start the target instance.
    2.  Open the CMD utility on the client, and enter `PowerShell`.
    3.  Access the target instance remotely through PowerShell. For more information, see [PowerShell remote management](#section_et5_g14_hhb).
    4.  Enter one of the following commands on the client:

        ```
        Enter-PsSession –ComputerName 172.16.1XX.183
        Restart-Computer -Force #Restart
        Stop-Computer -Force #Shut down
        ```

-   Through Windows Admin Center
    1.  Start the target instance.
    2.  Configure Windows Admin Center. For more information, see [Windows Admin Center](#section_y2t_3d4_hhb).
    3.  Open Windows Admin Center, and click the managed instance. Then, click **Overview**, and select **Restart** or **Shut down**.

**How do I install the IIS service?**

-   Through RDP applications

    1.  Connect to the target instance. For more information, see [Connect to a Windows instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
    2.  In the CMD utility, enter `PowerShell`.
    3.  Run the following command to install IIS:

        ```
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   Through PowerShell remote management

    1.  Start the target instance.
    2.  Open the CMD utility on the client, and enter `PowerShell`.
    3.  Access the target instance remotely through PowerShell. For more information, see [PowerShell remote management](#section_et5_g14_hhb).
    4.  Run the following command on the client:

        ```
        Enter-PsSession –ComputerName 172.16.1XX.183
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   Through Windows Admin Center

    1.  Start the target instance.
    2.  Configure Windows Admin Center. For more information, see [Windows Admin Center](#section_y2t_3d4_hhb).
    3.  Open Windows Admin Center, and click the managed instance. Click **Roles and Features** and **Web Server** in sequence, select the desired function, and click **Yes**.

**How do I re-open a command line window that was accidentally closed in an RDP session?**

To re-open a command line window, follow these steps:

1.  Press Ctrl + Alt + End. If the preceding combination does not work, press Ctrl + Alt + Del.
2.  In the interface that appears, select **Task Manager** and press Enter.
3.  Click **File** \> **New Task**, enter cmd, and click **OK**.

## References {#section_hcy_qw4_hhb .section}

-   [Windows Server Semi-Annual Channel overview](https://docs.microsoft.com/zh-cn/windows-server/get-started/semi-annual-channel-overview).
-   [Introducing Windows Server, version 1709](https://docs.microsoft.com/en-us/windows-server/get-started/get-started-with-1709?spm=a2c4g.11186623.2.54.3da666b5wlBkBq)

-   [Windows Admin Center](https://docs.microsoft.com/en-us/windows-server/manage/honolulu/honolulu?spm=a2c4g.11186623.2.55.3da666b5wlBkBq)

-   [About Remote Troubleshooting](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_troubleshooting?spm=a2c4g.11186623.2.56.3da666b5wlBkBq&view=powershell-6)


