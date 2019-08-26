# SSH key pair overview {#concept_j33_vqw_ydb .concept}

## What is an SSH key pair? {#section_shx_vqw_ydb .section}

An SSH key pair, or key pair for short, is a secure authentication method provided by Alibaba Cloud for remote logon to your Linux instance. It is an alternative to authentication using a username and password.

The key pair is composed of a public key and a private key. The asymmetric cryptography feature uses the **public key** to encrypt data, and the local client uses the **private key** to decrypt the data.

The Linux ECS instance stores the public key. You use the private key to connect to your instance by entering SSH commands or using other tools. Username and password authentication is disabled by ECS once the SSH key pair is enabled to guarantee security.

## Benefits {#section_thx_vqw_ydb .section}

Compared with typical username and password authentication, SSH key pair has the following benefits:

**High security** 

Using an SSH key pair to log on to a Linux instance is more secure and reliable.

-   A key pair prevents brute force attacks targeted at password cracking.

-   Due to the complexity of RSA encryption, the private key cannot be deduced even if the public key is maliciously acquired.


**Ease of use** 

-   You can log on remotely to an instance by configuring the key pair in the ECS console and on the local client, meaning you do not need to enter a password every time you log on.

-   We recommend this method if you maintain multiple ECS instances.


## Limits {#section_xhx_vqw_ydb .section}

Using an SSH key pair has the following restrictions:

-   Applies only to Linux instances.
-   Alibaba Cloud only supports the creation of 2048-bit RSA key pairs.
    -   Alibaba Cloud holds the public key of the key pair.
    -   After the key pair is created, you must download and securely store the private key.
    -   The private key is in the unencrypted PEM-encoded `PKCS#8` format.
-   Each Alibaba Cloud account can have a maximum of 500 key pairs per region.
-   Only one SSH key pair can be added to a Linux instance at a time. If a key pair has already been added to your instance, the new key pair replaces the old one.
-   During the lifecycle of a Linux instance, you can add or remove an SSH key pair at any time. After you add or remove a key pair, you must [restart the instance](../../../../reseller.en-US/Instances/Manage instances/Restart an instance.md) for the change to take effect.
-   All instances of any [instance type family](reseller.en-US/Instances/Instance type families.md), except for the I/O optimized-instances of Generation I, support SSH key pairs.

## Create an SSH key pair {#section_a3x_vqw_ydb .section}

To create an SSH key pair, you can use either of the following methods:

-   [Create an SSH key pair](../../../../reseller.en-US/Security/Key pairs/How do I use an SSH key pair?.md#) in the ECS console.

    **Note:** Once you create a key pair in the ECS console, you must immediately download and securely store the private key for later use. If SSH key pair authentication is enabled for an ECS instance, you cannot log on to the ECS instance without the private key of the key pair.

-   Create an SSH key pair by using other key pair builders and [import it](../../../../reseller.en-US//Import an SSH key pair.md) to ECS.

    The following key types are supported:

    -   rsa
    -   dsa
    -   ssh-rsa
    -   ssh-dss
    -   ecdsa
    -   ssh-rsa-cert-v00@openssh.com
    -   ssh-dss-cert-v00@openssh.com
    -   ssh-rsa-cert-v01@openssh.com
    -   ssh-dss-cert-v01@openssh.com
    -   ecdsa-sha2-nistp256-cert-v01@openssh.com
    -   ecdsa-sha2-nistp384-cert-v01@openssh.com
    -   ecdsa-sha2-nistp521-cert-v01@openssh.com

