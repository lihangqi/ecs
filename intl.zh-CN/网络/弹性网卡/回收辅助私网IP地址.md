# 回收辅助私网IP地址 {#concept_csv_ncm_ggb .concept}

如果您的弹性网卡不再需要辅助私网IP地址，您可以回收弹性网卡上已分配的一个或多个辅助私网IP地址。您无法回收主私网IP地址。

## 使用限制 {#section_rk2_ddm_ggb .section}

-   您无法回收弹性网卡的主私网IP地址。
-   单个专有网络VPC类型的安全组内的私网IP个数不能超过2000（主网卡和辅助网卡共享此配额）。

## 前提条件 {#section_bq5_gdm_ggb .section}

-   弹性网卡已分配辅助私网IP地址。
-   弹性网卡必须处于**可用**（`Available`）或者**已绑定**（`InUse`）状态。
-   回收主网卡上分配的多个辅助私网IP地址时，主网卡附加的实例必须处于**运行中**（`Running`）或者**已停止**（`Stopped`）状态。

## 操作步骤 {#section_2f2_npr_8y7 .section}

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**网络与安全** \> **弹性网卡**。
3.  在顶部状态栏处，选择地域。
4.  在网卡列表页面，找到目标弹性网卡，在**操作**列，单击**管理辅助私网IP**。
5.  在管理辅助私网IP页面，单击**取消分配**。可连续单击，表示取消分配多个辅助私网IP地址。
6.  单击**修改**。

相关API：[UnassignPrivateIpAddresses](../intl.zh-CN/API参考/弹性网卡/UnassignPrivateIpAddresses.md#)

## 相关操作 {#section_bg2_xmp_3gb .section}

如果您想提升实例的利用率或实现故障转移，您可以在一张弹性网卡上[分配多个辅助私网IP地址](intl.zh-CN/网络/弹性网卡/分配辅助私网IP地址.md#)。

