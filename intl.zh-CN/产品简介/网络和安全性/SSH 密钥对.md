# SSH 密钥对 {#concept_j33_vqw_ydb .concept}

SSH 密钥对，常简称为密钥对，是区别于用户名加密码的远程登录 Linux 实例认证方式。SSH 密钥对通过加密算法生成一对密钥，默认采用 RSA 2048 位的加密方式。一个对外界公开，称为 **公钥**，另一个您自己保留，称为 **私钥**，私钥使用未加密的 PEM（Privacy-Enhanced Mail） 编码的 `PKCS#8` 格式。

## 功能优势 {#section_thx_vqw_ydb .section}

相较于用户名和密码认证方式，SSH 密钥对有以下优势：

**安全性**

SSH 密钥对登录认证更为安全可靠：

-   密钥对安全强度远高于常规用户口令，可以杜绝暴力破解威胁。

-   不可能通过公钥推导出私钥。


**便捷性**

-   如果您将公钥配置在 Linux 实例中，那么，在本地或者另外一台实例中，您可以使用私钥通过 SSH 命令或相关工具登录目标实例，而不需要输入密码。

-   便于远程登录大量 Linux 实例，方便管理。如果您需要批量维护多台 Linux 实例，推荐使用这种方式登录。


## 使用限制 {#section_xhx_vqw_ydb .section}

使用 SSH 密钥对有如下限制：

-   仅支持 Linux 实例。
-   目前，ECS 只支持创建 2048 位的 RSA 密钥对。
-   一个云账号在一个地域最多可以拥有 500 个密钥对。
-   一台 Linux 实例只能绑定一个 SSH 密钥对。如果您的实例已绑定密钥对，绑定新的密钥对会替换原来的密钥对。
-   [已停售的实例规格](https://help.aliyun.com/document_detail/55263.html) 无法使用 SSH 密钥对。

**说明：** 

-   如果使用 SSH 密钥对登录 Linux 实例，将会禁用密码登录，以提高安全性。
-   ECS 会保存密钥对的公钥部分。
-   密钥对创建成功后，您需要妥善保管私钥。
-   基于数据安全考虑，在实例状态为 **运行中 （Running）** 绑定或者解绑密钥对时，您需要重启实例使操作生效。

## 生成方式 {#section_a3x_vqw_ydb .section}

SSH 密钥对的生成方式包括：

-   [由 ECS 生成](../../../../../cn.zh-CN/用户指南/密钥对/创建 SSH 密钥对.md#)，默认采用 RSA 2048 位的加密方式。

    **说明：** 如果您的密钥对由 ECS 生成，那么在首次生成密钥对时，请务必下载并妥善保存私钥。当该密钥对绑定某台实例时，如果没有私钥，您将无法登录实例。

-   由您采用 SSH 密钥对生成器生成后再导入 ECS，导入的密钥对必须支持下列任一种加密方式：
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

## 相关操作 {#section_v3y_1rw_ydb .section}

-   [创建 SSH 密钥对](../../../../../cn.zh-CN/用户指南/密钥对/创建 SSH 密钥对.md#)。
-   [导入 SSH 密钥对](../../../../../cn.zh-CN/用户指南/密钥对/导入 SSH 密钥对.md#)。
-   [删除 SSH 密钥对](../../../../../cn.zh-CN/用户指南/密钥对/删除 SSH 密钥对.md#)。
-   [绑定和解绑 SSH 密钥对](../../../../../cn.zh-CN/用户指南/密钥对/绑定和解绑 SSH 密钥对.md#)。
-   [创建实例](../../../../../cn.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#) 时指定 SSH 密钥对。
-   [使用SSH密钥对连接Linux实例](../../../../../cn.zh-CN/用户指南/连接实例/使用SSH密钥对连接Linux实例.md#)。

