# Create an SSH key pair {#concept_wy4_th1_ydb .concept}

## Limits {#section_odb_g31_ydb .section}

-   The [SSH key pair](../../../../reseller.en-US/Product Introduction/Network and security/SSH key pairs.md#), abbreviated as key pair, applies to Linux instances only.
-   Currently, only 2048-bit RSA key pairs are supported.
    -   Alibaba Cloud holds the public key of the key pair.
    -   After creating the key pair, you must save and keep the private key of the key pair for further use.
    -   The private key follows the unencrypted PEM-encoded `PKCS#8` format.
-   An Alibaba Cloud account can have a maximum of 500 key pairs per region.

## Create an SSH key pair {#section_f5c_h31_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Networks and Security** \> **SSH Key Pair**.
3.  Select a region.
4.  On the SSH Key Pairs page, select a region, and click **Create SSH Key Pair**.
5.  On the Create SSH Key Pair page, enter a name for the key pair, and select **Auto-Create SSH Key Pair**.

    **Note:** The specified key pair name must be unique. It cannot be the same as that of the existing key pairs or a key pair that was bound to the instance before being deleted. Otherwise, an error message “The key pair already exists” appears.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9728/15433135464669_en-US.png)

6.  Click **OK** to create the key pair.

    **Note:** After a key pair is created, you must download and save the private key for further use.  If you do not have the private key, you cannot log on to the ECS instance.


After creating the key pair, you can view the information, including key pair **Name** and **Fingerprint** in the key pair list.

## What to do next {#section_nn4_5j1_ydb .section}

After creating an SSH key pair, you can [bind or unbind it](reseller.en-US/User Guide/Key pairs/Bind or unbind an SSH key pair.md#) to an ECS instance.

