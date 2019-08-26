# How do I use an SSH key pair? {#concept_wy4_th1_ydb .concept}

This topic describes how to use an SSH key pair in the ECS console. Note that only Linux instances support an SSH key pair.

## Create an SSH key pair {#section_f5c_h31_ydb .section}

1.  Log on to the ECS console.
2.  In the left-side navigation pane, choose **Networks and Security** \> **SSH Key Pair**.
3.  Select the target region.
4.  Click **Create SSH Key Pair**.
5.  Enter a name for the SSH key pair, and then select **Auto-Create SSH Key Pair**.

    **Note:** Do not enter an SSH key pair name that already exists. Otherwise, the ECS console prompts you that the key already exists.

6.  Click **OK** to create the SSH key pair.

    **Note:** 

    -   After an SSH key pair is created, we recommend that you immediately download and securely save the private key.
    -   Each Alibaba account can have up to 500 SSH key pairs in each region.

Related API: [CreateKeyPair](../reseller.en-US/API Reference/SSH key pairs/CreateKeyPair.md#)

## View public key information {#section_u41_dvh_tgb .section}

For **Windows**:

1.  Start PuTTYgen.
2.  Click **Load**.
3.  Select the .ppk or.pem file.

    PuTTYgen shows the public key information.


For **Linux** or **Mac**:

Run the ssh-keygen command and specify the path of the .pem file.

```
ssh-keygen -y -f /path_to_key_pair/my-key-pair.pem
```

The returned public key information is as follows:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCxxxxxx
```

**Note:** If the execution of this command fails, run the `chmod 400 my-key-pair.pem` command to change the ownership to you only.

**View public key information within an instance**

A public key is stored in the `~/.ssh/authorized_keys` file. Opening that file in an instance returns public key information.

## Import an SSH key pair {#section_ztk_vvq_pgb .section}

In addition to creating an SSH key pair in the ECS console, you can also use a tool to generate an SSH key pair and import the public key to Alibaba Cloud.

**Note:** You must securely save the private key. Do not import the private key to Alibaba Cloud. Otherwise, your account security may be compromised.

An imported public key must be `Base64` encoded and must support any of the following encryption methods:

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

1.  Obtain public key information. For more information, see [查看公钥信息](#).
2.  Log on to the ECS console.
3.  In the left-side navigation pane, choose **Networks and Security** \> **SSH Key Pair**.
4.  Select the target region.
5.  Click **Create SSH Key Pair**.
6.  Enter a name for the SSH key pair, select **Import SSH Key Pair**, and then enter public key information in the **Public Key**box.

    **Note:** Do not specify a name that is the same as an existing one or as one that is deleted while remains attached to an instance. Otherwise, the ECS console prompts you that the key already exists.

7.  Click **OK**.

Related API: [ImportKeyPair](../reseller.en-US/API Reference/SSH key pairs/ImportKeyPair.md#).

## Attach an SSH key pair {#section_d4l_ql1_ydb .section}

You can attach an SSH key pair to an instance during or after instance creation.

**Note:** 

-   Each ECS instance can only be associated with one SSH key pair. If an ECS instance is already associated with an SSH key pair, the old key is automatically replaced with the new key.
-   If an ECS instance uses password authentication, the password authentication mode is automatically disabled after a key pair is associated with the instance. However, if you [重置实例密码](../reseller.en-US/Instances/Manage instances/Reset an instance password.md#) after attaching a key pair to an instance, you can use both the password and the key pair to log on to the instance.

1.  Log on to the ECS console.
2.  In the left-side navigation pane, choose **Networks and Security** \> **SSH Key Pair**.
3.  Select the target region.
4.  Find the target key pair, and click **Bind** in the **Actions** column.
5.  In the **Select Instance** box, select the target ECS instance, and click **\>** to move it to the **Selected** box.

    **Note:** If an ECS instance in the **Select Instance** box appears grey, it means that the instance is running Windows, which does not support usage of SSH key pairs.

6.  Click **OK**.

    **Note:** If an ECS instance is in the **Running** state, you must restart it in the ECS console or by using the API to activate the key pair after attaching it to the instance.


After you attach an SSH key pair to an ECS instance, you can log on to that ECS instance by using the SSH key pair.

Related API: [AttachKeyPair](../reseller.en-US/API Reference/SSH key pairs/AttachKeyPair.md#).

## Detach an SSH key pair {#section_lqq_yp1_ydb .section}

1.  Log on to the ECS console.
2.  In the left-side navigation pane, choose **Networks and Security** \> **SSH Key Pair**.
3.  Select the target region.
4.  Find the target key pair, and click **Unbind** in the **Actions** column.
5.  In the **Select Instance** box, select the target ECS instance, and click **\>** to move it to the **Selected** box.

    **Note:** If an ECS instance in the **Select Instance** box appears grey, it means that the instance is running Windows, which does not support usage of SSH key pairs.

6.  Click **OK**.

    **Note:** 

    -   If an ECS instance is in the **Running** state, you must restart it in the ECS console or by using the API to complete the operation after detaching it from the instance.
    -   If an instance password is reset before the detach operation, you can use the password to log on to the instance after the detach operation. Otherwise, after the detach operation, you must [重置实例密码](../reseller.en-US/Instances/Manage instances/Reset an instance password.md#) before you can use a password to log on to the instance.

Related API: [DetachKeyPair](../reseller.en-US/API Reference/SSH key pairs/DetachKeyPair.md#).

## Add or replace a key pair in an instance {#section_hd2_3vh_tgb .section}

You can add multiple key pairs in an instance and use them to access that instance. You can also replace an existing key pair.

1.  Retrieve the public key of a new key pair. For more information, see [查看公钥信息](#).
2.  Use the existing key pair to log on to the ECS instance.
3.  Run vim .ssh/authorized\_keys to open the file.
4.  Add or replace the public key.

    -   Add a public key: Add a new public key below the existing public key, and save the file.

        ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCys3aOkFm1Xh8iN0lijeQF5mz9Iw/FV/bUUduZjauiJa1KQJSF4+czKtqMAv38QEspiWStkSfpTn1g9qeUhfKd4uWlmxeQ+XjPsf22fRem+v7MHMa7KnZWiHJxO62D4Ihvv2hKfskz8K44mVMeInMjGO+u17IaL2l2ri8q9YdvVHt0Mw5TpCkERWGoBPE1Y8vxFb97TaE5+zc+2+eff6PDCMkVTP+c/feMeCxpx6Lhc2NEpHIPxMpjOv1IytKiDfWcezA2aCmKre0Q2t/YudCmJ8HTCnLId5LpirbNE4X08Bk7tXZAU8UaoeDdUr/FKB1Cxw1TbGMTfWBcdWkdp2lv imported-openssh-key
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCg9iTWWGrWFvVlnI0E3Deb/9H9mPCO1Xt2fxxxxxxxxBtmR imported-openssh-key
        ```

    -   Replace a public key: Delete the existing public key, add a new public key, and save the file.

        ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCg9iTWWGrWFvVlnI0E3Deb/9H9mPCO1Xt2fxxxxxxxxBtmR imported-openssh-key
        ```

    If you can use the new private key to log on to the ECS instance, the add or replace operation is completed successfully.


## Delete an SSH key pair {#section_dtt_zvq_pgb .section}

An SSH key pair cannot be restored once it is deleted. However, the delete operation does not impact the instance that is using that key pair, and the instance details still show the name of the deleted key pair.

**Note:** 

-   If your key pair has been attached to an instance, and it is not detached from that instance before the deletion, you cannot create a key pair of the same name after the deletion. Otherwise, if you create or import such a key pair, the ECS console prompts you that the key pair already exists when you enter this key pair name.
-   If your key pair is not attached to an instance, or is detached from an instance before the deletion, you can create a key pair of the same name after the deletion.

1.  Log on to the ECS console.
2.  In the left-side navigation pane, choose **Networks and Security** \> **SSH Key Pair**.
3.  Select the target region.
4.  Select one or more key pairs to be deleted.
5.  Click **Delete**.

Related API: [DeleteKeyPairs](../reseller.en-US/API Reference/SSH key pairs/DeleteKeyPairs.md#).

