# 为Linux实例开通IPv6服务 {#concept_mrr_fsv_yfb .concept}

本文描述了如何在Linux实例系统内查询IPv6服务状态、开通IPv6服务或者禁用IPv6服务。

## 背景信息 {#Background .section}

云服务器ECS支持创建带有IPv6地址的实例。更多详情，请参见 [ECS实例支持IPv6协议](../../../../../cn.zh-CN/产品简介/网络和安全性/IPv6.md#) 和 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)。

## 前提条件 {#section_ayv_wp2_lgb .section}

您已经在 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#) 或已经 [为已有实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为已有实例分配IPv6地址.md#)，但未开通IPv6服务。

## 检查实例是否已开启IPv6服务 {#section_gsy_3sv_yfb .section}

1.  远程连接实例。

2.  运行命令 `ip addr | grep inet6` 或者 `ifconfig | grep inet6` ：

    -   若返回 `inet6` 相关内容，表示实例已成功开启IPv6服务。您可以跳过本章内容。

    -   若实例未开启IPv6服务，请根据下文开启服务。


## 为Aliyun Linux实例开启IPv6服务 {#section_csy_3sv_yfb .section}

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


## 为CentOS 6或7实例开启IPv6服务 {#section_spb_y5v_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/modprobe.d/disable_ipv6.conf`，将 `options ipv6 disable=1` 修改为 `options ipv6 disable=0`。

3.  （CentOS 6）运行 `vi /etc/sysconfig/network`，将 `NETWORKING_IPV6=no` 修改为 `NETWORKING_IPV6=yes` 后保存退出。

4.  （CentOS 6）运行以下命令：

    ```
    modprobe ipv6 -r
    modprobe ipv6
    ```

5.  运行 `lsmod | grep ipv6`，当返回以下内容时，表明IPv6模块已经成功加载：

    ```
    ipv6                  xxxxx  8
    ```

    **说明：** 第三列参数值不能为0，否则您需要重新设置IPv6服务。

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


## 为CoreOS 14或17实例开启IPv6服务 {#section_y3j_hfw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /usr/share/oem/grub.cfg`，删除 `ipv6.disable=1`。

3.  重启实例。


## 为Debian 8或9实例开启IPv6服务 {#section_xsg_mfw_yfb .section}

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

## 为FreeBSD 11实例开启IPv6服务 {#section_fcb_cgw_yfb .section}

1.  远程连接实例。

2.  运行 `vi /etc/rc.conf`，添加 `ipv6_activate_all_interfaces="YES"` 。

3.  运行 `/etc/netstart restart` 重启网络。


## 为OpenSUSE 42实例开启IPv6服务 {#section_e3z_ggw_yfb .section}

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


## 为SUSE 11或12实例开启IPv6服务 {#section_ybh_kgw_yfb .section}

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


## 为Ubuntu 14或16实例开启IPv6服务 {#section_bzn_vgw_yfb .section}

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


## 禁用IPv6服务 {#section_h5v_dhw_yfb .section}

1.  远程连接实例。

2.  参阅上文如何为不同发行平台镜像开启IPv6服务，并作反向配置。


## 后续步骤 {#section_xtk_3nx_yfb .section}

您需要为Linux实例配置IPv6地址：

-   [手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例手动配置IPv6地址.md#)。
-   [自动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows和Linux实例自动配置IPv6地址.md#)。

