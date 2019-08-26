# Import an SSH key pair {#concept_hvw_wj1_ydb .concept}

If you prefer to use another key generation tool, you can use it to generate an RSA key pair and then import its public key into Alibaba Cloud. See [SSH key pairs](../../../../reseller.en-US/Product Introduction/Network and security/SSH key pairs.md#) for the supported types of imported key pairs.

**Note:** To guarantee your instance security, keep the private key of the key pair secure and do not import the private key to Alibaba Cloud.

To import an SSH key pair, you must have a key pair that has been generated using another tool. The public key to be imported into Alibaba Cloud must be Base64-encoded.

To import an SSH key pair, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Networks and Security** \> **SSH Key Pair**.
3.  Click **Create SSH Key Pair**.
4.  Select a region.
5.  On the Create SSH Key Pair page, enter a name for the key pair, and select **Import SSH Key Pair**, and then enter the **Public Key**.

    **Note:** The specified key pair name must not be the same as that of an existing key pair or a key pair that was bound to an instance before being deleted. Otherwise, an error message “The key pair already exists” appears.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9729/15433844284670_en-US.png)

6.  Click **OK**.

After creation, you can view the information, including the key pair **Name** and **Fingerprint**, in the key pair list.

