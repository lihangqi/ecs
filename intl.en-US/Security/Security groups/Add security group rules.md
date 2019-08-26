# Add security group rules {#concept_sm5_2wz_xdb .concept}

You can use security group rules to control the access to public or internal networks of the ECS instances in a security group.

## Background {#section_bjx_gby_zfb .section}

Security groups control access to or from public or internal networks. For security purposes, most security groups use deny policies for inbound traffic. If you use the default security group, or you select a Web Server Linux template or a Web Server Windows template when creating a security group, security group rules are automatically added to some communication ports. For more information, see [Security group overview](reseller.en-US/Security/Security groups/Security group overview.md#). This topic applies to the following scenarios:

-   When your application needs to communicate with the network outside the security group, but the request stays in the wait state, you need to add security group rules first.
-   When you discover malicious attacks from some request sources during the application operation, add deny security group rules to implement isolation.

## Notes {#section_ab5_j2c_kgb .section}

-   Security group rules depend on NIC types.
    -   Security group rules for classic networks distinguish between internal and public NICs.
    -   Security group rules for VPC networks do not distinguish between internal and public NICs.

        Public network access to and from VPC-type ECS instances is mapped and forwarded by internal NICs. You cannot see public NICs in ECS instances, and can add only internal security group rules. However, security group rules apply to both the internal and public network.

-   Before you add any rules to a security group, all outbound traffic is allowed and all inbound traffic is denied.
-   The total number of inbound and outbound rules for each security group cannot exceed 100.
-   You cannot configure the Priority parameter, set Authorization Type to Security Group, or set Action to Forbid for advanced security group rules. For more information, see [Advanced security group overview](reseller.en-US/Security/Security groups/Advanced security group overview.md#).

## Prerequisites {#section_fxy_lwz_xdb .section}

-   You have created a security group. For more information, see [Create a security group](reseller.en-US/Security/Security groups/Create a security group.md#).
-   You know which internal or public network requests need to be allowed or denied for your instance. For more information about security group rule configuration cases, see [Security group scenarios](../reseller.en-US/Security/Security groups/Scenarios.md#).

## Procedure {#section_trd_pwz_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Locate the security group to which you want to add authorization rules. Click **Add Rules** in the **Actions** column.
5.  On the Security Group Rules page, select one of the following methods to add rules:
    -   1. **Quick Rule Creation**. It can be used when ICMP and GRE are not required and you can select multiple ports. On the **Quick Rule Creation** page, the following application ports are provided: SSH 22, Telnet 23, HTTP 80, HTTPS 443, MS SQL 1433, Oracle 1521, MySQL 3306, RDP 3389, PostgreSQL 5432, and Redis 6379. You can select one or more ports, or customize TCP or UDP ports.

        For more information about the parameters such as **NIC**, **Rule Direction**, and **Port Range** on the **Quick Rule Creation** page, see **Add Security Group Rule**.

    -   2. **Add Security Group Rule**. It can be used when multiple communication protocols such as ICMP and GRE are required.
        1.  Click **Add Security Group Rule**.
        2.  Select **NIC** \(only for security group rules of the classic network\).
            -   **Internal Network**: You do not want your ECS instance to access the public network, or public network access is not required.
            -   **Internet**: Your ECS instance needs to access the public network, or provide applications to the public network.
        3.  Select **Rule Direction**.
            -   **Outbound**: Your ECS instances access other ECS instances in the internal network or resources in the public network.
            -   **Inbound**: Other ECS instances in the internal network or resources in the public network access your ECS instances.
        4.  Select **Action**.
            -   **Allow**: allows access requests on the port.
            -   **Forbid**: Data packets are discarded and no messages are returned. If two security groups have the same rules but different authorization policies, **Forbid** policies are used while **Allow** policies are ignored.
        5.  Select **Protocol Type** and **Port Range**.

            The port range is based on the protocol type. The following table describes the relationship between **Protocol Type** and **Port Range**. For more information about common ports, see [Typical applications of commonly used ports](reseller.en-US/Security/Security groups/Typical applications of commonly used ports.md#).

            |Protocol type|Port range|Scenario|
            |:------------|:---------|:-------|
            |All|-1/-1 is displayed, indicating all ports. You cannot set a port range for this protocol type.|It is used in all trusted scenarios.|
            |All ICMP \(IPv4\)|-1/-1 is displayed, indicating all ports. You cannot set a port range for this protocol type.|It is used when you run the `ping` command to check network connection status between instances.|
            |All GRE|-1/-1 is displayed, indicating all ports. You cannot set a port range for this protocol type.|It is used for VPN.|
            |Customized TCP|Customize a port range. Valid values: 1 to 65535. You must use the <start port\>/<end port\> format. For example, 80/80 indicates port 80, and 1/22 indicates port 1 to port 22.

 |It can be used to allow or deny one or several successive ports.|
            |Customized UDP|
            |SSH|22/22|It is used to connect to a Linux instance remotely. After connecting to the ECS instance, you can modify the port number. For more information, see [Modify the default remote access port](../reseller.en-US/Best Practices/Security/Modify the default remote access port.md#).|
            |Telnet|23/23|It is used to connect to an instance remotely.|
            |HTTP|80/80|It is used when an instance serves as a website or Web application server.|
            |HTTPS|443/443|It is used when an instance serves as a website or Web application server that supports the HTTPS protocol.|
            |MS SQL|1433/1433|It is used when an instance serves as an MS SQL server.|
            |Oracle|1521/1521|It is used when an instance serves as an Oracle SQL server.|
            |MySQL|3306/3306|It is used when an instance serves as a MySQL server.|
            |RDP|3389/3389|It is used to connect to a Windows instance remotely. After connecting to the ECS instance, you can modify the port number. For more information, see [Modify the default remote access port](../reseller.en-US/Best Practices/Security/Modify the default remote access port.md#).|
            |PostgreSQL|5432/5432|It is used when an instance serves as a PostgreSQL server.|
            |Redis|6379/6379|It is used when an instance serves as a Redis server.|

            **Note:** The default STMP port for outbound Internet traffic is port 25, which is disabled by default. It cannot be enabled by security group rules. If you need to use STMP port 25, take proper measures to avoid security risks and then [apply for enabling STMP port 25](https://partners-intl.aliyun.com/help/doc-detail/56130.htm).

        6.  Select **Authorization Type** and **Authorization Objects**.

            The authorized IP address is based on the authorization type.

            |Authorization type|Authorization object|
            |:-----------------|:-------------------|
            |IPv4 CIDR block|             -   Enter an IP address or CIDR block, in the format of 12.1.1.1 or 13.1.1.1/25.
             -   You can enter up to 10 authorization objects at a time. Separate multiple objects with commas \(`,`\).
             -   Specifying 0.0.0.0/0 will allow or deny all IP addresses, based on the authorization policy. Use caution when specifying 0.0.0.0/0.
 |
            |Security group|This authorization type is only valid for the internal network. Authorize the instances in a security group for your account or another account to access the instances in this security group. **CIDR Block** must be selected for public network access.             -   Authorize Current Account: Select another security group ID for your account. For a security group of the VPC type, the destination must be a security group in the same VPC.
            -   Authorize Other Accounts: Enter a security group ID and another account ID. Choose **Account Management** \> **Security Settings** to view your account ID.
 **Note:** For advanced security group rules, you cannot set Authorization Type to Security Group.

 |

            **Note:** When you add an inbound internal network rule for a security group of the classic network type, set Authorization Type to **Security Group** to improve security. If **CIDR Block** is selected, only one entry can be authorized. The entry must be in the a.b.c.d/32 format. Only IPv4 is supported and the subnet mask must be /32.

        7.  Specify a value for **Priority**. Valid values: 1 to 100.

            **Note:** The smaller the number, the higher the priority. You can set priority values only for basic security groups, but not for advanced security groups. For more information, see [Security group overview](reseller.en-US/Security/Security groups/Security group overview.md#section_mgh_wv1_wgb).

        8.  Click **OK**.

## Results {#section_voz_mhy_q88 .section}

Click the refresh icon to confirm that the security group rule is added. Changes to security group rules are automatically applied to ECS instances in the security group. We recommend that you immediately test whether the changes take effect.

## Related APIs {#section_vrl_q2c_3gb .section}

-   Call [AuthorizeSecurityGroup](../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#) to add an inbound security group rule.
-   Call [AuthorizeSecurityGroupEgress](../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md#) to add an outbound security group rule.

## Next operations {#section_pql_d11_ydb .section}

An ECS instance must belong to one or more security groups. You can [add an instance to one or more security groups](reseller.en-US/Security/Security groups/Add an ECS instances to a security group.md#) based on your business needs.

