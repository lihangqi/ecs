# 使用SSH密钥对 {#concept_wy4_th1_ydb .concept}

本文提供了在ECS控制台上使用SSH密钥对的操作指示。SSH密钥对仅支持Linux实例。

## 创建SSH密钥对 {#section_f5c_h31_ydb .section}

1.  登录ECS管理控制台。
2.  在左侧导航栏中，单击**密钥对**。
3.  选择地域。
4.  单击**创建密钥对**。
5.  设置密钥对名称，并选择**自动新建密钥对**。

    **说明：** 密钥对名称不能重复。否则，控制台会提示密钥对已存在。

6.  单击**确定**创建密钥对。

    **说明：** 

    -   创建密钥对后，请务必下载并妥善保管私钥。使用密钥对绑定ECS实例后，如果没有私钥，您将无法登录该ECS实例。
    -   一个账号在一个地域最多可以拥有500个密钥对。

相关API：[CreateKeyPair](../intl.zh-CN/API参考/SSH 密钥对/CreateKeyPair.md#)

## 查看公钥信息 {#section_u41_dvh_tgb .section}

**本地为Windows操作系统**

1.  启动PuTTYgen。
2.  单击**Load**。
3.  选择.ppk或.pem文件。

    PuTTYgen会显示公钥信息。


**本地为Linux或Mac系统**

运行ssh-keygen命令，并指定.pem文件的路径。

```
ssh-keygen -y -f /path_to_key_pair/my-key-pair.pem
```

返回公钥信息，类似如下所示：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCxxxxxx
```

**说明：** 如果该命令失败，请运行`chmod 400 my-key-pair.pem`命令更改权限，确保只有您才能查看该文件。

**在实例内部查看**

公钥内容放在`~/.ssh/authorized_keys`文件内。在实例内打开该文件，则返回公钥信息。

## 导入SSH密钥对 {#section_ztk_vvq_pgb .section}

除了新建密钥对之外，您也可以使用工具生成SSH密钥对并将公钥导入阿里云。

**说明：** 不要导入私钥。请您妥善保存私钥。

导入阿里云的公钥必须使用`Base64`编码，且必须支持下列加密方式中的一种：

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

1.  获取公钥信息。详细步骤，请参见[查看公钥信息](#)。
2.  登录ECS管理控制台。
3.  在左侧导航栏中，单击**密钥对**。
4.  选择地域。
5.  单击**创建密钥对**。
6.  设置密钥对名称，选择**导入已有密钥对**，并在**公钥内容**中输入公钥信息。

    **说明：** 指定的名称不应该与已有的密钥对名称重复，也不应该与删除前仍绑定实例的密钥对名称重复，否则，控制台会提示密钥对已存在。

7.  单击**确定**。

相关API：[ImportKeyPair](../intl.zh-CN/API参考/SSH 密钥对/ImportKeyPair.md#)

## 绑定SSH密钥对 {#section_d4l_ql1_ydb .section}

您可以在创建实例时指定SSH密钥对，也可以在创建实例后绑定SSH密钥对。

**说明：** 

-   一台ECS实例只能绑定一个SSH密钥对。如果ECS实例已经绑定了SSH密钥对，绑定新密钥对后，新密钥自动替换原有的密钥。
-   如果ECS实例使用密码认证，绑定密钥对后，密码验证方式自动失效。但如果在绑定密钥对之后[重置实例密码](../intl.zh-CN/实例/管理实例资源/重置实例登录密码.md#)，除使用密钥对方式之外，您也可以使用密码方式登录实例。

1.  登录ECS管理控制台。
2.  在左侧导航栏中，单击**密钥对**。
3.  选择地域。
4.  找到需要操作的密钥对，在**操作**列中，单击**绑定密钥对**。
5.  在**选择ECS实例**栏中，选中需要绑定该密钥对的ECS实例名称，单击**\>**，移入**已选择**栏中。

    **说明：** 如果**选择ECS实例**栏中的ECS实例名称显示为灰色，表示该实例为Windows实例，不支持SSH密钥对。

6.  单击**确定**。

    **说明：** 如果ECS实例处于**运行中**（Running）状态，绑定SSH密钥对后，您必须在控制台或者使用API重启实例，才能使操作生效。


ECS实例绑定SSH密钥对后，您就可以通过SSH密钥对登录ECS实例。

相关API：[AttachKeyPair](../intl.zh-CN/API参考/SSH 密钥对/AttachKeyPair.md#)

## 解绑SSH密钥对 {#section_lqq_yp1_ydb .section}

1.  登录ECS管理控制台。
2.  在左侧导航栏中，单击**密钥对**。
3.  选择地域。
4.  找到需要操作的密钥对，在**操作**列中，单击**解绑密钥对**。
5.  在**选择ECS实例**栏中，选中需要解绑的ECS实例名称，单击**\>**，移入**已选择**栏中。
6.  单击**确定**。

    **说明：** 

    -   如果ECS实例处于**运行中**（Running）状态，解绑SSH密钥对后，您必须在控制台或者使用API重启实例，才能使操作生效。
    -   如果在解绑密钥对之前已经重置了实例密码，则解绑密钥对之后可以使用密码方式登录。如果解绑密钥对之前没有重置实例密码，则解绑密钥对之后，必须[重置实例密码](../intl.zh-CN/实例/管理实例资源/重置实例登录密码.md#)才能使用密码方式登录实例。

相关API：[DetachKeyPair](../intl.zh-CN/API参考/SSH 密钥对/DetachKeyPair.md#)

## 在实例内添加或替换密钥对 {#section_hd2_3vh_tgb .section}

您可以在实例内添加多个密钥对，允许多个密钥对访问该实例。您也可以替换现有的密钥对。

1.  获取新密钥对的公钥信息。详细步骤，请参见[查看公钥信息](#)。
2.  使用现有的密钥对连接ECS实例。
3.  运行vim .ssh/authorized\_keys命令打开文件。
4.  添加或者替换公钥信息。

    -   添加公钥信息：在现有的公钥信息下方添加新的公钥信息，并保存。

        ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCys3aOkFm1Xh8iN0lijeQF5mz9Iw/FV/bUUduZjauiJa1KQJSF4+czKtqMAv38QEspiWStkSfpTn1g9qeUhfKd4uWlmxeQ+XjPsf22fRem+v7MHMa7KnZWiHJxO62D4Ihvv2hKfskz8K44mVMeInMjGO+u17IaL2l2ri8q9YdvVHt0Mw5TpCkERWGoBPE1Y8vxFb97TaE5+zc+2+eff6PDCMkVTP+c/feMeCxpx6Lhc2NEpHIPxMpjOv1IytKiDfWcezA2aCmKre0Q2t/YudCmJ8HTCnLId5LpirbNE4X08Bk7tXZAU8UaoeDdUr/FKB1Cxw1TbGMTfWBcdWkdp2lv imported-openssh-key
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCg9iTWWGrWFvVlnI0E3Deb/9H9mPCO1Xt2fxxxxxxxxBtmR imported-openssh-key
        ```

    -   替换公钥信息：删除现有的公钥信息，添加新的公钥信息，并保存。

        ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDdlrdZwV3+GF9q7rhc6vYrExwT4WU4fsaRcVXGV2Mg9RHex21hl1au77GkmnIgukBZjywlQOT4GDdsJy2nBOdJPrCEBIP6t0Mk5aPkK/fctNuKjcmMMOA8YUT+sJKn3l7rCLkesE+S5880yNdRjBiiUy40kyr7Y+fqGVdSOHGMXZQPpkBtojcV14uAy0yV6/htEqGa/Jq4fH7bR6CYQ2XgH/hCap29Mdi/G5Tx1nbUKuIHdMWOPvjGACGcXclex+lHtTGiAIRG1riyNRVC47ZEVCg9iTWWGrWFvVlnI0E3Deb/9H9mPCO1Xt2fxxxxxxxxBtmR imported-openssh-key
        ```

    如果能够使用新的私钥登录ECS实例，表示添加或者替换密钥对成功。


## 删除SSH密钥对 {#section_dtt_zvq_pgb .section}

删除SSH密钥对后不可恢复，但是正在使用该密钥对的实例不受影响，实例信息中仍然会显示被删除的密钥对名称。

**说明：** 

-   如果您的密钥对已经绑定实例，而且在删除前未解绑实例，删除后，您将不能再用相同的名称创建密钥对。否则，创建或导入密钥对时，输入这个名称，控制台会报错密钥对已存在。
-   如果您的密钥对在删除前未绑定实例或者已经解绑实例，删除后，您仍可以使用相同的名称创建密钥对。

1.  登录ECS管理控制台。
2.  在左侧导航栏中，单击**密钥对**。
3.  选择地域。
4.  选中一个或多个需要删除的密钥对。
5.  单击**删除**。

相关API：[DeleteKeyPairs](../intl.zh-CN/API参考/SSH 密钥对/DeleteKeyPairs.md#)

