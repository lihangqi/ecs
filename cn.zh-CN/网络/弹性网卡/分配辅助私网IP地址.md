# 分配辅助私网IP地址 {#concept_ff2_hbk_ggb .concept}

您可以在一张弹性网卡上分配一个或多个辅助私网IP地址。通过使用多个私网IP地址，能提高ECS实例高利用率和实现负载故障时的流量转移。

## 应用场景 {#section_chq_2rk_ggb .section}

-   多应用场景

    如果您的ECS实例托管多个应用，您可以在弹性网卡上分配多个辅助私网IP地址。每个应用对外呈现一个独立的服务IP地址，提升实例的利用率。

-   故障转移

    当实例发生故障时，您可以重新[绑定弹性网卡](cn.zh-CN/网络/弹性网卡/绑定弹性网卡.md#)，将请求流量转移到其他备用实例上，实现故障转移。


## 使用限制 {#section_mwz_glk_ggb .section}

-   弹性网卡只能附加到专有网络VPC类型的ECS实例，实例与弹性网卡必须属于同一个专有网络VPC、同一台虚拟交换机、同一个可用区。
-   单台专有网络VPC类型的安全组内的私网IP地址个数不能超过2000，主网卡和辅助网卡共享此配额。
-   一张弹性网卡最多可以分配20个私网IP地址。
    -   弹性网卡的状态处于**可用**（`Available`）时，您最多可以分配10个私网IP地址。
    -   弹性网卡的状态处于**已绑定**（`InUse`）时，您可以分配的私网IP地址数与实例规格相关。更多详情，请参见[实例规格族](../cn.zh-CN/实例/实例规格族.md#)。
-   您的实例规格必须支持分配多个辅助私网IP。更多详情，请参见[实例规格族](../cn.zh-CN/实例/实例规格族.md#)或通过[DescribeInstanceTypes](../cn.zh-CN/API参考/实例/DescribeInstanceTypes.md#)接口查询。
-   在主网卡上分配多个辅助私网IP地址时，主网卡附加的实例必须处于**运行中**（`Running`）或者**已停止**（`Stopped`）状态。

## 分配辅助私网IP地址 {#section_bam_ihj_gsy .section}

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**网络与安全** \> **弹性网卡**。
3.  在顶部状态栏处，选择地域。
4.  在网卡列表页面，找到目标弹性网卡，在**操作**列，单击**管理辅助私网IP**。
5.  在管理辅助私网IP页面，单击**分配新 IP**。可连续单击，表示分配多个辅助私网IP地址。

    您可以手动输入辅助私网IP地址，取值在**IPv4 私网网段**内即可。如果您不输入IP值，系统会从**IPv4 私网网段**随机分配IP地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83258/156082565647047_zh-CN.png)

6.  单击**修改**。
7.  （可选）如果您选择了自动分配辅助私网IP地址，在**操作**列，单击**管理辅助私网IP**查看系统已分配的辅助私网IP地址，用于实例配置的操作步骤中。
8.  （可选）如果您操作的弹性网卡还未绑定到ECS实例，请参见[绑定弹性网卡](cn.zh-CN/网络/弹性网卡/绑定弹性网卡.md#)完成绑定。

相关API：[AssignPrivateIpAddresses](../cn.zh-CN/API参考/弹性网卡/AssignPrivateIpAddresses.md#)

## 为Windows实例配置辅助私网IP地址 {#section_y4b_krk_ggb .section}

1.  远程登录实例。具体方法可参见[连接方式导航](../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
2.  打开网络和共享中心。
3.  单击**更改适配器设置**。
4.  双击当前网络连接名，单击**属性**。
5.  左键双击**Internet 协议版本4（TCP/IPv4）**。
6.  选择**使用下面的IP地址**，单击**高级**。
7.  在**IP 地址**栏中，单击**添加**，输入已分配的**IP 地址**，自行填写**子网掩码**。

    您可以为同一网卡适配器重复添加多个IP地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83258/156082565747049_zh-CN.png)

8.  单击**确定**。

## 为Linux实例配置辅助私网IP地址 {#section_b2x_hlb_3gb .section}

1.  远程登录实例。具体方法可参见[连接方式导航](../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
2.  根据您的实例操作系统选择配置辅助私网IP地址的方式。

    以下步骤均以主网卡eth0为操作示范，如果您使用的是辅助网卡，请根据实际情况修改网卡标识符。

    -   RHEL系列：CentOS 6/7、Red Hat 6/7、Aliyun Linux 17
        1.  运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0:0`命令打开网络配置文件，添加如下配置项。

            ``` {#codeblock_tr9_8mc_60j}
            DEVICE=eth0:0
            TYPE=Ethernet
            BOOTPROTO=static
            ONBOOT=yes
            IPADDR=<IPv4地址1>
            NETMASK=<IPv4掩码>
            GATEWAY=<IPv4网关>
            ```

            若有多IP，运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0:1`命令打开网络配置文件，添加如下配置项。

            ``` {#codeblock_07v_692_ihz}
            DEVICE=eth0:1
            TYPE=Ethernet
            BOOTPROTO=static
            ONBOOT=yes
            IPADDR=<IPv4地址2>
            NETMASK=<IPv4掩码>
            GATEWAY=<IPv4网关>
            ```

        2.  运行`service network restart`或`systemctl restart network`命令重启网络服务。
    -   Debian系列：Ubuntu 14/16、Debian/8/9
        1.  运行`vi /etc/network/interfaces`命令打开网络配置文件，添加如下配置项。

            ``` {#codeblock_3m7_8te_y3m}
            auto eth0:0
            iface eth0:0 inet static
            address <IPv4地址1>
            netmask <IPv4掩码>
            gateway <IPv4网关>
            
            auto eth0:1
            iface eth0:1 inet static
            address  <IPv4地址2>
            netmask <IPv4掩码>
            gateway <IPv4网关>
            ```

        2.  运行`service networking restart`或`systemctl restart networking`命令重启网络服务。
    -   SLES系列：SUSE 11/12、OpenSUSE 42
        1.  运行`vi /etc/sysconfig/network/ifcfg-eth0`命令打开网络配置文件，添加如下配置项：

            ``` {#codeblock_uon_675_v61}
            IPADDR_0=<IPv4地址1>
            NETMASK_0=<子网前缀长度>
            LABEL_0='0'
            
            IPADDR_1=<IPv4地址2>
            NETMASK_1=<子网前缀长度>
            LABEL_1='1'
            ```

        2.  运行`service network restart`或`systemctl restart network`命令重启网络服务。

## 相关操作 {#section_aqz_tlm_ggb .section}

如果您的弹性网卡不需要多个辅助私网IP地址，您可以[回收多个辅助私网IP地址](cn.zh-CN/网络/弹性网卡/回收辅助私网IP地址.md#)。

