# Scenarios {#concept_ngr_vht_xdb .concept}

This topic describes several typical scenarios in which VPC security groups and classic network security groups are used.

**Note:** 

-   For information about how to create security groups and add security group rules, see [Create a security group](reseller.en-US/Security/Security groups/Create a security group.md#) and [Add security group rules](reseller.en-US/Security/Security groups/Add security group rules.md#).
-   For information about commonly used ports, see [Typical applications of commonly used ports](../../../../reseller.en-US/Security/Security groups/Typical applications of commonly used ports.md#).

-   [Scenario 1: Establish intranet communication between two instances in the same region and under the same account](#) 

    If you need to copy resources between two ECS instances in the same region and under the same account, you can configure security group settings to establish intranet communication between the two ECS instances.

-   [Scenario 2: Establish intranet communication between two instances in the same region and under different accounts](#) 

    If you need to copy resources between two ECS instances in the same region and different accounts, you can configure security group settings to establish intranet communication between the two ECS instances.

-   [Scenario 3: Allow remote access to your instance from only specified IP addresses](#) 

    You can remotely modify the logon port number and only allow specified IP addresses to log on to your ECS instance.

-   [Scenario 4: Allow your instance to access specified external IP addresses only](#) 

    You can configure security group rules to allow your instance to access specified external IP addresses only.

-   [Scenario 5: Deny your instance to access specified external IP addresses](#) 

    You can configure security group settings to deny your instance to access specified external IP addresses.

-   [Scenario 6: Allow remote access to your instance through the Internet](#) 

    You can remotely connect to your ECS instance through the Internet.

-   [Scenario 7: Allow an ECS instance in a security group under another account in the same intranet to remotely connect to your instance](#) 

    You can remotely connect to your instance by using an ECS instance in a security group under another account in the same intranet.

-   [Scenario 8: Allow access to your instance through HTTP and HTTPS](#) 

    If you host a website on your instance, you can add security group rules to allow your users to access the website through HTTP or HTTPS.


## Scenario 1: Establish intranet communication between two instances in the same region and under the same account {#section_i35_nll_ngb .section}

For two instances in the same region and under the same account:

-   If the two instances are in the same security group, they can communicate with each other. Configuration is not required.
-   If the two instances are in different security groups, they cannot communicate with each other. You can add a rule to the security groups respectively to authorize the instances in the security groups to access each other through the intranet. Security rule settings vary among different network types, as shown in the following table.

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Priority|Authorization type|Authorization object|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-------|:-----------------|:-------------------|
    |VPC|Configuration is not required.|Inbound|Allow|Set the applicable protocol.|Set the port range.|1|Security group access \(authorize this account\).|Select the ID of the security group in which the allowed instance is located.|
    |Classic network|Intranet|


**Note:** 

For ECS instances that belong to a VPC, if they are in the same VPC, you can configure their security group rules to establish intranet communication. If they are in different VPCs \(regardless of whether they belong to the same account or in the same region\), you can use Express Connect to establish VPC communication. For more information, see [Connect two VPCs under different accounts](https://partners-intl.aliyun.com/help/doc-detail/44842.htm).

## Scenario 2: Establish intranet communication between two instances in the same region and under different accounts {#section_sfg_zll_ngb .section}

This scenario applies only to ECS instances in a classic network.

For example, User A owns an ECS instance in a classic network in China \(Hangzhou\), named Instance A \(The intranet IP address is A.A.A.A\), which belongs to a security group named Group A.

User B owns an ECS instance in a classic network in China \(Hangzhou\), named Instance B \(The intranet IP address is B.B.B.B\), which belongs to a security group named Group B.

You must add security group rules in Group A and Group B to authorize intranet communication between Instance A and Instance B.

-   Add a rule to Group A to authorize Instance B to access Instance A. The rule settings are described in the following table.

    |NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Intranet|Inbound|Allow|Select the applicable protocol type.|Set the port range.|Security group access \(authorize other accounts\).|The ID of Group B. Enter the User B's ID specified in **Account ID**.|1|

-   Add a rule to Group B to authorize Instance A to access Instance B. The rule settings are described in the following table.

    |NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Intranet|Inbound|Allow|Select the applicable protocol type.|Set the port range.|Security group access \(authorize other accounts\).|The ID of Group A. Enter the User A's ID specified in **Account ID**.|1|

    **Note:** To guarantee instance security, when you set an intranet inbound rule for the classic network, **Security Group Access** is preferred for the authorization type. If you select **CIDR block Access**, only a single IP address can be authorized, and the authorization object must be in the format of `a.b.c.d/32`. The IP address can be set as needed, but the subnet mask must be /32.


## Scenario 3: Allow remote access to your instance from only specified IP addresses {#specifyIpAccess .section}

If you only want a specified IP address to remotely log on to your instance, add a rule to the security group to which your instance belongs by using the settings described in the following examples.

-   Linux instance

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|SSH \(22\)|22/22|CIDR block access|The IP address that allows remote access \(for example, 1.2.3.4/32 or 10.0.0.0/8\)|1|
    |Classic network|Internet|

-   Windows instance

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|RDP \(3389\)|3389/3389|CIDR block access|The IP address that allows remote access \(for example, 1.2.3.4/32 or 10.0.0.0/8\)|1|
    |Classic network|Internet|


## Scenario 4: Allow your instance to access specified external IP addresses only {#specifyInstanceAccess .section}

If you only want your instance to access only a specified IP address, add a rule to the security group to which your instance belongs by using the settings described in the following examples.

-   To deny your instance to access all Internet IP addresses through any protocol, set a priority lower than the priority of the security group rule that allows access to Internet IP addresses. In this example, set the priority to 2. The security group rule settings are described in the following table.

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Outbound|Deny|All|-1/-1|CIDR block access|0.0.0.0/0|2|
    |Classic network|Internet|

-   To allow your instance to access specified Internet IP addresses, set a priority higher than the priority of the security group rule used to deny access to Internet IP addresses. In this example, set the priority to 1.

    |Network Type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Outbound|Allow|Select the applicable protocol type.|Set the port range.|CIDR block access|The specified Internet IP address that you allow to be accessed by your instance \(for example, 1.2.3.4/32 or 10.0.0.0/8\)|1|
    |Classic network|Internet|


After adding a security group rule, connect to the instance, and then conduct a `ping` or `telnet` test. If the instance can access only the allowed IP address, it means that the security group rule takes effect.

## Scenario 5: Deny your instance to access specified external IP addresses {#section_qtl_vhz_ngb .section}

If you do not want your instance to access a specified external IP address, add a rule to the security group to which your instance belongs by using the settings described in the following tables.

|Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
|:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
|VPC|Configuration is not required.|Outbound|Deny|All|-1/-1|CIDR block access|The specified Internet IP address that you deny to be accessed by your instance \(for example, 1.2.3.4/32 or 10.0.0.0/8\)|1|
|Classic network|Internet|

## Scenario 6: Allow remote access to your instance through the Internet {#allowRemoteAccess .section}

To allow remote access to your instance through the Internet, add the security group rule described in the following table.

|Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
|:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
|VPC|Configuration is not required.|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|CIDR block access|If you allow all Internet IP addresses to connect to your instance, enter 0.0.0.0/0. If you only allow specified IP addresses to remotely connect to your instance, see [Scenario 3: Allow remote access to your instance from specified IP addresses only](#).|1|
|Linux: SSH \(22\)|22/22|
|Custom TCP|Custom \(for example, 8080/8080\)|
|Classic network|Internet|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|CIDR block access|If you allow all Internet IP addresses to connect to your instance, enter 0.0.0.0/0. If you only allow specified IP addresses to remotely connect to your instance, see [Scenario 3: Allow remote access to your instance from only specified IP addresses](#).|1|
|Linux: SSH \(22\)|22/22|
|Custom TCP|Custom \(for example, 8080/8080\)|

For information about how to customize remote access ports, see [Modify the default remote access port](https://partners-intl.aliyun.com/help/doc-detail/51644.htm).

## Scenario 7: Allow an ECS instance in a security group under another account in the same intranet to remotely connect to your instance {#section_tkx_fyq_ngb .section}

If your account is in the same intranet as another account in the same region, and you want to allow remote access to an ECS instance in a security group of that account, add a security group rule by using the settings described in the following examples.

-   To allow an intranet IP address of an instance under another account to connect to your instance, add the security group rule described in the following table. For VPC instances, ensure that the instances under the two accounts can communicate with each other through Express Connect before you add a security group rule. For more information, see [Interconnect two VPCs under the same account](../../../../reseller.en-US/Peering connections/Interconnect two VPCs under the same account.md#).

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|CIDR block access|The private IP address of the peer instance|1|
    |Linux: SSH \(22\)|22/22|
    |Custom TCP|Custom, for example, 8080/8080|
    |Classic network|Intranet|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|CIDR block access|The intranet IP address of the peer instance. For security purposes, only single IP address authorization is supported \(for example, a.b.c.d/32\).|1|
    |Linux: SSH \(22\)|22/22|
    |Custom TCP|Custom, for example, 8080/8080|

-   To allow all ECS instances in a security group under another intranet account to connect to your instance, add the security group rule described in the following table. For VPC instances, ensure that the instances under the two accounts can communicate with each other through Express Connect before you add a security group rule. For more information, see [Connect two VPCs under the same account](../../../../reseller.en-US/Peering connections/Interconnect two VPCs under the same account.md#).

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|Security group access \(authorize other accounts\)|The ID of the security group to which the peer instance belongs. Enter the ID of the peer account.|1|
    |Linux: SSH \(22\)|22/22|
    |Custom TCP|Custom, for example, 8080/8080|
    |Classic network|Intranet|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|Security group access \(authorize other accounts\).|The ID of the security group to which the peer instance belongs. Enter the ID of the peer account.|1|
    |Linux: SSH \(22\)|22/22|
    |Custom TCP|Custom \(for example, 8080/8080\)|


## Scenario 8: Allow access to your instance through HTTP and HTTPS {#allowHttp .section}

If you host a website on your instance, you can add a security group rule to allow your users to access the website through HTTP or HTTPS.

-   To allow all Internet IP addresses to access your website, add the security rule described in the following table.

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|HTTP \(80\)|80/80|CIDR block access|0.0.0.0/0|1|
    |HTTPS \(443\)|443/443|
    |Custom TCP|Custom \(for example, 8080/8080\)|
    |Classic network|Internet|Inbound|Allow|HTTP \(80\)|80/80|CIDR block access|0.0.0.0/0|1|
    |HTTPS \(443\)|443/443|
    |Custom TCP|Custom, for example, 8080/8080|

-   To allow specified Internet IP addresses to access your website, add the security group rule described in the following table.

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Configuration is not required.|Inbound|Allow|HTTP \(80\)|80/80|CIDR block access|One or more Internet IP addresses of the hosts that you allow to access your website|1|
    |HTTPS \(443\)|443/443|
    |Custom TCP|Custom \(for example, 8080/8080\)|
    |Classic network|Internet|Inbound|Allow|HTTP \(80\)|80/80|CIDR block access|One or more Internet IP addresses of the hosts that you allow to access your website|1|
    |HTTPS \(443\)|443/443|
    |Custom TCP|Custom \(for example, 8080/8080\)|


**Note:** 

-   If your users cannot access your instance by using the `http://Internet IP address`, [verify if TCP port 80 works properly](https://partners-intl.aliyun.com/help/faq-detail/59367.htm).
-   Port 80 is the default port for the HTTP service. If you want to use another port \(for example, port 8080\), you must modify the listening port settings in the configuration file of the Web server.

