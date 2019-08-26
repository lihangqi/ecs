# 通过 API 使用实例 RAM 角色 {#concept_jwk_pd5_xdb .concept}

## 使用限制 {#section_f2w_td5_xdb .section}

使用实例 RAM 角色存在如下限制：

-   只有专有网络 （VPC） 网络类型的 ECS 实例才能使用实例 RAM 角色。
-   一个 ECS 实例一次只能授予一个实例 RAM 角色。
-   当您给 ECS 实例授予了实例 RAM 角色后，并希望在 ECS 实例内部部署的应用程序中访问云产品的 API 时，您需要通过 [实例元数据](intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#) 获取实例 RAM 角色的临时授权 Token。参阅 [获取临时授权 Token](#)。
-   如果您是通过 RAM 用户子账号使用实例 RAM 角色，您需要通过云账号 [授权 RAM 用户使用实例 RAM 角色](#)。

## 前提条件 {#section_h2w_td5_xdb .section}

您已经开通 RAM 服务，参阅 RAM 文档 [开通方法](../../../../intl.zh-CN/产品定价/开通方法.md#) 开通 RAM 服务。

## 1. 创建实例 RAM 角色 {#step3 .section}

1.  调用接口 [CreateRole](../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#) 创建实例 RAM 角色。
2.  设置 RoleName 参数，如将其值置为 EcsRamRoleDocumentTesting。
3.  按如下策略设置 AssumeRolePolicyDocument：

    ```
    {
         "Statement": [
         {
             "Action": "sts:AssumeRole",
             "Effect": "Allow",
             "Principal": {
             "Service": [
             "ecs.aliyuncs.com"
             ]
             }
         }
         ],
         "Version": "1"
     }
    ```


## 2. 授权实例 RAM 角色 {#section_jhn_g25_xdb .section}

1.  调用接口 [CreatePolicy](../../../../intl.zh-CN/API参考/API 参考（RAM）/授权策略管理接口/CreatePolicy.md#) 新建授权策略。
2.  设置 RoleName 参数，如将其值置为 EcsRamRoleDocumentTestingPolicy。
3.  按如下策略设置 PolicyDocument：

    ```
    {
         "Statement": [
             {
             "Action": [
                 "oss:Get*",
                 "oss:List*"
             ],
             "Effect": "Allow",
             "Resource": "*"
             }
         ],
         "Version": "1"
     }
    ```

4.  调用接口 [AttachPolicyToRole](../../../../intl.zh-CN/API参考/API 参考（RAM）/授权策略管理接口/AttachPolicyToRole.md#) 授权角色策略。
5.  设置 PolicyType 参数为 Custom。
6.  设置 PolicyName 参数，如 EcsRamRoleDocumentTestingPolicy。
7.  设置 RoleName 参数，如 EcsRamRoleDocumentTesting。

## 3. 授予实例 RAM 角色 {#section_pmw_bf5_xdb .section}

1.  调用接口 [AttachInstanceRamRole](../../../../intl.zh-CN/API 参考/实例/AttachInstanceRamRole.md#) 为实例授予 RAM 角色。
2.  设置 RegionId 及 InstanceIds 参数指定一个 ECS 实例。
3.  设置 RamRoleName 参数，如 EcsRamRoleDocumentTesting。

## 4. （可选）收回实例 RAM 角色 {#section_k4m_2f5_xdb .section}

1.  调用接口 [DetachInstanceRamRole](../../../../intl.zh-CN/API 参考/实例/DetachInstanceRamRole.md#) 收回实例 RAM 角色。
2.  设置 RegionId 及 InstanceIds 参数指定一个 ECS 实例。
3.  设置 RamRoleName 参数，如 EcsRamRoleDocumentTesting。

## 5. （可选）获取临时授权 Token {#Token .section}

您可以获得实例 RAM 角色的临时授权 Token，该临时授权 Token 可以执行实例 RAM 角色的权限和资源，并且该临时授权 Token 会自动周期性地更新。示例：

1.  检索名为 EcsRamRoleDocumentTesting 的实例 RAM 角色的临时授权 Token：
    -   Linux 实例： 执行命令 `curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting` 。
    -   Windows 实例：参阅文档 [实例元数据](intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)。
2.  获得临时授权 Token。返回示例如下：

    ```
    {
    "AccessKeyId" : "XXXXXXXXX",
    "AccessKeySecret" : "XXXXXXXXX",
    "Expiration" : "2017-11-01T05:20:01Z",
    "SecurityToken" : "XXXXXXXXX",
    "LastUpdated" : "2017-10-31T23:20:01Z",
    "Code" : "Success"
    }
    
    
    ```


## 6. （可选）授权 RAM 用户使用实例 RAM 角色 {#Authorize .section}

**说明：** 当您授权 RAM 用户使用实例 RAM 角色时，您必须授权 RAM 用户对该实例 RAM 角色的 PassRole 权限。其中，PassRole 决定该 RAM 用户能否直接执行角色策略赋予的权限。

登录 RAM 控制台，参阅文档 [为 RAM 用户授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md#) 完成授权，如下所示：

```
{
        "Version": "2016-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": [
                "ecs: [ECS RAM Action]",
                "ecs: CreateInstance",
                "ecs: AttachInstanceRamRole",
                "ecs: DetachInstanceRAMRole"
            ],
            "Resource": "*"
            },
            {
        "Effect": "Allow",
        "Action": "ram:PassRole",
        "Resource": "*"
            }
        ]
}
```

其中，\[ECS RAM Action\] 表示可授权 RAM 用户的权限，请参阅 [鉴权规则](../../../../intl.zh-CN/API 参考/鉴权规则.md#)。

## 参考链接 {#section_bgl_kf5_xdb .section}

-   您也可以 [通过控制台使用实例 RAM 角色](intl.zh-CN/用户指南/实例/实例RAM角色/通过控制台使用实例 RAM 角色.md#)。
-   您也许想 [借助于实例 RAM 角色访问其他云产品](../../../../intl.zh-CN/最佳实践/借助于实例 RAM 角色访问其他云产品.md#)。
-   实例 RAM 角色相关的 API 接口包括：
    -   创建 RAM 角色：[CreateRole](../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#)
    -   查询 RAM 角色列表：[ListRoles](../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#)
    -   新建 RAM 角色策略：[CreatePolicy](../../../../intl.zh-CN/API参考/API 参考（RAM）/授权策略管理接口/CreatePolicy.md#)
    -   授权 RAM 角色策略：[AttachPolicyToRole](../../../../intl.zh-CN/API参考/API 参考（RAM）/授权策略管理接口/AttachPolicyToRole.md#)
    -   授予实例 RAM 角色：[AttachInstanceRamRole](../../../../intl.zh-CN/API 参考/实例/AttachInstanceRamRole.md#)
    -   收回实例 RAM 角色：[DetachInstanceRamRole](../../../../intl.zh-CN/API 参考/实例/DetachInstanceRamRole.md#)
    -   查询实例 RAM 角色：[DescribeInstanceRamRole](../../../../intl.zh-CN/API 参考/实例/DescribeInstanceRamRole.md#)

