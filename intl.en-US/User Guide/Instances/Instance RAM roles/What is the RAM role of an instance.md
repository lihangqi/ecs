# What is the RAM role of an instance {#concept_kbp_r1t_xdb .concept}

Instance RAM \(Resource Access Management\) roles allow you to authorize role-based permissions to ECS instances.

You can assign a [role](../../../../reseller.en-US//Identities/Role.md#) to an ECS instance to allow applications hosted on that instance to access other cloud services by using a temporary STS \(Security Token Service\) credential. This helps guarantee the security of your AccessKey and allows you to apply fine-grained access control of your instances.

## Background {#section_rsm_x1t_xdb .section}

Generally, applications within an ECS instance need to use the AccessKey of the **primary account** or [RAM user account](../../../../reseller.en-US//Identities/User.md#),  which includes an AccessKeyId and AccessKeySecret, to access various cloud services on the Alibaba Cloud platform.

This means that, to make a call, you must apply the AccessKey directly in the instance, such as in the configuration file. However, if Alibaba Cloud writes the AccessKey into the instance for calling purposes, the AccessKey may be mistakenly exposed. To ensure the security of your account and resources, Alibaba Cloud provides instance RAM roles to support .

## Benefits {#section_ssm_x1t_xdb .section}

Instance RAM roles enable you to:

-   Associate a [role](../../../../reseller.en-US//Identities/Role.md#) to an ECS instance.

-   Access other cloud services securely \(such as OSS, SLB, and ApsaraDB for RDS\) by using the STS credential from the applications within the ECS instance.

-   Assign roles that have different policies for different ECS instances, and allow those instances have restrictive access level to other cloud services to obtain fine-grained access control.

-   Maintain the access permission of ECS instances by modifying only the policy of the RAM role, meaning no changes to the AccessKey are required.


## Pricing {#section_usm_x1t_xdb .section}

Instance RAM roles are free to use.

## Limits {#section_vsm_x1t_xdb .section}

Instance RAM roles have the following limits:

-   Instance RAM roles are only applicable to VPC instances.

-   An ECS instance can only be authorized to one instance RAM role.


## How to use an instance RAM role {#section_xsm_x1t_xdb .section}

The instance RAM role can be used by any of the following methods:

-   [Use the instance RAM role in the console](reseller.en-US/User Guide/Instances/Instance RAM roles/Use the instance RAM role in the console.md#).

-   [Use the instance RAM role by calling APIs](reseller.en-US/User Guide/Instances/Instance RAM roles/Use the instance RAM role by calling APIs.md#).


## References {#section_vwf_kbt_xdb .section}

-   For a list of cloud services that support STS, see [cloud services supporting RAM](../../../../reseller.en-US/Product Introduction/Cloud services supporting RAM.md#).

-   See [access other Cloud Product APIs by the Instance RAM Role](../../../../reseller.en-US/Best Practices/Access other Cloud Product APIs by the Instance RAM Role.md#) for instruction on how to access other cloud services.


