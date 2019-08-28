# Revoke the authorization for internal network communication between ECS instances for different accounts through the API {#task_810852 .task}

If you have authorized internal network communication between ECS instances for different accounts in the same region, you can revoke security group authorization as specified in this topic.

Alibaba Cloud CLI is used to call ECS APIs. Make sure that you have installed Alibaba Cloud CLI. For more information, see [Alibaba Cloud CLI Installation Guide](../../../../intl.en-US/Installation Guide/Overview.md#).

As specified in this topic, you can call [RevokeSecurityGroup](../../../../intl.en-US/API Reference/Security groups/RevokeSecurityGroup.md#) to revoke an authorized security group rule. You must prepare the following items:

-   Account name: the name of the account that you use to log on to the ECS console.
-   Security group ID for the ECS instance: the ID of the security group to which the instance involved belongs. You can view this item in the ECS console or by calling [DescribeSecurityGroupReferences](../../../../intl.en-US/API Reference/Security groups/DescribeSecurityGroupReferences.md#).
-   Region ID for the ECS instance: See [Regions and zones](../../../../intl.en-US/General Reference/Regions and zones.md#). cn-beijing is used in this example.

The following table lists the information of two accounts.

|Account|Account name|Security group|Security group ID|
|-------|------------|--------------|-----------------|
|Account A|a@aliyun.com|sg1|sg-bp1azkttqpldxgtedXXX|
|Account B|b@aliyun.com|sg2|sg-bp15ed6xe1yxeycg7XXX|

After revoking the authorization for internal network communication between ECS instances for different accounts, you can re-authorize the communication.

1.  Run the following command for Account A: 

    ``` {#codeblock_mtf_6ex_ila}
    aliyun ecs RevokeSecurityGroup --SecurityGroupId sg-bp1azkttqpldxgtedXXX --RegionId cn-beijing --IpProtocol all --PortRange -1/-1 --SourceGroupId sg-bp15ed6xe1yxeycg7XXX --SourceGroupOwnerAccount b@aliyun.com --NicType intranet
    ```

2.  Run the following command for Account B: 

    ``` {#codeblock_2dl_w8z_o1k}
    aliyun ecs RevokeSecurityGroup --SecurityGroupId sg-bp15ed6xe1yxeycg7XXX --RegionId cn-beijing --IpProtocol all --PortRange -1/-1 --SourceGroupId sg-bp1azkttqpldxgtedXXX --SourceGroupOwnerAccount a@aliyun.com --NicType intranet
    ```


