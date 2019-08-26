# 步骤4：配置IPv6地址 {#concept_prn_qbx_wgb .concept}

本文描述了如何为 Linux 实例自动配置 IPv6 地址和手动配置 IPv6 地址，推荐您使用更高效的自动配置工具配置 IPv6 地址。

## 自动配置 IPv6 地址 {#section_smq_tyw_yfb .section}

**背景信息**

ecs-util-ipv6 能为已分配 IPv6 地址的 ECS 实例一键配置 IPv6 地址，或者为没有分配 IPv6 地址的 ECS 实例一键清理 IPv6 配置。

**使用限制** 

-   ecs-util-ipv6 工具仅适用于 VPC 类型实例，依赖实例元数据服务，使用前请勿将网络禁用或者将相关出口 IP 端口（100.100.100.200:80）禁用。详情请参见[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
-   ecs-util-ipv6 工具运行时会自动重启网卡、网络服务，短时间内网络可能会不可用，请慎重执行。

**执行方式**

下载对应系统版本工具到目标系统，赋予执行权限后使用管理员权限执行：

``` {#codeblock_y1r_2b4_dly}
chmod +x ./ecs-utils-ipv6
./ecs-utils-ipv6
```

**执行效果**

如果当前 ECS 已绑定 IPv6 地址，则会自动配置；否则会自动清理原有 IPv6 地址配置。

**命令行参数** 

``` {#codeblock_oan_n3e_5qy}
ecs-utils-ipv6 --help           # show usage
ecs-utils-ipv6 --version        # show version
ecs-utils-ipv6                  # auto config all dev ipv6
ecs-utils-ipv6 --static [dev] [ip6s] [prefix_len] [gw6] # config dev static ipv6
e.g. ecs-utils-ipv6 --static eth0
       ecs-utils-ipv6 --static eth0 xxx::x1 64 xxx::x0
       ecs-utils-ipv6 --static eth0 "xxx::x1 xxx:x2 xxx:x3" 64 xxx::x0
ecs-utils-ipv6 --enable         # enable ipv6
ecs-utils-ipv6 --disable        # disable ipv6
```

可以开启、禁用、手动配置、自动配置（默认）IPv6。

``` {#codeblock_me4_f5b_9uf}
./ecs-utils-ipv6                 #默认可不带参数，自动配置多网卡多IPv6
./ecs-utils-ipv6 --enable    #开启IPv6
./ecs-utils-ipv6 --disable    #禁用IPv6
./ecs-utils-ipv6 --static <dev>      #自动配置网卡IPv6
./ecs-utils-ipv6 --static <dev> <ip6s> <prefix_len> <gw6>     #手动配置网卡IPv6，支持多IPv6，请用""包含，多个IPv6用空格隔开
```

**下载地址** 

|系列|发行版|下载地址|
|:-|:--|:---|
|RHEL| -   CentOS 5/6/7
-   Red Hat 5/6/7
-   Aliyun Linux 17

 |[下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6)|
|Debian| -   Ubuntu 14/16
-   Debian/8/9

 |[下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/debian/ecs-utils-ipv6)|
|SLES| -   SUSE 11/12
-   OpenSUSE 42

 |[下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/sles/ecs-utils-ipv6)|
|CoreOS|CoreOS 14/17|[下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/coreos/ecs-utils-ipv6)|
|FreeBSD|FreeBSD 11|[下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/freebsd/ecs-utils-ipv6)|

**自动化脚本示例**

对于需要自动化配置 IPv6 实例的需求，比如大批量配置，建议您使用[云助手](../../../../cn.zh-CN/部署与运维/云助手/云助手概述.md#)或者[实例自定义数据](cn.zh-CN/实例/管理实例/使用实例自定义数据/生成实例自定义数据.md#)配合脚本的方式来调用。以下为脚本示例（假设是RHEL系列，Bash Shell 脚本）。

``` {#codeblock_k26_35u_2wn}
#!/bin/sh
install_dir=/usr/sbin
install_path="$install_dir"/ecs-utils-ipv6
if [ ! -f "$install_path" ]; then
    tool_url="http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6"
    # download the tool
    if ! wget "$tool_url" -O "$install_path"; then
        echo "[Error] download tool failed, code $?"
        exit "$?"
    fi
fi
# chmod the tool
if ! chmod +x "$install_path"; then
    echo "[Error] chmod tool failed, code $?"
    exit "$?"
fi
# run the tool
"$install_path"
```

## 手动配置 IPv6 地址 {#section_ylc_1vg_ygb .section}

**检查实例是否已开启 IPv6 服务**

1.  远程连接实例。
2.  运行命令 `ip addr | grep inet6` 或者 `ifconfig | grep inet6` ：
    -   若返回 `inet6` 相关内容，表示实例已成功开启 IPv6 服务。您可以跳过本章内容。
    -   若实例未开启 IPv6 服务，请根据下文开启服务。

**开启 IPv6 服务**

Aliyun Linux 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/default/grub`，删除内核参数 `ipv6.disable=1` 后保存退出。
3.  运行 `vi /boot/grub/grub.cfg`，删除内核参数 `ipv6.disable=1` 后保存退出。
4.  重启实例。
5.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0` 后保存退出。
6.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_x2l_guq_jj4}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

7.  运行 `sysctl -p` 使配置生效。

CentOS 6 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0` 后保存退出。
3.  运行 `vi /etc/sysconfig/network`，将 `NETWORKING_IPV6=no` 修改为 `NETWORKING_IPV6=yes` 后保存退出。
4.  运行以下命令：

    ``` {#codeblock_09y_wys_j4c}
    modprobe ipv6 -r
    modprobe ipv6
    ```

5.  运行 `lsmod | grep ipv6`，当返回以下内容时，表明 IPv6 模块已经成功加载：

    ``` {#codeblock_tmr_oco_n8w}
    ipv6                  xxxxx  8
    ```

    **说明：** 第三列参数值不能为 0，否则您需要重新设置 IPv6 服务。

6.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_e2i_l2e_ogj}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

7.  运行 `sysctl -p` 使配置生效。

CentOS 7 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0` 后保存退出。
3.  运行 `vi /etc/sysconfig/network`，将 `NETWORKING_IPV6=no` 修改为 `NETWORKING_IPV6=yes` 后保存退出。
4.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_rpc_19y_t9v}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

5.  运行 `sysctl -p` 使配置生效。

CoreOS 14 或 17 操作步骤

1.  远程连接实例。
2.  运行 `vi /usr/share/oem/grub.cfg`，删除 `ipv6.disable=1` 后保存退出。
3.  重启实例。

Debian 8 或 9 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/default/grub`，删除 `ipv6.disable=1` 后保存退出。
3.  运行 `vi /boot/grub/grub.cfg`，删除 `ipv6.disable=1` 后保存退出。
4.  重启实例。
5.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_wk5_vbp_5qp}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

6.  运行 `sysctl -p` 使配置生效。

FreeBSD 11 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/rc.conf`，添加 `ipv6_activate_all_interfaces="YES"` 后保存退出。
3.  运行 `/etc/netstart restart` 重启网络。

OpenSUSE 42 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_it3_tqt_yqy}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

3.  运行 `sysctl -p` 使配置生效。

SUSE 11 或 12 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/modprobe.d/50-ipv6.conf`，删除 `install ipv6 /bin/true` 后保存退出。
3.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_iiw_c7i_6rw}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

4.  运行 `sysctl -p` 使配置生效。

Ubuntu 14 或 16 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ``` {#codeblock_lz0_w17_oef}
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

3.  运行 `sysctl -p` 使配置生效。

**查询实例的 IPv6 地址**

您可以通过控制台和实例元数据查看实例分配的 IPv6 地址。

-   控制台：请参见[分配 IPv6 地址](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤2：分配IPv6地址.md#)。
-   实例元数据：通过以下元数据项获取 IPv6 地址。详情请参见[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
    -   IPv6 地址：network/interfaces/macs/\[mac\]/ipv6s
    -   IPv6 网关：network/interfaces/macs/\[mac\]/ipv6-gateway
    -   IPv6 虚拟交换机 CIDR 地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block

**手动配置 IPv6 地址**

Aliyun Linux 17、CentOS 6/7 和 Red Hat 6/7 操作步骤

1.  远程连接实例。
2.  运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0`打开网卡配置文件，`eth0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
    -   单 IPv6 地址：

        ``` {#codeblock_kt9_jsi_epo}
        IPV6INIT=yes
        IPV6ADDR=<IPv6地址>/<子网前缀长度>
        IPV6_DEFAULTGW=<IPv6网关>
        ```

    -   多 IPv6 地址：

        ``` {#codeblock_qdb_05k_tvt}
        IPV6INIT=yes
        IPV6ADDR=<IPv6地址>/<子网前缀长度>
        IPV6ADDR_SECONDARIES="<IPv6地址1>/<子网前缀长度> <IPv6地址2>/<子网前缀长度>"
        IPV6_DEFAULTGW=<IPv6网关>
        ```

        **说明：** 为区分单个 IPv6 与多个 IPv6 地址，请在 IPV6ADDR\_SECONDARIES 参数中使用列表格式表达多地址格式，使用半角引号（`"`）包含地址，并用空格隔开。

3.  重启网络服务：运行 `service network restart` 或 `systemctl restart network`。

Debian/8/9 和 Ubuntu 14/16 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/network/interfaces` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
    -   单 IPv6 地址：

        ``` {#codeblock_9lg_b8o_i97}
        auto eth0
        iface eth0 inet6 static
        address <IPv6地址>
        netmask <子网前缀长度>
        gateway <IPv6网关>
        ```

    -   多 IPv6 地址：

        ``` {#codeblock_7pq_dcu_da8}
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

        **说明：** 为区分单个 IPv6 与多个 IPv6 地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

3.  重启网络服务：运行 `service network restart` 或 `systemctl restart networking`。

OpenSUSE 42 和 SUSE Linux 11/12 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/sysconfig/network/ifcfg-eth0` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
    -   单 IPv6 地址：

        ``` {#codeblock_5rc_nwa_gmw}
        IPADDR_0=<IPv6地址>
        PREFIXLEN_0=<子网前缀长度>
        ```

    -   多 IPv6 地址：

        ``` {#codeblock_ifj_ops_bbt}
        IPADDR_0=<IPv6地址>
        PREFIXLEN_0=<子网前缀长度>
        
        IPADDR_1=<IPv6地址1>
        PREFIXLEN_1=<子网前缀长度>
        
        IPADDR_2=<IPv6地址2>
        PREFIXLEN_2=<子网前缀长度>
        ```

        **说明：** 为区分单个 IPv6 与多个 IPv6 地址，请使用不用的 IPADDR\_N 和 PREFIXLEN\_N 重复添加地址信息。

3.  运行 `vi /etc/sysconfig/network/routes` 打开路由配置文件，添加配置项：

    ``` {#codeblock_s5s_94i_qli}
    default <IPv6网关> - -
    ```

4.  重启网络服务：运行 `service network restart` 或 `systemctl restart networking`。

CoreOS 14/17 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/systemd/network/10-eth0.network` 打开网卡配置文件，`eth0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
    -   单 IPv6 地址：

        ``` {#codeblock_15m_8p4_okp}
        [Address]
        Address=<IPv6地址>/<子网前缀长度>
        [Route]
        Destination=::/0
        Gateway=<IPv6网关>
        ```

    -   多 IPv6 地址：

        ``` {#codeblock_1vw_32u_92g}
        [Address]
        Address=<IPv6地址1>/<子网前缀长度>
        [Address]
        Address=<IPv6地址2>/<子网前缀长度>
        [Route]
        Destination=::/0
        Gateway=<IPv6网关>
        ```

        **说明：** 为区分单个 IPv6 与多个 IPv6 地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

3.  重启网络服务：运行 `systemctr restart systemd-networkd`。

FreeBSD 11 操作步骤

1.  远程连接实例。
2.  运行 `vi /etc/rc.conf` 打开网卡配置文件，`vtnet0` 为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
    -   单 IPv6 地址：

        ``` {#codeblock_nfr_u6l_17a}
        ipv6_ifconfig_vtnet0="<IPv6地址>"
        ipv6_defaultrouter="<IPv6网关>"
        ```

    -   多 IPv6 地址：

        ``` {#codeblock_grw_pff_eev}
        ipv6_ifconfig_vtnet0="<IPv6地址1>"
        ipv6_ifconfig_vtnet0="<IPv6地址2>"
        ipv6_defaultrouter="<IPv6网关>"
        ```

        **说明：** 为区分单个 IPv6 与多个 IPv6 地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

3.  重启网络服务：运行 `/etc/netstart restart`。

