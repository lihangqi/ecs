# 通过API使用实例RAM角色 {#concept_jwk_pd5_xdb .concept}

您可以通过API创建、授权实例RAM角色，并将其授予实例。

## 使用限制 {#section_f2w_td5_xdb .section}

-   只有专有网络（VPC）网络类型的ECS实例才能使用实例RAM角色。
-   一个ECS实例一次只能授予一个实例RAM角色。
-   当您给ECS实例授予了实例RAM角色后，并希望在ECS实例内部部署的应用程序中访问云产品的API时，您需要通过[实例元数据](cn.zh-CN/实例转移/配置实例运行时环境/实例自定义数据和元数据/实例元数据.md#)获取实例RAM角色的临时授权Token。参见[获取临时授权Token](#)。
-   如果您是通过RAM用户子账号使用实例RAM角色，您需要通过云账号[授权RAM用户使用实例RAM角色](#)。

## 前提条件 {#section_h2w_td5_xdb .section}

您已经开通RAM服务，参见RAM文档[开通方法](../../../../../cn.zh-CN/产品定价/开通方法.md#)开通RAM服务。

## 步骤1：创建实例RAM角色 {#step3 .section}

1.  调用接口[CreateRole](../../../../../cn.zh-CN/API参考/角色管理接口/CreateRole.md#)创建实例RAM角色。
2.  设置RoleName参数，如将其值置为EcsRamRoleDocumentTesting。
3.  按如下策略设置AssumeRolePolicyDocument：

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


## 步骤2：授权实例RAM角色 {#section_jhn_g25_xdb .section}

1.  调用接口[CreatePolicy](../../../../../cn.zh-CN/API参考/权限策略管理接口/CreatePolicy.md#)新建授权策略。
2.  设置RoleName参数，如将其值置为EcsRamRoleDocumentTestingPolicy。
3.  按如下策略设置PolicyDocument：

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

4.  调用接口[AttachPolicyToRole](../../../../../cn.zh-CN/API参考/权限策略管理接口/AttachPolicyToRole.md#)授权角色策略。
5.  设置PolicyType参数为Custom。
6.  设置PolicyName参数，如EcsRamRoleDocumentTestingPolicy。
7.  设置RoleName参数，如EcsRamRoleDocumentTesting。

## 步骤3：授予实例RAM角色 {#section_pmw_bf5_xdb .section}

1.  调用接口[AttachInstanceRamRole](../../../../../cn.zh-CN/API参考/实例/AttachInstanceRamRole.md#)为实例授予RAM角色。
2.  设置RegionId及InstanceIds参数指定一个ECS实例。
3.  设置RamRoleName参数，如EcsRamRoleDocumentTesting。

## 步骤4：（可选）收回实例RAM角色 {#section_k4m_2f5_xdb .section}

1.  调用接口[DettachInstanceRamRole](../../../../../cn.zh-CN/API参考/实例/DetachInstanceRamRole.md#)收回实例RAM角色。
2.  设置RegionId及InstanceIds参数指定一个ECS实例。
3.  设置RamRoleName参数，如EcsRamRoleDocumentTesting。

## 步骤5：（可选）获取临时授权Token {#Token .section}

您可以获得实例RAM角色的临时授权Token，该临时授权Token可以执行实例RAM角色的权限和资源，并且该临时授权Token会自动周期性地更新。示例：

1.  检索名为EcsRamRoleDocumentTesting的实例RAM角色的临时授权Token：
    -   Linux实例：执行命令`curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting`。
    -   Windows实例：参见文档[实例元数据](cn.zh-CN/实例转移/配置实例运行时环境/实例自定义数据和元数据/实例元数据.md#)。
2.  获得临时授权Token。返回示例如下：

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


## 步骤6：（可选）授权RAM用户使用实例RAM角色 {#Authorize .section}

**说明：** 当您授权RAM用户使用实例RAM角色时，您必须授权RAM用户对该实例RAM角色的PassRole权限。其中，PassRole决定该RAM用户能否直接执行角色策略赋予的权限。

登录[RAM控制台](https://ram.console.aliyun.com/#/overview)，参见文档[为RAM用户授权](../../../../../cn.zh-CN/快速入门/为 RAM 用户授权.md#)完成授权，如下所示：

```
{
        "Version": "2016-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": [
                "ecs: \[ECS RAM Action\]",
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

其中，\[ECS RAM Action\]表示可授权RAM用户的权限，请参见[鉴权规则](../../../../../cn.zh-CN/API参考/鉴权规则.md#)。

## 相关文档 {#section_bgl_kf5_xdb .section}

-   您也可以[通过控制台使用实例RAM角色](cn.zh-CN/安全/实例RAM角色/通过控制台使用实例RAM角色.md#)。
-   您也许想[借助于实例RAM角色访问其他云产品](../../../../../cn.zh-CN/最佳实践/借助于实例 RAM 角色访问其他云产品.md#)。
-   实例RAM角色相关的API接口包括：
    -   创建RAM角色：[CreateRole](../../../../../cn.zh-CN/API参考/角色管理接口/CreateRole.md#)
    -   查询RAM角色列表：[ListRoles](../../../../../cn.zh-CN/API参考/角色管理接口/ListRoles.md#)
    -   新建RAM角色策略：[CreatePolicy](../../../../../cn.zh-CN/API参考/权限策略管理接口/CreatePolicy.md#)
    -   授权RAM角色策略：[AttachPolicyToRole](../../../../../cn.zh-CN/API参考/权限策略管理接口/AttachPolicyToRole.md#)
    -   授予实例RAM角色：[AttachInstanceRamRole](../../../../../cn.zh-CN/API参考/实例/AttachInstanceRamRole.md#)
    -   收回实例RAM角色：[DettachInstanceRamRole](../../../../../cn.zh-CN/API参考/实例/DetachInstanceRamRole.md#)
    -   查询实例RAM角色：[DescribeInstanceRamRole](../../../../../cn.zh-CN/API参考/实例/DescribeInstanceRamRole.md#)

