# Scenarios {#concept_ngr_vht_xdb .concept}

This topic details several scenarios of VPC-Connected and Classic network-connected security groups.

**Note:** For more information about how to create a security group and corresponding rules, see [create a security group](reseller.en-US/User Guide/Security groups/Create a security group.md#) and [add a security group rule](reseller.en-US/User Guide/Security groups/Add security group rules.md#).

-   [Scenario 1: Enable intranet communication](#) 

    If you want to copy files between two Classic network-connected ECS instances owned by different accounts or in different security groups, you must first enable intranet communication between both instances by configuring security group rules before you can copy files.

-   [Scenario 2: Allow remote connection from specified IP addresses only](#) 

    If your ECS instance is remotely accessed by hackers, you can modify the port for remote connection and then configure security group rules to allow access from specified IP addresses only.

-   [Scenario 3: Allow an instance to access specified IP addresses only](#) 

    If the security of your ECS instance is compromised, you can configure security group rules to allow the instance access to specified IP addresses.

-   [Scenario 4: Allow remote connection to an ECS instance](#) 

    If you need to remotely access your ECS instance, you can configure a corresponding security group rule.

-   [Scenario 5: Allow access to an ECS instance over HTTP or HTTPS service](#) 

    If you build a website on your instance, you can configure security group rules to enable your users to access the website.


## Scenario 1: Enable intranet communication {#intranetCommunication .section}

Security group rules can be used in the following cases to enable intranet communication between ECS instances that belong to different accounts or security groups in the same region:

-   Case 1: Instances belong to one region and one account.
-   Case 2: Instances belong to one region but different accounts.

**Note:** For VPC-connected ECS instances,

-   If they are in one VPC, you can configure their security group rules to enable intranet communication.
-   If they are in different VPCs, or owned by different accounts in the same region, Express Connect is the only option to establish intranet communication. For more information, see [establish an intranet connection between VPCs under different accounts](https://partners-intl.aliyun.com/help/doc-detail/44842.htm).

**Case 1: Instances belong to one region and one account**

For two instances in one region but owned by one account, if they are in one security group, intranet communication is enabled by default. If they are in different security groups, you must configure security group rules to enable intranet communication according to the network types.

-   VPC

    If they are in one VPC, add a rule in each security group to authorize shared access between the security groups. The rule must be as follows.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Priority|Authorization Type|Authorization Object|
    |:--|:-------------|:-------------------|:------------|:---------|:-------|:-----------------|:-------------------|
    |N/A|Inbound|Allow|Select the required protocol|Set the required port range|1|Security group access \(authorize this account\)|Select the Security Group ID on which you want to allow access to the instance|

-   Classic network

    Add a rule in each security group to authorize shared access between the security groups. The rule must be as follows.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Priority|Authorization Type|Authorization Object|
    |:--|:-------------|:-------------------|:------------|:---------|:-------|:-----------------|:-------------------|
    |Intranet|Inbound|Allow|Select the required protocol|Set the required port range|1|Security group access \(authorize this account\)|Select the Security Group ID on which you want to allow access to the instance|


**Case 2: Instances belong to one region but different accounts**

The following information is for Classic network-connected ECS instances only.

Authorize shared access between security groups. For example:

-   User A owns a Classic network-connected ECS instance in the China East 1 region, named Instance A, with the private IP address A.A.A.A. The security group is Group A.
-   User B owns a Classic network-connected ECS instance in the China East 1 region, named Instance B, with the private IP address B.B.B.B. The security group is Group B.
-   Add a rule in Group A to authorize access of Instance A to Instance B, as shown in the following table.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Intranet|Inbound|Allow|Select the required protocol |Set the required port range|Security group access \(authorize other accounts\) |Type the account ID of User B and the security group ID of Group B|1|

-   Add a rule in Group B to authorize access of Instance B to Instance A, as shown in the following table.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Intranet|Inbound|Allow |Select the required protocol|Set the required port range|Security group access \(authorize other accounts\)|Type the account ID of User A and the security group ID of Group A|1|

    **Note:** To guarantee the security of your instances, when you are configuring an intranet inbound rule for a Classic network-connected security group, **Security Group Access** is the top priority for **Authorization Type**. If you select **Address Field Access**, you must enter an IP address with CIDR prefix, `/32`, in the format of a.b.c.d/32. Only IPv4 is supported.


## Scenario 2: Allow remote connection from specified IP addresses only {#specifyIpAccess .section}

If you want to allow remote connection to your instance from the specified public IP addresses, add the following rule. In this example, remote connection to an instance on TCP Port 22 from a specified IP address is allowed.

|Network Type|NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
|:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
|VPC|N/A|Inbound|Allow|SSH\(22\)|22/22|Address field access|The IP address to allow access, such as 1.2.3.4.|1|
|Classic network|Internet|

## Scenario 3: Allow an instance to access specified IP addresses only {#specifyInstanceAccess .section}

If you want your instance to access specified IP addresses, add the following rules to its security group.

1.  Add the following rule to drop any access to all public IP addresses. The priority must be lower than the rule in step 2.

    |Network Type|NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|N/A|Inbound|Drop|All|-1/-1|Address field access|0.0.0.0/0|2|
    |Classic network|Internet|

2.  Add the following rule to allow access to the specified IP address, with a higher priority than that in step 1.

    |Network Type|NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|N/A|Outbound|Allow|Select the required protocol|Set the required port range|Address field access|Type the specified IP address, such as 1.2.3.4|1|
    |Classic network|Internet|


After you add the rules, connect to the instance and try to `ping` it or`telnet` to the instance from a specified IP address. If the instance can be accessed by the specified IP address, the rule is successfully applied.

## Scenario 4: Allow remote connection to an ECS instance {#allowRemoteAccess .section}

You may want to connect to your instance in the following cases:

-   Case 1: Allow remote connection to your instance from the Internet.
-   Case 2: Allow remote connection to your instance from intranet.

**Case 1: Allow remote connection to your instance from the Internet**

To allow remote connection to your instance from the Internet, add the following rule according to the network type and the operating system of your instance.

-   VPC

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |N/A|Inbound|Allow|Windows: RDP\(3389\)|3389/3389|Address field access|To allow Internet access from any public IP address, type 0.0.0.0/0. To allow Internet access from a specified Internet IP address, see [scenario 2](#).|1|
    |Linux: SSH \(22\)|22/22|
    |Custom TCP|Customized|

-   Classic network

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Internet|Inbound|Allow|Windows: RDP\(3389\)|3389/3389|Address field access|To allow Internet access from any public IP address, type 0.0.0.0/0. To allow Internet access from a specified Internet IP address, see [Scenario 2](#).|1|
    |Linux: SSH\(22\)|22/22|
    |Custom TCP|Customized|


To customize the port for remote connection, see [modify the default remote access port](https://partners-intl.aliyun.com/help/doc-detail/51644.htm).

**Case 2: Allow remote connection to your instance from intranet**

If you have enabled intranet communication between instances that belong to one region but different accounts, and you want to allow the instances in different security groups to connect to each other, add the following rules as needed.

-   To allow a private IP address to connect to an instance.
    -   VPC

        Make sure that an intranet communication has been built between both accounts by using [Express Connect](https://partners-intl.aliyun.com/help/doc-detail/44843.htm), and then add any one of the following rule.

        |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
        |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
        |N/A|Inbound|Allow|Windows: RDP\(3389\)|3389/3389|Address field access|Specify the private IP address of the peer instance|1|
        |Linux: SSH \(22\)|22/22|
        |Custom TCP|Customized|

    -   Classic network

        Add any one of the following rules.

        |NIC|Rule direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
        |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
        |Intranet|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|Address field access|Specify the private IP address of the peer instance. To secure the instance, only an IP address with CIDR prefix, `/32`, in the format of a.b.c.d/32, is allowed.|1|
        |Linux: SSH \(22\)|22/22|
        |Custom TCP|Customized|

-   To allow all the instances in a security group of one account to connect to your instance:
    -   VPC

        Make sure that an intranet communication is built between both accounts by using [Express Connect](https://partners-intl.aliyun.com/help/doc-detail/44843.htm), and then add any one of the following rule.

        |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
        |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
        |N/A|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|Security group access \(authorize other accounts\)|Type the account ID of the peer and the security group ID|1|
        |Linux: SSH\(22\)|22/22|
        |Custom TCP|Customized|

    -   Classic network

        Add any one of the following rules.

        |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
        |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
        |Intranet|Inbound|Allow|Windows: RDP \(3389\)|3389/3389|Security group access \(authorize other account\)|Type the account ID of the peer and the security group ID|1|
        |Linux: SSH\(22\)|22/22|
        |Custom TCP|Customized|


## Scenario 5: Allow access to an ECS instance over HTTP or HTTPS service {#allowHttp .section}

If you have built a website on your instance and want users to visit the site over HTTP or HTTPS service, add any one of the following rules.

-   VPC

    To allow any public IP addresses access your site, add any one of the following rules.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |N/A|Inbound|Allow|HTTP\(80\)|80/80|Address field access|0.0.0.0/0|1|
    |HTTPS\(443\)|443/443|
    |Custom TCP|Customized, such as 8080/8080|

-   Classic network

    To allow all public IP addresses to access your site, add any one of the following rules.

    |NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |Internet|Inbound|Allow|HTTP\(80\)|80/80|Address field access|0.0.0.0/0|1|
    |HTTPS \(443\)|443/443|
    |Custom TCP|Customized, such as 8080/8080|


**Note:** 

-   If users cannot access your instance by using `http://Public IP address`, [verify if TCP port 80 works properly](https://partners-intl.aliyun.com/help/faq-detail/59367.htm).
-   TCP Port 80 is the default port for HTTP services. If you want to use other ports, modify the port in the configuration file of the Web server.

