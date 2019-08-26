# Assign multiple secondary private IP addresses {#concept_ff2_hbk_ggb .concept}

You can assign one or more secondary private IP addresses to an Elastic Network Interface \(ENI\).

## Scenarios {#section_chq_2rk_ggb .section}

-   High instance usage

    If your server hosts multiple applications, you can assign multiple secondary private IP addresses to an ENI to extend the utilization of your instance. Each application is then represented by a separate service IP address.

-   Failover transfer

    If your instance fails, you can quickly transfer traffic to the IP address of other standby instances.


## Limits {#section_mwz_glk_ggb .section}

-   You can only attach an ENI to a VPC ECS instance in the same VPC.
-   A single VPC security group can contain a maximum of 2,000 private IP addresses \(shared by the primary and secondary ENIs\).
-   You can assign a maximum of 20 private IP addresses to an ENI.
    -   When an ENI is in `Available` state, you can assign a maximum of 10 private IP addresses to the ENI.
    -   When an ENI is in `InUse` state, the number of private IP addresses that you can assign to the ENI depends on the instance type. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md#).

## Prerequisites {#section_mk2_n4k_ggb .section}

-   Your instance type can be assigned with multiple secondary private IP addresses. For more information, see [DescribeInstanceTypes](../../../../../reseller.en-US/API Reference/Instances/DescribeInstanceTypes.md#).
-   The ENI must be in `Available` or `InUse` state.
-   When you assign secondary private IP addresses to the primary ENI, the instances attached to the primary ENI must be in `Running` or `Stopped` state.

## Assign multiple secondary private network IP addresses to a Windows instance {#section_y4b_krk_ggb .section}

1.  Open Network and Sharing Center .
2.  Click**Change Adapter Settings**.
3.  Double-click the current network connection name, and then click**Properties**.
4.  Double-click **Internet Protocol Version 4 \(TCP/IPv4\)**.
5.  Select **Use the Following IP Address**, and then click**Advanced**.
6.  Click**Add**, and then enter the assigned IP address and subnet mask. You can add multiple IP addresses.
7.  Click **OK**.

## Assign multiple secondary private IP addresses to a Linux instance {#section_b2x_hlb_3gb .section}

1.  Use the [AssignPrivateIpAddresses](../../../../../reseller.en-US/API Reference/Elastic network interfaces/AssignPrivateIpAddresses.md#) API to assign multiple secondary private IP addresses.
2.  Use the [DescribeNetworkInterfaces](../../../../../reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md#) API to query the assigned secondary private IP addresses.
3.  [Connect to an instance by using the Management Terminal](reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to an instance by using the Management Terminal.md#).
4.  Configure the assigned IP addresses.

    |Release|Applicable version|Procedure|
    |:------|:-----------------|:--------|
    |RHEL series|     -   CentOS 6/7
    -   Red Hat 6/7
    -   Aliyun Linux 17
 |     1.  If the ENI is eth0, run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:0` command to open the network configuration file and add the following configuration items:

        ```
DEVICE=eth0:0
TYPE=Ethernet
BOOTPROTO=static
ONBOOT=yes
IPADDR=<IPv4 address 1>
NETMASK=<IPv4 mask>
GATEWAY=<IPv4 gateway>
        ```

If multiple IP addresses are assigned, run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:1` command to open the network configuration file and add the following configuration items:

        ```
DEVICE=eth0:1
TYPE=Ethernet
BOOTPROTO=static
ONBOOT=yes
IPADDR=<IPv4 address 2>
NETMASK=<IPv4 mask>
GATEWAY=<IPv4 gateway>
        ```

    2.  Run the `service network restart` or `systemctl restart network` command to restart the service.
 |
    |Debian series|     -   Ubuntu 14/16
    -   Debian/8/9
 |     1.  If the ENI is eth0, run the `vi /etc/network/interfaces` command to open the network configuration file and add the following configuration items:

        ```
auto eth0:0
iface eth0:0 inet static
address <IPv4 address 1>
netmask <IPv4 mask>
gateway <IPv6 gateway>

auto eth0:1
iface eth0:1 inet static
address  <IPv4 address 2>
netmask <IPv4 mask>
gateway <IPv4 gateway>
        ```

    2.  Run the `service networking restart` or `systemctl restart networking` command to restart the service.
 |
    |SLES series|     -   SUSE 11/12
    -   OpenSUSE 42
 |     1.  If the ENI is eth0, run the `vi /etc/sysconfig/network/ifcfg-eth0` command to open the network configuration file and add the following configuration items:

        ```
IPADDR_0=<IPv4 address 1>
NETMASK_0=<subnet prefix length>
LABEL_0='0'

IPADDR_1=<IPv4 address 2>
NETMASK_1=<subnet prefix length>
LABEL_1='1'
        ```

    2.  Run the `service network restart` or `systemctl restart network` command to restart the service.
 |


## What to do next {#section_aqz_tlm_ggb .section}

When your ENI does not require multiple secondary private IP addresses, you can[Revoke multiple secondary private IP addresses](reseller.en-US/Network/Elastic Network Interfaces/Revoke multiple secondary private IP addresses.md#).

