# FAQ {#concept_40637_zh .concept}

-   [什么是 BGP 机房？](#)
-   [什么是广域网和局域网？](#)
-   [什么是 ECS 实例的入网带宽和出网带宽？](#)
-   [如何表示子网掩码？](#)
-   [如何划分子网？](#)
-   [如何查询 ECS 实例的 IP 地址？](#)
-   [如何查询 IP 地址的详细信息？](#)
-   [如何禁用 ECS 实例的网卡？](#)
-   [如何查看云服务器 ECS 公网流量统计信息？](#)
-   [为什么不能访问 ECS 服务器上的网站？](#)
-   [为什么云监控显示的 ECS 带宽和 ECS 控制台显示带宽不一致？](#)
-   [云盾是否有屏蔽 IP 的功能？](#)
-   [云服务器 ECS 出现了异地登录怎么办？](#)
-   [ECS 实例为已停止状态，为什么按量付费带宽仍产生出网流量？](#)

## Why should I implement BGP in my on-premises data center? {#section_hmd_spf_qgb .section}

The Border Gateway Protocol \(BGP\) is used to interconnect Autonomous Systems \(ASs\) on the Internet, control routing information propagation, and select the best route.

Mainland China-based carriers such as China Netcom, China Telecom, China Tietong, and other large private data center operators, have AS numbers. Most network operators in Mainland China interconnect with each other by using BGP and AS numbers.

To interconnect these multiple lines, data centers must apply for a CIDR block and AS numbers from China Internet Network Information Center \(CNNIC\) or Asia Pacific Network Information Centre \(APNIC\), and then broadcast the CIDR block to the network of other operators by using BGP. With BGP-based interconnection, all backbone routing devices of these operators can determine the best route to the CIDR block of their respective data centers to ensure that their end users can access networks quickly.

## What are WAN and LAN? {#section_o52_nlg_4gb .section}

**WAN**: A Wide Area Network \(WAN\), also known as public network, is a remote network that connects computers in Local Area Networks \(LANs\) and Metropolitan Area Networks \(MANs\) across multiple regions, cities, countries, or continents to provide long-distance communication. However, a WAN is different from the Internet.

**LAN**: A Local Area Network \(LAN\), also known as an intranet, is a computer group that consists of multiple interconnected computers in an area. A LAN supports file management, application sharing, printer sharing, task scheduling, and email and fax services. A LAN is a closed network that can consist of a small network \(such as two computers in an office\), up to thousands of computers in a company.

## What are the inbound bandwidth and outbound bandwidth of an ECS instance? {#section_pv3_qbl_qgb .section}

The following table describes the inbound bandwidth and the outbound bandwidth of an ECS instance.

|Bandwidth type|Description|
|:-------------|:----------|
|Inbound bandwidth|The bandwidth used for traffic to go to ECS. For example: -   ECS downloads external network resources.
-   An FTP client uploads resources to ECS.

 |
|Outbound bandwidth|The bandwidth used for traffic to go out of ECS. For example: -   ECS provides external access.
-   An FTP client downloads resources from ECS.

 |

## How is a subnet mask expressed? {#section_lgk_wqf_qgb .section}

A subnet mask is expressed in the following two formats:

-   Dotted decimal notation, for example:

    Default subnet mask of class-A networks: 255.0.0.0

-   An IP address plus a forward slash \(/\) and a number \(from 1 to 32, which indicates the length of the network identifier in the subnet mask\), for example:

    192.168.0.3/24


## How can I divide subnets? {#section_prv_5sf_qgb .section}

For information about how to divide subnets, see [Plan and design VPC](https://help.aliyun.com/document_detail/54095.html).

## How can I query the IP address of an ECS instance? {#section_vpl_qbg_qgb .section}

-   For a Linux instance

    Run the `ifconfig` command to view the ENI information, including the IP address, subnet mask, gateway, DNS, and MAC address.

-   For a Windows instance

    Run the `ipconfig /all` command to view the ENI information, including the IP address, subnet mask, gateway, DNS, and MAC address.


## How can I query IP address details? {#section_gzn_x1g_qgb .section}

You can log on to the [Taobao IP address library](http://ip.taobao.com/ipSearch.html) to query detailed information of an IP address, such as region/country, province, city, county, and operator.

## How can I disable the ENI of an ECS instance? {#section_bxf_ywf_qgb .section}

-   For a Linux instance
    1.  Run the `ifconfig` command to view the ENI name of the ECS instance.
    2.  Run the `ifdown` command to disable the ENI. For example, if the ENI name is `eth1`, run the `ifdown eth1` command.
-   For a Windows instance
    1.  Run the `ipconfig` command to view the ENI information.
    2.  Choose **Control Panel** \> **Network and Internet** \> **Network and Sharing Center** \> **Change adapter settings** and then disable the ENI.

## How can I view public network traffic statistics of ECS? {#section_skr_3kg_qgb .section}

To view the public network traffic statistics of ECS, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.aliyun.com/login-required#/ecs).
2.  In the upper right corner of the page, choose **Billing Management** \> **Billing Management**
3.  In the left-side navigation pane, click **Usage Records**.
4.  Select **Elastic Compute Service \(ECS\) - Pay-As-You-Go** from the **Product Name** drop-down list.
5.  Select a **Use Period** and a **Unit**.
6.  Enter the verification code, and then click **Export CSV**.
7.  Open the exported CSV file to view the public network traffic statistics of ECS.

## Why am I unable to access a website that is hosted on an ECS instance? {#section_cwr_y3g_4gb .section}

If this issue occurs, it is likely because Aegis has determined that the address of the website poses a threat and has blocked the website. To resolve this issue, add the affected website address to the Aegis whitelist. For more information, see [Avoid Anti-DDoS Basic false positives by using a whitelist](../../../../reseller.en-US/Anti-DDoS Basic Service/User Guide/Avoid Anti-DDoS Basic false positives by using a whitelist.md#).

## Why is the ECS bandwidth displayed on CloudMonitor different from that displayed in the ECS console? {#section_cvc_bjl_qgb .section}

ECS acts as the backend server of SLB instances and uses the 7-layer HTTP forwarding model. As a result of this forwarding model, SLB forwards requests from the client to ECS, which then responds to the client by using the external bandwidth. This external bandwidth is not displayed in the ECS console. Instead, it is counted as part of outbound traffic generated by SLB.

## What should I do if I detect a suspicious remote logon attempt to my ECS instance? {#section_nda_9m3_7o0 .section}

If you detect a suspicious remote logon attempt to your ECS instance, follows these steps:

1.  Check the logon time to see whether you or other administrators logged on to ECS.
2.  If the logon is suspicious, perform the following operations:
    1.  Reset the instance logon password immediately. For more information, see [Reset an instance logon password](../../../../reseller.en-US/Instances/Manage instances/Reset an instance logon password.md#).
    2.  Check whether a virus has infected your ECS instance. .
    3.  Configure the security group to [只允许特定的IP登录](../../../../reseller.en-US/Security/Security groups/Scenarios.md#specifyIpAccess).

## Why does a Pay-As-You-Go bandwidth package still generate outbound traffic and incur fees after my ECS instance is stopped? {#section_im4_sdl_qgb .section}

This is because CC security protection is enabled for your ECS instance. As a result, the security mechanism automatically sends attack probe packets and generates outbound traffic. To resolve this issue, disable CC security protection.

## Can I change a public IP \(IPv4\) address six hours after I created an instance? {#section_7z6_4zn_vop .section}

## Why am I unable to see the **Change Public IP** option in the ECS console? {#section_kdx_8zp_tyw .section}

## Can I change a private IP address? {#section_knr_78u_9te .section}

## How can I obtain a public IP address if I did not assign a public IP \(IPv4\) address during instance creation? {#section_ni4_qgx_0tb .section}

