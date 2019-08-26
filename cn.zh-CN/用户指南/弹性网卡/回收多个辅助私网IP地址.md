# 回收多个辅助私网IP地址 {#concept_csv_ncm_ggb .concept}

如果您的弹性网卡不再需要辅助私网IP地址，您可以回收弹性网卡上已分配的多个辅助私网IP地址，您无法回收主私网IP地址。

## 使用限制 {#section_rk2_ddm_ggb .section}

-   目前回收多个辅助私网IP地址功能白名单开放，白名单申请请 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。
-   您无法回收主私网IP地址。
-   弹性网卡只能附加到VPC类型的ECS实例，实例与弹性网卡必须属于同一个VPC。
-   单个VPC类型的安全组内的私网IP个数不能超过2000（主网卡和辅助网卡共享此配额）。

## 前提条件 {#section_bq5_gdm_ggb .section}

-   弹性网卡已分配多个辅助私网IP地址。
-   弹性网卡必须处于 **可用**（`Available`）或者 **已绑定**（`InUse`）状态。
-   回收主网卡上分配的多个辅助私网IP地址时，主网卡附加的实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。

## 配置步骤 {#section_pzj_qcm_ggb .section}

1.  使用 [DescribeNetworkInterfaces](../../../../../cn.zh-CN/API参考/弹性网卡/DescribeNetworkInterfaces.md#) 接口查询分配的辅助私网IP地址。
2.  使用 [UnassignPrivateIpAddresses](../../../../../cn.zh-CN/API参考/弹性网卡/UnassignPrivateIpAddresses.md#) 接口回收辅助私网IP地址。

## 相关操作 {#section_bg2_xmp_3gb .section}

如果您想提升实例的利用率或实现故障转移，您可以在一张弹性网卡上 [分配多个辅助私网IP地址](cn.zh-CN/用户指南/弹性网卡/分配多个辅助私网IP地址.md#)。

