# 分配多个辅助私网IP地址 {#concept_ff2_hbk_ggb .concept}

您可以在一张弹性网卡上分配多个辅助私网IP地址。

## 应用场景 {#section_chq_2rk_ggb .section}

-   实例高利用率

    如果您的服务器托管多个应用，您可以在弹性网卡上分配多个辅助私网IP地址，提升实例的利用率，每个应用对外呈现一个独立的服务IP地址。

-   故障转移

    当实例发生故障时，您可以将流量快速转移到其他备用实例的IP地址上，实现故障转移。


## 使用限制 {#section_mwz_glk_ggb .section}

-   目前分配多个辅助私网IP地址功能白名单开放，白名单申请请 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。
-   弹性网卡只能附加到VPC类型的ECS实例，实例与弹性网卡必须属于同一个VPC。
-   单个VPC类型的安全组内的私网IP地址个数不能超过2000（主网卡和辅助网卡共享此配额）。
-   一张弹性网卡最多可以分配20个私网IP地址。
    -   弹性网卡的状态处于 **可用**（`Available`）时，最多可以分配10个私网IP地址。
    -   弹性网卡的状态处于 **已绑定**（`InUse`）时，可以分配的私网IP地址数与实例规格相关。详细信息，请参见 [实例规格族](../../../../../cn.zh-CN/实例/选择实例规格/实例规格族汇总.md#)。

## 前提条件 {#section_mk2_n4k_ggb .section}

-   您的实例规格必须支持分配多个辅助私网IP。支持分配多个辅助私网IP地址的实例规格可通过 [DescribeInstanceTypes](../../../../../cn.zh-CN/API参考/实例/DescribeInstanceTypes.md#) 接口查询。
-   弹性网卡必须处于 **可用**（`Available`）或者 **已绑定**（`InUse`）状态。
-   在主网卡上分配多个辅助私网IP地址时，主网卡附加的实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。

## 为Windows实例分配多个辅助私网IP地址 {#section_y4b_krk_ggb .section}

1.  打开 网络和共享中心。
2.  单击 **更改适配器设置**。
3.  双击当前网络连接名，单击 **属性**。
4.  双击 **Internet 协议版本4（TCP/IPv4）**。
5.  点选 **使用下面的IP地址**，单击 **高级**。
6.  单击 **添加**，输入分配的IP地址和子网掩码。您可以重复添加多个IP地址。
7.  单击 **确定**。

## 为Linux实例分配多个辅助私网IP地址 {#section_b2x_hlb_3gb .section}

1.  使用 [AssignPrivateIpAddresses](../../../../../cn.zh-CN/API参考/弹性网卡/AssignPrivateIpAddresses.md#) 接口来分配多个辅助私网IP地址。
2.  使用 [DescribeNetworkInterfaces](../../../../../cn.zh-CN/API参考/弹性网卡/DescribeNetworkInterfaces.md#) 接口查询分配的辅助私网IP地址。
3.  [连接ECS实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)。
4.  配置已分配的IP地址。

    |发行版|适用版本|操作步骤|
    |:--|:---|:---|
    |RHEL系列|     -   CentOS 6/7
    -   Red Hat 6/7
    -   Aliyun Linux 17
 |     1.  假设网卡是eth0，通过`vi /etc/sysconfig/network-scripts/ifcfg-eth0:0`命令打开网络配置文件，添加如下配置项：

        ```
DEVICE=eth0:0
TYPE=Ethernet
BOOTPROTO=static
ONBOOT=yes
IPADDR=<IPv4地址1>
NETMASK=<IPv4掩码>
GATEWAY=<IPv4网关>
        ```

若有多IP，通过`vi /etc/sysconfig/network-scripts/ifcfg-eth0:1`命令打开网络配置文件，添加如下配置项：

        ```
DEVICE=eth0:1
TYPE=Ethernet
BOOTPROTO=static
ONBOOT=yes
IPADDR=<IPv4地址2>
NETMASK=<IPv4掩码>
GATEWAY=<IPv4网关>
        ```

    2.  通过`service network restart`或`systemctl restart network`命令重启服务。
 |
    |Debian系列|     -   Ubuntu 14/16
    -   Debian/8/9
 |     1.  假设网卡是eth0，通过`vi /etc/network/interfaces`命令打开网络配置文件，添加如下配置项：

        ```
auto eth0:0
iface eth0:0 inet static
address <IPv4地址1>
netmask <IPv4掩码>
gateway <IPv6网关>

auto eth0:1
iface eth0:1 inet static
address  <IPv4地址2>
netmask <IPv4掩码>
gateway <IPv4网关>
        ```

    2.  通过`service networking restart`或`systemctl restart networking`命令重启服务。
 |
    |SLES系列|     -   SUSE 11/12
    -   OpenSUSE 42
 |     1.  假设网卡是eth0，通过`vi /etc/sysconfig/network/ifcfg-eth0`命令打开网络配置文件，添加如下配置项：

        ```
IPADDR_0=<IPv4地址1>
NETMASK_0=<子网前缀长度>
LABEL_0='0'

IPADDR_1=<IPv4地址2>
NETMASK_1=<子网前缀长度>
LABEL_1='1'
        ```

    2.  通过`service network restart`或`systemctl restart network`命令重启服务。
 |


## 相关操作 {#section_aqz_tlm_ggb .section}

如果您的弹性网卡不需要多个辅助私网IP地址，您可以 [回收多个辅助私网IP地址](cn.zh-CN/网络/弹性网卡/回收多个辅助私网IP地址.md#)。

