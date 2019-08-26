# 通过控制台使用实例 RAM 角色 {#concept_v3v_zct_xdb .concept}

## 使用限制 {#section_x4c_cdt_xdb .section}

使用实例 RAM 角色存在如下限制：

-   只有专有网络 （VPC） 网络类型的 ECS 实例才能使用实例 RAM 角色。
-   一个 ECS 实例一次只能授予一个实例 RAM 角色。
-   当您给 ECS 实例授予了实例 RAM 角色后，并希望在 ECS 实例内部部署的应用程序中访问云产品的 API 时，您需要通过 [ZH-CN\_TP\_9661.md\#](intl.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#) 获取实例 RAM 角色的临时授权 Token。参阅 [6. （可选）获取临时授权 Token](#Token)。
-   如果您是通过 RAM 用户子账号使用实例 RAM 角色，您需要通过云账号 [7. （可选）授权 RAM 用户使用实例 RAM 角色](#Authorize)。

## 前提条件 {#section_z4c_cdt_xdb .section}

您已经开通 RAM 服务，参阅 RAM 文档 [开通方法](../../../../intl.zh-CN/产品定价/开通方法.md#) 开通 RAM 服务。

## 1. 创建实例 RAM 角色 {#step2 .section}

1.  登录 [RAM 控制台](https://ram.console.aliyun.com/#/overview)。
2.  在导航窗格中，单击 **角色管理**。
3.  在角色管理页面，单击 **新建角色**。
4.  在弹窗中：
    1.  **角色类型** 选择 **服务角色**。
    2.  **类型信息** 选择 **ECS 云服务器**。
    3.  输入角色名称及备注，如 EcsRamRoleDocumentTesting。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15663661095501_zh-CN.png)

    4.  单击 **确认** 完成新建。

## 2. 授权实例 RAM 角色 {#section_q1m_sst_xdb .section}

1.  登录 [RAM 控制台](https://ram.console.aliyun.com/#/overview)。
2.  在导航窗格中，单击 **策略管理**。
3.  在 策略管理 页面，单击 **新建授权策略**。
4.  在弹窗中：
    1.  **权限策略模板** 选择 **空白模板**。
    2.  输入 **授权策略名称** 及 **策略内容**，如 EcsRamRoleDocumentTestingPolicy。

        **说明：** 关于如何编写策略内容，您可以参阅 RAM 文档 [Policy 语法结构](../../../../intl.zh-CN/用户指南/（隐藏）旧版用户指南/授权策略语言/Policy 语法结构.md#)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15663661105502_zh-CN.png)

    3.  单击 **新建授权策略** 完成授权。
5.  在导航窗格中，单击 **角色管理**。
6.  在 角色管理 页面，选择创建好的角色，如 EcsRamRoleDocumentTesting，单击 **授权**。
7.  输入创建的 **授权策略名称**，如 EcsRamRoleDocumentTestingPolicy。
8.  单击符号 **\>** 选中策略名，单击 **确认**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15663661135503_zh-CN.png)


## 3. 授予实例 RAM 角色 {#section_mpc_cdt_xdb .section}

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home)。
2.  在导航窗格中，单击 **实例**。
3.  选择地域。
4.  找到要操作的 ECS 实例，选择 **更多** \> **实例设置** \> **授予/收回 RAM 角色**。
5.  在弹窗中，选择创建好的实例 RAM 角色，如 EcsRamRoleDocumentTesting，单击 **确定** 完成授予。

## 4. （可选）收回实例 RAM 角色 {#section_wn3_bwt_xdb .section}

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home)。
2.  在导航窗格中，单击 **实例**。
3.  选择地域。
4.  选择一个已经授予 RAM 角色的 ECS 实例，选择 **更多** \> **实例设置** \> **授予/收回 RAM 角色**。
5.  **操作类型** 选择 **收回**，单击 **确定** 即可收回实例 RAM 角色。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15663661135506_zh-CN.png)


## 5. （可选）更换实例 RAM 角色 {#section_wfl_2wt_xdb .section}

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home)。
2.  在导航窗格中，单击 **实例**。
3.  选择地域。
4.  选择一个已经授予 RAM 角色的 ECS 实例，选择 **更多** \> **实例设置** \> **授予/收回 RAM 角色**。
5.  **操作类型** 选择 **授予**，在已有 **RAM 角色** 中选择其他实例 RAM 角色，单击 **确定** 即可更换当前 RAM 角色。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15663661145507_zh-CN.png)


## 6. （可选）获取临时授权 Token {#Token .section}

您可以获得实例 RAM 角色的临时授权 Token，该临时授权 Token 可以执行实例 RAM 角色的权限和资源，并且该临时授权 Token 会自动周期性地更新。示例：

1.  远程连接并登录到 ECS 实例。
2.  检索名为 EcsRamRoleDocumentTesting 的实例 RAM 角色的临时授权 Token：
    -   Linux 实例： 执行命令 `curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting`。
    -   Windows 实例：参阅 [ZH-CN\_TP\_9661.md\#](intl.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
3.  获得临时授权 Token。返回示例如下：

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


## 7. （可选）授权 RAM 用户使用实例 RAM 角色 {#Authorize .section}

**说明：** 当您授权 RAM 用户使用实例 RAM 角色时，您必须授权 RAM 用户对该实例 RAM 角色的 **PassRole** 权限。其中，**PassRole** 决定该 RAM 用户能否直接执行角色策略赋予的权限。

登录 RAM 控制台，参阅 [为 RAM 用户授权](../../../../intl.zh-CN/快速入门/（隐藏）旧版快速入门/为 RAM 用户授权.md#) 完成授权，授权策略如下所示：

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

其中，\[ECS RAM Action\] 表示可授权 RAM 用户的权限，请参阅 [鉴权规则](../../../../intl.zh-CN/API参考/鉴权规则.md#)。

## 参考链接 {#section_bxr_pwt_xdb .section}

-   您也可以 [通过API使用实例RAM角色](intl.zh-CN/安全/实例RAM角色/通过API使用实例RAM角色.md#)。
-   您也许想 [借助实例 RAM 角色访问其它云产品 API](https://www.alibabacloud.com/help/doc-detail/54579.htm)。

