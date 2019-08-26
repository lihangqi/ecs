# Configure an ENI {#concept_lyl_2kk_zdb .concept}

If your instance is running one of the following images, you do not have to configure the Elastic Network Interfaces \(ENI\) manually to have them recognized by the OS.

-   Centos 7.3 64-bit
-   Centos 6.8 64-bit
-   64-bit Windows Server 2016 data center Edition
-   Windows Server 2012 R2 Data Center Edition 64-bit64-bit Windows Server 2012 R2 data center Edition

If your instance is running none of the preceding images, and you want to attach an ENI to your instance, you must manually configure the ENI to be recognizable. If your instance does not use these images, however, if you want to attach a flexible network card to an instance, You need to manually configure the elastic network card. This document uses an instance running CentOS 7.2 64-bit as an example to introduce  how to configure an ENI to make the interface recognizable.

## Prerequisite {#section_oyn_hkk_zdb .section}

You have attached an elastic network card to an ECS instance.

## Procedure {#section_pyn_hkk_zdb .section}

To configure the ENI, follow these steps:

1.  Use the [DescribeNetworkInterfaces](../../../../reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md#) interface or log on to the ECS console to obtain the following attributes of the ENI: primary private IP address, subnet mask, the default route, and the MAC address. To obtain these attributes in the ECS console, follow these steps: MAC address. Do the following on the console.
    1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).Log on to the ECS Management Console.
    2.  Find a network interface, and obtain its primary private IP address, subnet mask, default route, and MAC address. Locate the primary and private IP address, mask address, default route,  and MAC for each network interface. Example:

        ```
        
        eth1 10.0.0.20/24 10.0.0.253 00: 16: 12: E7: 27
        eth2 10.0.0.21/24 10.0.0.253 00: 16: 12: 16: EC
        ```

2.  [Connect to the ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md).
3.  Run the command to generate the config file `cat /etc/sysconfig/network-scripts/ifcfg-[network interface name in the OS]`.

    **Note:** 

    -   Pay attention to the relation between network interface name in the OS and the MAC address.
    -   Pay attention to the relation between network interface name in the OS and the MAC address. The default route must be set to  `DEFROUTE=no` . Other editions must have the same configuration. Note that running the `ifup`command may change the active default route configuration after configuring the network interface.
    -   Example:

        ```
        # cat /etc/sysconfig/network-scripts/ifcfg-eth1 
        DEVICE=eth1
        BOOTPROTO=dhcp
        ONBOOT=yes
        TYPE=Ethernet
        USERCTL=yes
        PEERDNS=no
        IPV6INIT = No
        PERSISTENT_DHCLIENT = Yes
        HWADDR=00:16:3e:12:e7:27
        DEFROUTE=noDefroute = No
        ```

4.  Follow these steps to start the network interface:
    1.  Run the `ifup [network interface name in the OS]`  command to start the dhclient process, and initiate a  DHCP request. Example:

        ```
        # ifup eth1
        # ifup eth2
        ```

    2.  After a response is received, run the `ip a`  a command to check the  IP allocation on the network interfaces, which must match with the information displayed on the ECS console. Example:

        ```
        # ip a
        1: lo: mtu 65536 qdisc noqueue state UNKNOWN qlen 1
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host loInet 125.0.0.1/8 Scope host Lo
        valid_lft forever preferred_lft forever
        2: eth0: mtu 1500 qdisc pfifo_fast state UP qlen 10002: eth0: MTU 1500 qdisc glasstate up qlen 1000
        link/ether 00:16:3e:0e:16:21 brd ff:ff:ff:ff:ff:ff
        Inet 10.0.0.19/24 BRD glasscope Global Dynamic eth0
        valid_lft 31506157sec preferred_lft 31506157secValid_lft 31506157sec preferred_lft 31506157sec
        3: eth1: MTU 1500 qdisc glasstate up qlen 1000
        link/ether 00:16:3e:12:e7:27 brd ff:ff:ff:ff:ff:ff
        inet 10.0.0.20/24 brd 10.0.0.255 scope global dynamic eth1Inet 10.0.0.20/24 BRD glasscope Global Dynamic eth1
        Valid_lft 31525994sec preferred_lft 31525994sec
        4: eth2: MTU 1500 qdisc glasstate up qlen 1000
        Link/ether 00: 16: Rye: 12: 16: ec brd ff: FF: FF
        inet 10.0.0.21/24 brd 10.0.0.255 scope global dynamic eth2
        valid_lft 31526009sec preferred_lft 31526009sec
        ```

5.  Set the metric for each network interface in the route table. In this example, set the metric parameters of eth1 and eth2  as follows.

    ```
    eth1: gw: 10.0.0.253 metric: 1001
    eth2: gw: 10.0.0.253 metric: 1002
    ```

    1.  Run the following command to set the metric parameters.

        ```
        # Ip-4 route add default via glasdev eth1 metric 1001
        # ip -4 route add default via 10.0.0.253 dev eth2 metric 1002
        ```

    2.  Run the `route -n` command to check whether the configuration is successful or not. Example:

        ```
        # route -n
        Kernel IP routing table
        Destination Gateway Genmask Flags Metric Ref Use Iface
        0.0.0.0 10.0.0.253 0.0.0.0 UG 0 0 0 eth0
        0.0.0.0 10.0.0.253 0.0.0.0 UG 1001 0 0 eth1
        0.5.0.0 10.0.0.253 ug ub1002 0 0 eth2
        10.0.0.0 0.5.0.0 255.25.25.0 u 0 0 0 eth0
        10.0.0.0 0.0.0.0 255.255.255.0 U 0 0 0 eth1
        10.0.0.0 0.5.0.0 255.25.25.0 u 0 0 0 eth2
        169.254.0.0 0.0.0 255.0.0 U 1002 0 0 eth0
        169.254.0.0 0.0.0.0 255.255.0.0 U 1003 0 0 eth1
        169.254.0.0 0.0.0.0 255.255.0.0 U 1004 0 0 eth2169.254.0.0 0.0.0 255.0.0 U 1004 0 0 eth2
        ```

6.  Follow these steps to build a route table:

    **Note:** We recommend that you use the metric value as the route table name.

    1.  Run the command to build a route table.

        ```
        # ip -4 route add default via 10.0.0.253 dev eth1 table 1001
        # Ip-4 route add default via glasdev eth2 table 1002
        ```

    2.  Run the command to check whether the route table is built successfully or not.

        ```
        # ip route list table 1001
        default via 10.0.0.253 dev eth1
        # ip route list table 1002
        default via 10.0.0.253 dev eth2
        ```

7.  Configure policy routing.
    1.  Run the following command .

        ```
        # ip -4 rule add from 10.0.0.20 lookup 1001
        # ip -4 rule add from 10.0.0.21 lookup 1002
        ```

    2.  Run `ip rule list` to view routing rules.

        ```
        # ip rule list
        0: from all lookup local
        32764: from 10.0.0.21 lookup 1002
        32765: from 10.0.0.20 lookup 1001
        32766: from all lookup main
        32767: from all lookup default
        ```


At this point, you have completed the configuration of the elastic network card.

