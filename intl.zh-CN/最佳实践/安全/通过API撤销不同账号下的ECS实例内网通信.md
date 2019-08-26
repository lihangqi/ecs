# 通过API撤销不同账号下的ECS实例内网通信 {#task_810852 .task}

若您在同一地域下授权过不同账号的ECS实例内网通信，可以通过API接口撤销安全组授权。

-   本文使用阿里云CLI调用ECS API，请确保您已经安装了阿里云CLI。详情请参见[阿里云CLI安装指南](../../../../../intl.zh-CN/安装指南/简介.md#)。
-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。

本文通过调用RevokeSecurityGroup接口撤销已授权的安全组规则。在操作之前，您需要准备以下信息：

-   账号名：您登录ECS管理控制台的账号名称。
-   ECS实例所在的安全组ID：已授权账号内网互通的ECS实例所在的安全组。

    您可以在ECS管理控制台查看，也可以通过调用DescribeSecurityGroupReferences接口查询。

-   ECS实例所在的地域名称：取值请参见[地域和可用区](../../../../../intl.zh-CN/通用参考/地域和可用区.md#)。本文示例设置为cn-beijing，即华北 2（北京）地域。

假设两个账号的信息如下表所示。

|账号|账号名|安全组|安全组ID|
|--|---|---|-----|
|账号A|a@aliyun.com|sg1|sg-bp1azkttqpldxgtedXXX|
|账号B|b@aliyun.com|sg2|sg-bp15ed6xe1yxeycg7XXX|

除了撤销授权不同账号下的ECS实例内网通信，您也可以重新授权。详情请参见[通过API允许不同账号下的ECS实例内网通信](intl.zh-CN/最佳实践/安全/通过API允许不同账号下的ECS实例内网通信.md#)。

1.  账号A运行以下命令。 

    ``` {#codeblock_mtf_6ex_ila}
    aliyun ecs RevokeSecurityGroup --SecurityGroupId sg-bp1azkttqpldxgtedXXX --RegionId cn-beijing --IpProtocol all --PortRange -1/-1 --SourceGroupId sg-bp15ed6xe1yxeycg7XXX --SourceGroupOwnerAccount b@aliyun.com --NicType intranet
    ```

2.  账号B运行以下命令。 

    ``` {#codeblock_2dl_w8z_o1k}
    aliyun ecs RevokeSecurityGroup --SecurityGroupId sg-bp15ed6xe1yxeycg7XXX --RegionId cn-beijing --IpProtocol all --PortRange -1/-1 --SourceGroupId sg-bp1azkttqpldxgtedXXX --SourceGroupOwnerAccount a@aliyun.com --NicType intranet
    ```


**相关文档**  


[RevokeSecurityGroup](../intl.zh-CN/API参考/安全组/RevokeSecurityGroup.md#)

[DescribeSecurityGroupReferences](../intl.zh-CN/API参考/安全组/DescribeSecurityGroupReferences.md#)

