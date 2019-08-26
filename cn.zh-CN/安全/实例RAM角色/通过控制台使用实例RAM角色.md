# 通过控制台使用实例RAM角色 {#concept_v3v_zct_xdb .concept}

您可以在控制台创建、授权实例RAM角色，并将其授予实例。

## 使用限制 {#section_x4c_cdt_xdb .section}

-   只有专有网络（VPC）类型的ECS实例才能使用实例RAM角色。
-   一个ECS实例一次只能授予一个实例RAM角色。
-   当您给ECS实例授予了实例RAM角色后，并希望在ECS实例内部部署的应用程序中访问云产品的API时，您需要通过[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)获取实例RAM角色的临时授权Token。参见[获取临时授权Token](#)。
-   如果您是通过RAM用户子账号使用实例RAM角色，您需要通过云账号[授权RAM用户使用实例RAM角色](#)。

## 前提条件 {#section_z4c_cdt_xdb .section}

您已经开通RAM服务，参见RAM文档[开通方法](../../../../../cn.zh-CN/产品定价/开通方法.md#)。

## 步骤一：创建实例RAM角色 {#step2 .section}

1.  登录[RAM控制台](https://ram.console.aliyun.com/#/overview)。
2.  在导航窗格中，单击**角色管理**。
3.  在角色管理页面，单击**新建角色**。
4.  在弹窗中：
    1.  **角色类型**选择**服务角色**。
    2.  **类型信息**选择**ECS 云服务器**。
    3.  输入角色名称及备注，如EcsRamRoleDocumentTesting。
    4.  单击**创建**。

## 步骤二：授权实例RAM角色 {#section_q1m_sst_xdb .section}

1.  登录[RAM控制台](https://ram.console.aliyun.com/#/overview)。
2.  在导航窗格中，单击**策略管理**。
3.  在策略管理页面，单击**新建授权策略**。
4.  在弹窗中：
    1.  **权限策略模板**选择**空白模板**。
    2.  输入**授权策略名称**及**策略内容**，如EcsRamRoleDocumentTestingPolicy。

        **说明：** 关于如何编写策略内容，您可以参见RAM文档[Policy 语法结构](../../../../../cn.zh-CN//授权策略语言/Policy 语法结构.md#)。

    3.  单击**新建授权策略**完成授权。
5.  在导航窗格中，单击**角色管理**。
6.  在角色管理页面，选择创建好的角色，如EcsRamRoleDocumentTesting，单击**授权**。
7.  输入创建的**授权策略名称**，如EcsRamRoleDocumentTestingPolicy。
8.  单击符号**\>**选中策略名，单击**确定**。

## 步骤三：授予实例RAM角色 {#section_tjg_gvt_xdb .section}

-   方式一：通过控制台授予实例RAM角色
    1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
    2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
    3.  在顶部状态栏处，选择地域。
    4.  找到要操作的ECS实例，选择**更多** \> **实例设置** \> **授予/收回 RAM 角色**。
    5.  在弹窗中，选择创建好的实例RAM角色，如EcsRamRoleDocumentTesting，单击**确定**完成授予。
-   方式二：创建ECS实例时授予RAM角色
    1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
    2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
    3.  单击**创建实例**。
    4.  可参见[步骤 2：创建ECS实例](../cn.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#)设置实例的相关信息，并在**RAM 角色**属性中为实例选择已创建好的实例RAM角色，如EcsRamRoleDocumentTesting。
-   实例创建后，会拥有该实例RAM角色策略中所授权的权限。


## 步骤四：（可选）收回实例RAM角色 {#section_wn3_bwt_xdb .section}

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
3.  在顶部状态栏处，选择地域。
4.  选择一个已经授予RAM角色的ECS实例，选择**更多** \> **实例设置** \> **授予/收回 RAM 角色**。
5.  **操作类型**选择**收回**，单击**确定**即可收回实例RAM角色。

## 步骤五：（可选）更换实例RAM角色 {#section_wfl_2wt_xdb .section}

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
3.  在顶部状态栏处，选择地域。
4.  选择一个已经授予RAM角色的ECS实例，选择**更多** \> **实例设置** \> **授予/收回 RAM 角色**。
5.  **操作类型**选择**授予**，在已有**RAM 角色**中选择其他实例RAM角色，单击**确定**即可更换当前RAM角色。

## 步骤六：（可选）获取临时授权Token {#Token .section}

您可以获得实例RAM角色的临时授权Token，该临时授权Token可以执行实例RAM角色的权限和资源，并且该临时授权Token会自动周期性地更新。示例：

1.  远程连接并登录到ECS实例。
2.  检索名为EcsRamRoleDocumentTesting的实例RAM角色的临时授权Token：
    -   Linux实例：执行命令`curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting`。
    -   Windows实例：参见[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
3.  获得临时授权Token。返回示例如下：

    ``` {#codeblock_cyl_4pu_6h8}
    {
    "AccessKeyId" : "XXXXXXXXX",
    "AccessKeySecret" : "XXXXXXXXX",
    "Expiration" : "2017-11-01T05:20:01Z",
    "SecurityToken" : "XXXXXXXXX",
    "LastUpdated" : "2017-10-31T23:20:01Z",
    "Code" : "Success"
    }
    ```


## 步骤七： （可选）授权RAM用户使用实例RAM角色 {#Authorize .section}

**说明：** 当您授权RAM用户使用实例RAM角色时，您必须授权RAM用户对该实例RAM角色的**PassRole**权限。其中，**PassRole**决定该RAM用户能否直接执行角色策略赋予的权限。

登录[RAM控制台](https://ram.console.aliyun.com/#/overview)，参见[为 RAM 用户授权](../../../../../cn.zh-CN/快速入门/为 RAM 用户授权.md#)完成授权，授权策略如下所示：

``` {#codeblock_if9_f3f_efp}
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

其中，\[ECS RAM Action\]表示可授权RAM用户的权限，请参见[鉴权规则](../cn.zh-CN/API参考/鉴权规则.md#)。

## 相关文档 {#section_bxr_pwt_xdb .section}

-   您也可以[通过API使用实例RAM角色](cn.zh-CN/安全/实例RAM角色/通过API使用实例RAM角色.md#)。
-   您也许想[借助于实例RAM角色访问其他云产品](../cn.zh-CN/最佳实践/借助于实例RAM角色访问其他云产品.md#)。

