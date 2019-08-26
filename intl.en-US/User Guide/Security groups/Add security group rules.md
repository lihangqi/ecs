# Add security group rules {#concept_sm5_2wz_xdb .concept}

You can add security group rules to enable or disable access to and from the Internet or intranet for ECS instances in the security group.

-   VPC: You only need to set inbound and outbound rules, and you do not need to create different rules for the Internet and intranet. The Internet access for VPC instance is realized through private NIC mapping. Therefore, you cannot see the Internet NIC inside the instance, and you can only set intranet rules in the security group. The rules apply to Internet and intranet access at the same time.
-   Classic network: You must set outbound and inbound rules for the Internet and intranet respectively.

For a new security group without any rules, outbound traffic is allowed and inbound traffic is refused by default, over either the Internet or intranet. Therefore, we recommend that you only need rules to refuse outbound traffic or allow inbound traffic.

Changes to the security group rules automatically apply to ECS instances in the security group.

## Prerequisites {#section_fxy_lwz_xdb .section}

You have created a security group. For more information, see [create a security group](reseller.en-US/User Guide/Security groups/Create a security group.md#).

You know which Internet or intranet requests need to be allowed or refused for your instance.

## Procedure {#section_trd_pwz_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Networks and Security** \> **Security Groups**.
3.  Select the target region.
4.  Find the security group to add authorization rules and then, in the **Actions** column, click **Add Rules**.
5.  On the Security Group Rules page, click **Add Security Group Rule**.

    **Note:** If you do not need to enable or disable all ports for all protocols, ICMP, or GRE, you can select **Quick Rule Creation**.

    |Protocol|SSH|telnet|HTTP|HTTPS|MS SQL|
    |Port|22|2, 3|80.|443|1433|
    |Protocol|Oracle|MySQL|RDP|PostgreSQL|Redis|
    |Port|1521|3306|3389|5432|6379|

    **Note:** See step 6 for descriptions on each parameter configuration.

6.  In the dialog box, set the following parameters:
    -   **NIC**:
        -   For a VPC-Cconnected security group, you do not need to select the NIC.

            **Note:** 

            -   If your instances can access the Internet, the rules work for both the Internet and intranet.
            -   If your instances cannot access the Internet, the rules work for intranet only.
        -   For a Classic network-connected security group, you must select **Internet** or **Intranet**.
    -   **Rule Direction**:
        -   **Outbound**: ECS instances access other ECS instances over intranet networks, or through Internet resources.
        -   **Inbound**: Other ECS instances in the intranet and Internet resources access the ECS instance.
    -   **Action**: Select **Allow** or **Forbid**.

        **Note:** **Forbid** policies discard the data packet without returning a response. If two security group rules overlap except the authorization policy, the **Forbid** rule takes priority over the **Allow** rule.

    -   **Protocol Type** and **Port Range**: The port range setting is affected by the selected protocol type. The following table shows the relationship between protocol types and port ranges.

        |Protocol Type|Port Range|Scenarios|
        |All|Shown as -1/-1, indicating all ports. You cannot modify it.|Used in scenarios where both applications are fully and mutually trusted.|
        |All ICMP|Shown as -1/-1, indicating no port restriction. You cannot modify it.|Used to detect the instance network connection status by using `ping`.|
        |All GRE|Shown as -1/-1, indicating no port restriction. You cannot modify it.|Used for VPN service.|
        |Custom TCP|For custom port ranges, the valid port value is 1−65535, and the valid port range format is Start Port/End Port. A valid port range format must be used for one port. For example, use 80/80 to indicate port 80.|It can be used to allow or forbid one or several successive ports.|
        |Custom UDP|
        |SSH|Shown as 22/22.After connecting to the ECS instance, you can modify the port number. For more information, see [default remote access port modifications](https://partners-intl.aliyun.com/help/doc-detail/51644.htm).

|Used for SSH to connect to a Linux instance remotely.|
        |TELNET|Shown as 23/23.|Used to remotely log on to instances by using Telnet.|
        |HTTP|Shown as 80/80.|The instance is used as a server for a website or a web application.|
        |HTTPS|Shown as 443/443.|The instance is used as a server for a website or a web application that supports HTTPS.|
        |MS SQL|Shown as 1433/1433.|The instance is used as an MS SQL server.|
        |Oracle|Shown as 1521/1521.|The instance is used as an Oracle SQL server.|
        |MySQL|Shown as 3306/3306.|The instance is used as a MySQL server.|
        |RDP|Shown as 3389/3389.After connecting to the ECS instance, you can modify the port number. For more information, see [default remote access port modifications](https://partners-intl.aliyun.com/help/doc-detail/51644.htm).

|Used to remotely connect to Windows instances.|
        |PostgreSQL|Shown as 5432/5432.|The instance is used as a PostgreSQL server.|
        |Redis|Shown as 6379/6379.|The instance is used as a Redis server.|

        **Note:** Port 25 is restricted by default and cannot be opened through security group rules. However, you can submit a ticket to [apply to open TCP port 25](https://partners-intl.aliyun.com/help/doc-detail/56130.htm). For more common port information, see [introduction to common ECS instance ports](reseller.en-US/User Guide/Security groups/Introduction to common ECS instance ports.md#).

    -   **Authorization Type** and **Authorization Object**: The authorization object affects the setting of authorization type. The following table shows the relationship between them.

        |Authorization Type|Authorization Object|
        |Address field access|Use the IP or CIDR block format such as 10.0.0.0 or 192.168.0.0/24. Only IPv4 addresses are supported. 0.0.0.0/0 indicates all IP addresses.|
        |Security group access|Only for intranet access. Authorize the instances in a security group under your account or another account to access the instances in this security group.        -   Authorize this account: Select a security group under your account. Both security groups must be in the same VPC.
        -   Authorize another account: Enter the target security group ID and the account ID. On the **Account Management** \> **Security Settings**, you can obtain the account ID.
For VPC-Connected network instances, security group access works for private IP addresses only. If you want to authorize Internet IP address access, use address field access.|

        **Note:** To guarantee the security of your instance, when you are configuring an intranet inbound rule for a classic network-connected security group, **Security Group Access** is the top priority for **Authorization Type**. If  you select **Address Field Access**, and you want to type an IP address in the CIDR format, type an IP address in the format of a.b.c.d/32. Only 32 is the valid CIDR prefix.

    -   **Priority**: The value range is 1-100. The smaller the value, the higher the priority. For more information, see [ECS security group rule priority explanation](reseller.en-US/User Guide/Security groups/Add security group rules.md#priority).

         

7.  Click **OK**.

Security group rules generally take effect immediately.

## Verify security group rules {#section_r1s_jzz_xdb .section}

If you have installed a web service on the instance and added a security group rule in a security group, you can allow all IP addresses to have inbound access to TCP port 80 of the instance. Follow these steps according to your instance OS to verify the security group rule.

**Linux instances:**

For a Linux instance in the security group, follow these steps to verify the security group rule:

1.  [Connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the following command to check whether TCP 80 is being listened.

    ```
    netstat -an | grep 80
    ```

    If the following result returns, web service for TCP port 80 is enabled.

    ```
    tcp        0      0 0.0.0.0:80                  0.0.0.0:*                   LISTEN
    ```

3.  Enter `http://public IP address of the instance` into your browser. If access is successful, the rules have been activated.

**Windows instances:**

For a Windows instance in the security group, follow these steps to verify the security group rule:

1.  [Connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  Run the **CMD**, and run the following command to check whether TCP port 80 is being listened.

    ```
    netstat -aon | findstr :80
    ```

    If the following result returns, web service for TCP port 80 is enabled.

    ```
    TCP 0.5.0.0: 80 0.5.0.0: 0 listening 1172
    ```

3.  Enter `http: // instance public IP address` into your browser. If access is successful, the rules have been activated.

## ECS security group rule priority explanation {#priority .section}

The **Priority** value of a security group rule ranges from 1 to 100. A smaller number indicates a higher priority.

ECS instances can belong to different security groups. As a result, instances may have multiple security group rules that have the same protocol types, port ranges, authorization types, and authorization objects. The rule that takes effect depends on the setting of **Priority** and **Authorization Policy**:

-   If the rules have the same **Priority**, the **Forbid** rule takes effect, and the **Allow** rule does not.
-   If the rules have different **Priority**, the rule with higher priority takes effect first, regardless the setting of **Authorization Policy** .

## Related topics {#section_pql_d11_ydb .section}

-   [Security group FAQ](https://partners-intl.aliyun.com/help/faq-detail/40570.htm)
-   [Security group](../../../../reseller.en-US/Product Introduction/Network and security/Security group.md#)
-   [Default security group rules](reseller.en-US/User Guide/Security groups/Default security group rules.md#)
-   [Implication and matching sequence of the ECS security group rule priority](https://partners-intl.aliyun.com/help/faq-detail/40642.htm)

