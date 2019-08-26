# Build an FTP site on a Windows ECS instance {#concept_kmr_213_ffb .concept}

This article describes how to build an FTP site on a Windows ECS instance. This method is applicable to Windows Server 2008 and later versions. In this article, Windows Server 2008 R2 is used.

The procedure for building an FTP site on a Windows ECS instance is as follows:

-   Step 1. Add IIS and FTP service roles
-   Step 2. Create FTP user name and password
-   Step 3. Set permissions for shared files
-   Step 4. Add and configure an FTP site
-   Step 5. Configure a security group and firewall
-   Step 6. Test

## Step 1. Add IIS and FTP service roles {#section_dgv_q13_ffb .section}

You must install IIS and FTP services before building an FTP site.

1.  [Connect to a Windows instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  Click **Start** \> **All Programs** \> **Administrative Tools** \> **Server Manager**.
3.  In the left-side navigation pane, click **Roles**, and then click **Add Roles**.
4.  In the dialog box, click **Next**.
5.  Select **Web Server \(IIS\)**, and then click **Next**.
6.  Select **IIS Management Console** and **FTP Server**, click **Next**, and then click **Install**.

## Step 2. Create FTP user name and password {#section_g5d_z13_ffb .section}

If you want to allow anonymous users to access the FTP, skip this step.

1.  Click **Start** \> **Administrative Tools** \> **Server Manager**.
2.  Click **Configuration** \> **Local Users and Groups** \> **Users**, right click the blank space, and select **New User**. In the **New User** dialog box, type the new user information. For example, ftptest is used in this article.

    **Note:** The password must contain a mixture of upper-case letters, lower-case letters, and numbers. Otherwise, the password is invalid.


## Step 3. Set permissions for shared files {#section_mvf_kc3_ffb .section}

You must set permissions to read, write, or execute for folders shared to users on the FTP site.

1.  Create a folder for the FTP site, right click the folder, and then select **Properties**.
2.  Click **Security**, select **Users**, and then click **Edit**.
3.  Edit **Permissions for Users**. In this example, we grant **all permissions**.

## Step 4. Add and configure an FTP site {#section_xf1_pc3_ffb .section}

Follow these steps to install an FTP site:

1.  Click **Start** \> **All Programs** \> **Administrative Tools** \> **Internet Information Services \(IIS\) Manager**.
2.  In the left-side navigation pane, click the instance ID, right click **Sites**, and then click **Add FTP Site**.
3.  In the dialog box, specify the FTP site name and the physical path of the shared folder, and then click **Next**.
4.  Use the **default value** for the IP address, and then type the port number of this instance. The default FTP port number is 21.
5.  Select SSL settings.
    -   **Allow SSL**: Allows the FTP site to support both non-SSL and SSL connections with the client.
    -   **Require SSL**: Requires SSL encryption for communication between the FTP server and the client.
    -   **No SSL**: If No SSL encryption is required, select **No SSL**.
6.  Select one or more authentication methods.
    -   **Anonymous**: Allows any user to access the shared content, by entering the user name **anonymous** or **ftp**.
    -   **Basic**: Requires users to enter the valid user name and password before they can access the shared content. The basic authentication method transmits the unencrypted password through the network. Therefore, use this authentication method only when you are sure that the connection between the client and the FTP server is secure, for example, when SSL is used.
7.  Select one of the following options from the **Authorization** list, and set permissions:
    -   **All users**: All users \(both anonymous and identified users\) can access the relevant content.
    -   **Anonymous users**: Anonymous users can access the relevant content.
    -   **Specified roles or user groups**: Only members of the specific role group or user group can access the relevant content. Enter the role group or user group in the corresponding field.
    -   **Specified users**: Only the specified users can access the relevant content. Enter the user name in the corresponding field.
8.  Select **read** and **write** permissions for the authorized users. Click **Finish**

.

## Step 5. Configure a security group and firewall {#section_jk1_3d3_ffb .section}

After building the FTP site, you must add a rule in the security group to allow inbound traffic on the FTP port. For more information, see [add a security group rule](https://www.alibabacloud.com/help/doc-detail/25471.htm).

By default, TCP port 21 is open on the server firewall by default for the FTP service. If you have entered another port number, you must add an inbound rule to open this port on the firewall.

## Step 6. Test { .section}

On your **local computer**, access the FTP site by using `ftp://IP address:FTP port` \(the default port 21 is used if you do not enter the port\). For example, you can enter `ftp://0.0.0.0:20`. You are prompted for your user name and password if the configuration was successful. After entering the user name and password correctly, you can perform the relevant FTP file operations according to your permissions.

**Note:** If you use this method to access the FTP site from the client, you must adjust the Internet Explorer settings to open FTP folders. Open Internet Explorer, and then select **Tools** \> **Internet Options** \> **Advanced**. Select **Enable folder view for FTP sites**, and then clear **Use Passive FTP**.

## What to do next {#section_cdm_rd3_ffb .section}

You can take actions to [improve your FTP service security](https://www.alibabacloud.com/help/faq-detail/37452.htm).

For more information, see [FTP anonymous logon and weak password vulnerabilities](https://www.alibabacloud.com/help/doc-detail/32190.htm?spm=a2c63.p38356.a3.12.5b52b4bdYbjKBN) .

