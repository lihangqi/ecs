# Assign a secondary private IP address {#concept_ff2_hbk_ggb .concept}

This topic describes how to assign secondary private IP addresses to an Elastic Network Interface \(ENI\).

## Scenarios {#section_chq_2rk_ggb .section}

-   Optimize application usage

    If your ECS instance hosts multiple applications, you can assign multiple secondary private IP addresses to the corresponding ENI. In this way, each application uses a separate IP address for services, which optimizes the usage of the ECS instance.

-   Avoid service disruptions

    You can attach the ENI of an active ECS instance to another instance to direct traffic to the standby instance if the active instance fails, enabling service continuity.


## Limits {#section_mwz_glk_ggb .section}

-   You can only attach an ENI to an ECS instance in a VPC. The ENI and the instance must be in the same VPC, VSwitch, and zone.
-   Each VPC security group can contain a maximum of 2,000 private IP addresses, and the quota is shared among all corresponding primary and secondary ENIs.
-   You can assign a maximum of 20 private IP addresses to an ENI.
    -   If the target ENI is in the `Available` state, you can assign a maximum of 10 private IP addresses to the ENI.
    -   If the target ENI is in the `InUse` state, the number of private IP addresses that you can assign to the ENI depends on the instance type. For more information, see [Instance type families](../reseller.en-US/Instances/Instance type families.md#).
-   Your instance type must be able to support being assigned multiple secondary private IP addresses. For more information, see [Instance type families](../reseller.en-US/Instances/Instance type families.md#) or call the [DescribeInstanceTypes](../reseller.en-US/API Reference/Instances/DescribeInstanceTypes.md#) API action.
-   If you assign multiple secondary private IP addresses to a primary ENI, the instance to which the primary ENI is attached must be in the `Running` or `Stopped` state.

## Assign a secondary private IP address to an ENI {#section_zz0_16c_2q3 .section}

1.  On the Network Interfaces page, locate the target ENI, and then click **Manage Secondary Private IP Address** in the **Actions** column.
2.  In the displayed dialog box, click **Assign New IP** once or multiple times if additional IP addresses are needed.

    You can also enter one or more secondary private IP addresses that are within the **IPv4 Private CIDR**. If you do not enter any secondary private IP address, the system randomly assigns IP addresses that are within the **IPv4 Private CIDR**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83258/156472631947047_en-US.png)

3.  Click **Modify**.
4.  Optional. If you use automatic assignment of a secondary private IP address, click **Manage Secondary Private IP Address** in the **Actions** column to view the assigned secondary private IP address, and then configure this IP address for an ECS instance.
5.  Optional. If the target ENI is not attached, attach it to an ECS instance. For more information, see [Attach an ENI](reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#).

Related API: [AssignPrivateIpAddresses](../reseller.en-US/API Reference/Elastic network interfaces/AssignPrivateIpAddresses.md#)

## Assign a secondary private IP address to a Windows instance {#section_y4b_krk_ggb .section}

1.  Connect to the target instance. For more information, see [Overview](../reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Open the Network and Sharing Center.
3.  Click **Change adapter settings**.
4.  Double-click the current network connection name, and then click **Properties**.
5.  Double-click **Internet Protocol Version 4 \(TCP/IPv4\)**.
6.  Select **Use the following IP address**, and then click **Advanced**.
7.  Click **Add**, and then enter the assigned **IP Address** and set the **Subnet Mask**.

    You can add multiple IP addresses to the same adapter.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83258/156472631947049_en-US.png)

8.  Click **OK**.

## Assign a secondary private IP address to a Linux instance {#section_b2x_hlb_3gb .section}

1.  Connect to the target instance. For more information, see [Overview](../reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Follow the instructions in the method that corresponds to the OS of your instance to assign a secondary private IP address.

    In the following example, a primary ENI named eth0 are used. If you use a secondary ENI, you must modify the ENI identifier as needed.

    -   RHEL series: CentOS 6/7, Red Hat 6/7, and Aliyun Linux 17
        1.  Run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:0` command to open the network configuration file and add the following configuration items:

            ``` {#codeblock_rn2_hix_2fq}
            DEVICE=eth0:0
            TYPE=Ethernet
            BOOTPROTO=static
            ONBOOT=yes
            IPADDR=<IPv4 address 1>
            NETMASK=<IPv4 mask>
            GATEWAY=<IPv4 gateway>
            ```

            If you assign multiple IP addresses, run the `vi /etc/sysconfig/network-scripts/ifcfg-eth0:1` command to open the network configuration file and add the following configuration items:

            ``` {#codeblock_8vy_zac_xvr}
            DEVICE=eth0:1
            TYPE=Ethernet
            BOOTPROTO=static
            ONBOOT=yes
            IPADDR=<IPv4 address 2>
            NETMASK=<IPv4 mask>
            GATEWAY=<IPv4 gateway>
            ```

        2.  Run the `service network restart` or `systemctl restart network` command to restart the network service.
    -   Debian series: Ubuntu 14/16 and Debian/8/9
        1.  Run the `vi /etc/network/interfaces` command to open the network configuration file and add the following configuration items:

            ``` {#codeblock_9ok_cfn_9ev}
            auto eth0:0
            iface eth0:0 inet static
            address <IPv4 address 1>
            netmask <IPv4 mask>
            gateway <IPv4 gateway>
            
            auto eth0:1
            iface eth0:1 inet static
            address  <IPv4 address 2>
            netmask <IPv4 mask>
            gateway <IPv4 gateway>
            ```

        2.  Run the `service networking restart` or `systemctl restart networking` command to restart the network service.
    -   SLES series: SUSE 11/12 and OpenSUSE 42
        1.  Run the `vi /etc/sysconfig/network/ifcfg-eth0` command to open the network configuration file and add the following configuration items:

            ``` {#codeblock_6h3_4j1_b81}
            IPADDR_0=<IPv4 address 1>
            NETMASK_0=<subnet prefix length>
            LABEL_0='0'
            
            IPADDR_1=<IPv4 address 2>
            NETMASK_1=<subnet prefix length>
            LABEL_1='1'
            ```

        2.  Run the `service network restart` or `systemctl restart network` command to restart the network service.

## What to do next {#section_aqz_tlm_ggb .section}

If you no longer require the current number of secondary private IP addresses, you can revoke one or more of them from the target ENI. For more information, see [Revoke a secondary private IP address](reseller.en-US/Network/Elastic Network Interfaces/Revoke a secondary private IP address.md#).

