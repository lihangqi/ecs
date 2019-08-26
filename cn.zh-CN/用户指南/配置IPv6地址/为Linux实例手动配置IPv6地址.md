# 为Linux实例手动配置IPv6地址 {#concept_qs3_zvw_yfb .concept}

本文描述了如何通过添加内核参数为Linux实例手动配置IPv6 地址。

## 前提条件 {#section_z1h_2ww_yfb .section}

您已经为实例开通了IPv6服务。更多详情，请参见 [为Linux实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例开通IPv6服务.md#)。

## 步骤 1：查询实例的IPv6地址 {#section_nw4_lww_yfb .section}

您可以通过控制台和实例元数据查看实例分配的IPv6地址。

控制台操作请参阅 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)。

实例元数据请参阅 [实例元数据](cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)，并通过以下元数据项获取 IPv6 地址：

-   IPv6地址：network/interfaces/macs/\[mac\]/ipv6s

-   IPv6网关：network/interfaces/macs/\[mac\]/ipv6-gateway

-   IPv6虚拟交换机CIDR地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block


## 步骤 2：手动配置IPv6地址 {#section_smq_tyw_yfb .section}

**Aliyun Linux 17、CentOS 6/7和Red Hat 6/7操作步骤**

1.  远程连接实例。

2.  运行 `vi /etc/sysconfig/network-scripts/ifcfg-eth0` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：

    -   单IPv6地址：

```
IPV6INIT=yes
IPV6ADDR=<IPv6地址>/<子网前缀长度>
IPV6_DEFAULTGW=<IPv6网关>
```

    -   多IPv6地址：

```
IPV6INIT=yes
IPV6ADDR=<IPv6地址>/<子网前缀长度>
IPV6ADDR_SECONDARIES="<IPv6地址1>/<子网前缀长度> <IPv6地址2>/<子网前缀长度>"
IPV6_DEFAULTGW=<IPv6网关>
```

        **说明：** 为区分单个IPv6与多个IPv6地址，请在 IPV6ADDR\_SECONDARIES 参数中使用列表格式表达多地址格式，使用半角引号（`"`）包含地址，并用空格隔开。

3.  重启网络服务：运行 `service network restart` 或 `systemctl restart network`。


**Debian/8/9和Ubuntu 14/16操作步骤**

1.  远程连接实例。

2.  运行 `vi /etc/network/interfaces` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：

    -   单IPv6地址：

```
auto eth0
iface eth0 inet6 static
address <IPv6地址>
netmask <子网前缀长度>
gateway <IPv6网关>
```

    -   多IPv6地址：

```
auto eth0
iface eth0 inet6 static
address <IPv6地址>
netmask <子网前缀长度>
gateway <IPv6网关>

auto eth0:0
iface eth0:0 inet6 static
address <IPv6地址1>
netmask <子网前缀长度>
gateway <IPv6网关>

auto eth0:1
iface eth0:1 inet6 static
address <IPv6地址2>
netmask <子网前缀长度>
gateway <IPv6网关>
```

        **说明：** 为区分单个IPv6与多个IPv6地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

3.  重启网络服务：运行 `service network restart` 或 `systemctl restart networking`。


**OpenSUSE 42和SUSE Linux 11/12操作步骤**

1.  远程连接实例。

2.  运行 `vi /etc/sysconfig/network/ifcfg-eth0` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：

    -   单IPv6地址：

```
IPADDR_0=<IPv6地址>
PREFIXLEN_0=<子网前缀长度>
```

    -   多IPv6地址：

```
IPADDR_0=<IPv6地址>
PREFIXLEN_0=<子网前缀长度>

IPADDR_1=<IPv6地址1>
PREFIXLEN_1=<子网前缀长度>

IPADDR_2=<IPv6地址2>
PREFIXLEN_2=<子网前缀长度>
```

        **说明：** 为区分单个IPv6与多个IPv6地址，请使用不用的 IPADDR\_N 和 PREFIXLEN\_N 重复添加地址信息。

3.  运行 `vi /etc/sysconfig/network/routes` 打开路由配置文件，添加配置项：

    ```
    default <IPv6网关> - -
    ```

4.  重启网络服务：运行 `service network restart` 或 `systemctl restart networking`。


**CoreOS 14/17操作步骤**

1.  远程连接实例。

2.  运行 `vi /etc/systemd/network/10-eth0.network` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：

    -   单IPv6地址：

```
[Address]
Address=<IPv6地址>/<子网前缀长度>
[Route]
Destination=::/0
Gateway=<IPv6网关>
```

    -   多IPv6地址：

```
[Address]
Address=<IPv6地址1>/<子网前缀长度>
[Address]
Address=<IPv6地址2>/<子网前缀长度>
[Route]
Destination=::/0
Gateway=<IPv6网关>
```

        **说明：** 为区分单个IPv6与多个IPv6地址，您只需重复添加地址信息即可。

3.  重启网络服务：运行 `systemctr restart systemd-networkd`。


**FreeBSD 11操作步骤**

1.  远程连接实例。

2.  运行 `vi /etc/rc.conf` 打开网卡配置文件，`vtnet0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：

    -   单IPv6地址：

```
ipv6_ifconfig_vtnet0="<IPv6地址>"
ipv6_defaultrouter="<IPv6网关>"
```

    -   多IPv6地址：

```
ipv6_ifconfig_vtnet0="<IPv6地址1>"
ipv6_ifconfig_vtnet0="<IPv6地址2>"
ipv6_defaultrouter="<IPv6网关>"
```

        **说明：** 为区分单个IPv6与多个IPv6地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

3.  重启网络服务：运行 `/etc/netstart restart`。


## 相关操作 {#section_sh5_pr2_lgb .section}

-   如果您不希望手动配置多个IPv6地址，您可以 [为Linux实例自动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows和Linux实例自动配置IPv6地址.md#)。
-   如果您创建的是Windows实例，您可以 [为Windows实例手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例手动配置IPv6地址.md#)。
-   如果您的实例不需要IPv6地址，您可以 [删除实例的IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/删除实例的IPv6地址.md#)。删除IPv6地址后，您仍然可以使用IPv4地址。

