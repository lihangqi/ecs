# Build an FTP site on a Linux ECS instance {#concept_ww3_123_ffb .concept}

vsftpd is a light, safe, and easy-to-use FTP server for Linux. It is the most popular FTP server across all Linux versions. This article describes how to install vsftpd on a Linux ECS instance running CentOS 7.2 x64. This article describes how to install vsftpd on a Linux ECS instance running CentOS 7.2 x64.

To build an FTP site on a Linux ECS instance, follow these steps:

-   Step 1. Install vsftpd
-   Step 2. Configure vsftpd
-   Step 3. Configure a security group
-   Step 4. Test

## Step 1. Install vsftpd {#section_d55_c23_ffb .section}

1.  [Connect to a Linux instance by using a password](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the following command to install vsftpd.

    ```
    yum install -y vsftpd
    ```

    Run the following command

3.  to open and view `etc/vsftpd`.

    ```
    cd /etc/vsftpd
    ls
    ```

    **Note:** 

    -   `/etc/vsftpd/vsftpd.conf` is the core configuration file.
    -   `/etc/vsftpd/ftpusers` is the blacklist. Users on the blacklist are prevented from accessing the FTP server.
    -   `/etc/vsftpd/user_list` is the whitelist. Only the users on the whitelist are allowed to access the FTP server.
4.  Run the following command to set vsftpd to automatically start on startup.

    ```
    systemctl enable vsftpd.service
    ```

5.  Run the following command to start the FTP service.

    ```
    systemctl start vsftpd.service
    ```

6.  Run the following command to view the FTP service port.

    ```
    netstat -antup | grep ftp
    ```


## Step 2. Configure vsftpd {#section_wpy_x23_ffb .section}

After vsftpd is installed, the anonymous FTP function is enabled by default. Using the anonymous FTP function, users can log on to the FTP server without the user name and password, but do not have the permission to modify or upload files.

This section describes the following vsftpd configuration methods and the corresponding parameter descriptions for your reference.

-   Grant the file upload permission to anonymous users
-   Configure local user logon
-   Introduction to vsftpd.conf parameters

**Grant the file upload permission to anonymous users**

You can grant more permissions to anonymous users by modifying the options in the `vsftpd.conf` configuration file.

1.  Follow these steps to modify `/etc/vsftpd/vsftpd.conf`:
    1.  Run `vim /etc/vsftpd/vsftpd.conf`.
    2.  Press the **i** key to enter Edit mode.
    3.  Set `write_enable=YES`.
    4.  Set `anon_upload_enable=YES`.
    5.  Press the **Esc** key and then type `:wq` to save and close the file.
2.  Run the following command to change the permissions of the `/var/ftp/pub` directory, grant write permissions to the FTP users, and reload the configuration file.

    ```
    chmod o+w /var/ftp/pub/systemctl restart vsftpd.service
    ```


**Configure local user logon**

Local user logon refers to a user logging on to the FTP server by using the user name and password for the Linux operation system.

After vsftpd is installed, only anonymous FTP logon is supported. If you attempt to log on to the FTP server with the Linux user name, your access to vsftp will be denied. However, you can adjust the vsftpd configuration to allow logon with a user name and password. Follow these steps:

1.  Run the following command to create the ftptest user.

    ```
    useradd ftptest
    ```

2.  Run the following command to modify the password for the ftptest user.

    ```
    passwd ftptest
    ```

3.  Follow these steps to modify`/etc/vsftpd/vsftpd.conf`:
    1.  Run `vim /etc/vsftpd/vsftpd.conf`.
    2.  Press the **i** key to enter edit mode.
    3.  Set `anonymous enable=NO`.
    4.  Set `local_enable=YES`.
    5.  Press the **Esc** key and then type `:wq` to save and close the file.
4.  Run the following command to reload the configuration file.

    ```
    systemctl restart vsftpd.service
    ```


**Introduction to vsftpd.conf parameters**

Run `cat /etc/vsftpd/vsftpd.conf` to view content in the configuration file.

The following table lists all the parameters related to user logon control.

|Parameter|Description|
|:--------|:----------|
|anonymous\_enable=YES|Allows anonymous logon.|
|no\_anon\_password=YES|Anonymous users are not prompted for a password when logging on.|
|anon\_root=\(none\)|Root directory for anonymous users.|
|local\_enable=YES|Allows local user logon.|
|local\_root=\(none\)|Root directory for local user.|

The following table lists all the parameters related to user permission control.

|Parameter|Description|
|:--------|:----------|
|write\_enable=YES|Allows file upload \(global control\).|
|local\_umask=022|Umask for the local user to upload files.|
|file\_open\_mode=0666|Uses umask for file upload permission.|
|anon\_upload\_enable=NO|Allows anonymous users to upload files.|
|anon\_mkdir\_write\_enable=NO|Allows anonymous users to create directories.|
|anon\_other\_write\_enable=NO|Allows anonymous users to modify and delete files and directories.|
|chown\_username=lightwiter|Anonymous Upload File belongs User Name.|

## User name for anonymously uploaded files {#section_unb_wf3_ffb .section}

After building the FTP site, you must add a rule to open the FTP port. For more information, see [add a security group rule](../../../../reseller.en-US/User Guide/Security groups/Add security group rules.md#).

## Step 4. Test {#section_cn2_xf3_ffb .section}

On your **local computer**, access the FTP site by using `ftp://public IP address:FTP port` \(the default port 21 is used if you do not enter the port\). For example, `ftp://0.0.0.0:20`. You are prompted for your user name and password if the configuration was successful. After entering the user name and password correctly, you can perform the relevant FTP file operations according to your permissions.

**Note:** If you use this method to access the FTP site from the client, you must adjust the Internet Explorer settings to open FTP folders. Open Internet Explorer, and then select **Tools** \> **Internet Options** \> **Advanced**. Select **Enable folder view for FTP sites**, and then clear **Use Passive FTP**.

## What to do next {#section_lxz_dg3_ffb .section}

You can take actions to improve your FTP service security. For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/faq-detail/37452.htm).

