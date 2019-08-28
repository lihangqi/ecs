# Create a new account with the root user privilege {#concept_52012_zh .concept}

This topic describes how to use a user-defined script to create a new account with the root user privilege when creating a Linux instance. User-defined scripts can also be used to create a new account with the administrator privilege for a Windows instance.

## Scenarios {#section_mfk_fbm_2fb .section}

Use user-defined scripts of instances if you want to achieve the following results when creating a Linux ECS instance:

-   Disable the default root account that comes with a Linux ECS instance. You can use the script to customize how to disable the root user and how many root user privileges are disabled.
-   Create a new account with the root user privilege and customize the account name.
-   Use only SSH key pairs, but not user passwords, for remote logon to manage the instance by using the new account with the root user privilege.
-   If this new account is required to perform operations that can only be done by a user with root user privilege, the `sudo` command can be used without a password for privilege escalation.

## Procedure {#section_n32_hbm_2fb .section}

To create a new account with the root user privilege, follow these steps:

1.  Create an instance by referring to [Create an instance by using the wizard](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). Be aware of the following configuration items:
    -   On the Basic Configurations page, note the following customized configurations:
        -   **Instance Type**: Select an I/O-optimized instance.
        -   **Image**: Select a supported image type, for example, CentOS 7.2 on the **Public Image** tab.
2.  On the **Networking** page, set **Network Type** to VPC
3.  On the System Configurations page, enter the following script in the **User Data** text box in the **Advanced** area:

    ``` {#codeblock_ha8_evu_ei2 .language-shell}
    #! /bin/sh
    useradd test
    echo "test   ALL=(ALL)        NOPASSWD:ALL" | tee -a /etc/sudoers
    mkdir /home/test/.ssh
    touch /home/test/.ssh/authorized_keys
    echo "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAhGqhEh/rGbIMCGItFVtYpsXPQrCaunGJKZVIWtINrGZwusLc290qDZ93KCeb8o6X1Iby1Wm+psZY8THE+/BsXq0M0HzfkQZD2vXuhRb4xi1z98JHskX+0jnbjqYGY+Brgai9BvKDXTTSyJtCYUnEKxvcK+d1ZwxbNuk2QZ0ryHESDbSaczlNFgFQEDxhCrvko+zWLjTVnomVUDhdMP2g6fZ0tgFVwkJFV0bE7oob3NOVcrx2TyhfcAjA4M2/Ry7U2MFADDC+EVkpoVDm0SOT/hYJgaVM1xMDlSeE7kzX7yZbJLR1XAWV1xzZkNclY5w1kPnW8qMYuSwhpXzt4gsF0w== rsa-key-20170217" | tee -a /home/test/.ssh/authorized_keys
    					
    ```

    **Note:** 

    -   The first line must be `#!. /bin/sh`, with no leading space.
    -   Do not enter unnecessary spaces or carriage return characters in the text.
    -   The last line is your public key. You can define it.
    -   You can add other configuration in the script as you need.
    -   The example script only applies to CentOS 7.2. If you are using other images, customize the script according to the operating system types.

After the instance is started, you can use the new **test** user to connect to the instance by using an SSH private key. You can also escalate the permission level by using the `sudo` command and run operations that require the root user privilege, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9824/156678802912173_en-US.png)

