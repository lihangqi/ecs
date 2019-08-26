# 为Linux实例配置IPv6服务 {#concept_mrr_fsv_yfb .concept}

本文描述了如何在 Linux 实例系统内查询 IPv6 服务状态、配置 IPv6 服务或者禁用 IPv6 服务。

## 背景信息 {#Background .section}

云服务器 ECS 支持创建带有 IPv6 地址的实例。更多详情，请参阅 [ECS 实例支持 IPv6 协议](../../../../cn.zh-CN/产品简介/网络和安全性/IPv6.md#) 和 [创建实例时配置 IPv6 地址](cn.zh-CN/用户指南/配置IPv6地址/创建实例时配置IPv6地址.md#)。

若您的实例已经分配了 IPv6 地址但未开启服务模块，可以根据本文描述在实例系统内完成操作。

## 检查实例是否已开启 IPv6 服务 {#section_gsy_3sv_yfb .section}

1.  远程连接实例。

2.  运行命令 `ip addr | grep inet6` 或者 `ifconfig | grep inet6` ：

    -   若返回 `inet6` 相关内容，代表实例已成功开启 IPv6 服务。

    -   若实例还未开启 IPv6 服务，请根据下文描述操作。


## 为 Aliyun Linux 实例开启 IPv6 服务 {#section_csy_3sv_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/default/grub`，删除内核参数 `ipv6.disable=1` 后保存退出。

3.  运行 `vi /boot/grub/grub.cfg`，删除内核参数 `ipv6.disable=1` 后保存退出。

4.  重启实例。

5.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0`。

6.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

7.  运行 `sysctl -p` 使配置生效。


## 为 CentOS 6 或 7 实例开启 IPv6 服务 {#section_spb_y5v_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0`。

3.  （CentOS 6）运行 `vi /etc/sysconfig/network`，将 `NETWORKING_IPV6=no` 修改为 `NETWORKING_IPV6=yes` 后保存退出。

4.  （CentOS 6）运行以下命令：

    ```
    modprode ipv6 -r
    modprode ipv6
    ```

5.  运行 `lsmod | grep ipv6`，当返回以下内容时，表明 IPv6 模块已经成功加载：

    ```
    ipv6                  xxxxx  8
    ```

    **说明：** 第三列参数值不能为 0，否则您需要重新设置 IPv6 服务。

6.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

7.  运行 `sysctl -p` 使配置生效。


## 为 CoreOS 14 或 17 实例开启 IPv6 服务 {#section_y3j_hfw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /usr/share/oem/grub.cfg`，删除 `ipv6.disable=1`。

3.  重启实例。


## 为 Debian 8 或 9 实例开启 IPv6 服务 {#section_xsg_mfw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/default/grub`，删除 `ipv6.disable=1`。

3.  运行 `vi /boot/grub/grub.cfg`，删除 `ipv6.disable=1`。

4.  重启实例。

5.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

6.  运行 `sysctl -p` 使配置生效。

## 为 FreeBSD 11 实例开启 IPv6 服务 {#section_fcb_cgw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/rc.conf`，添加 `ipv6_activate_all_interfaces="YES"` 。

3.  运行 `/etc/netstart restart` 重启网络。


## 为 OpenSUSE 42 实例开启 IPv6 服务 {#section_e3z_ggw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

3.  运行 `sysctl -p` 使配置生效。


## 为 SUSE 11 或 12 实例开启 IPv6 服务 {#section_ybh_kgw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/modprobe.d/50-ipv6.conf`，删除 `install ipv6 /bin/true`。

3.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

4.  运行 `sysctl -p` 使配置生效。


## 为 Ubuntu 14 或 16 实例开启 IPv6 服务 {#section_bzn_vgw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/sysctl.conf` 做如下修改：

    ```
    #net.ipv6.conf.all.disable_ipv6 = 1
    #net.ipv6.conf.default.disable_ipv6 = 1
    #net.ipv6.conf.lo.disable_ipv6 = 1
    
    net.ipv6.conf.all.disable_ipv6 = 0
    net.ipv6.conf.default.disable_ipv6 = 0
    net.ipv6.conf.lo.disable_ipv6 = 0
    ```

3.  运行 `sysctl -p` 使配置生效。


## 禁用 IPv6 服务 {#section_h5v_dhw_yfb .section}

1.  远程连接实例。

2.  参阅上文如何为不同发行平台镜像开启 IPv6 服务，并作反向配置。


## 下一步 {#section_xtk_3nx_yfb .section}

[为Linux实例配置静态IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例配置静态IPv6地址.md#)

