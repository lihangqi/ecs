# Default security group rules {#concept_f4j_vtz_xdb .concept}

This article introduces the default rules in the security groups created manually or by the system.

**Note:** 

Security groups have status. If an outbound packet is allowed, inbound packets corresponding to this connection are also allowed. For more information about security groups, see [security groups](../../../../reseller.en-US/Product Introduction/Network and security/Security group.md#).

## Security groups created by the system {#section_nwl_d5z_xdb .section}

When you create an ECS instance in a region where you have not created a security group, use the default security group provided by the system.

Such a security group only has the default rules for access over the ICMP protocol, TCP Port 22 \(for SSH\), TCP Port 3389 \(for RDP\), TCP Port 80 \(for HTTP\), and TCP Port 443 \(for HTTPS\). The default rules vary with the network type of the security group.

-   VPC: The rules apply to both Internet and intranet access. The Internet access of the VPC type instance is realized through the private NIC mapping. So, you cannot see the Internet NIC inside the instance, and you can only set intranet rules in the security group. The security group rules take effect for both intranet and the Internet. The default rules of the default VPC-connected security group are shown in the following table.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Priority|Authorization Type|Authorization Object|
    |N/A|Inbound|Allow|Custom TCP \(SSH\)|22/22|110|Address field access|0.0.0.0/0|
    |Custom TCP \(RDP\)|3389/3389|
    |All ICMP|-1/-1|
    |Custom TCP \(HTTP\), optional|80/80|
    |Custom TCP \(HTTPS\), optional|443|

-   Classic network: The default rules of a classic network-connected security group are shown in the following table.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Priority|Authorization Type|Authorization Object|
    |Internet|Inbound|Allow|Custom TCP \(SSH\)|22/22|110|Address field access|0.0.0.0/0|
    |Custom TCP \(RDP\)|3389/3389|
    |All ICMP|-1/-1|
    |Custom TCP \(HTTP\), optional|80/80|
    |Custom TCP \(HTTPS\), optional|443|

    **Note:** Rules with priority 110 means that they have the lowest priority in the security group. When you manually create a security group, only values from 1 to 100 are valid for priority setting. For more information about the rule priority, see [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#).


To meet your business needs, you can [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#) in the default security group.

## Manually created security group {#section_gbf_x5z_xdb .section}

After [creating a security group](reseller.en-US/User Guide/Security groups/Create a security group.md#), before you add rules, the following default rules apply to the communication of all the instances in the group over the Internet or intranet:

-   Outbound: Allow
-   Inbound: Refuse

If your instance has joined such a security group, you can use the [Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#) only to connect to an instance, rather than using any remote connection methods like [connecting to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#) or [connecting to a Windows instance by using remote connection software](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).

To meet your business needs, you can [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#) in the manually created security groups.

