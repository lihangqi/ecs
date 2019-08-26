# Best practices of the security group \(part 1\) {#concept_51170_zh .concept}

This article introduces how to configure the inbound rules of security groups.

Like a virtual firewall, a security group controls network access for one or more ECS instances. It is an important means of security isolation. When creating an ECS instance, you must select a security group. You can also add security group rules to control outbound and inbound access for all ECS instances in the same security group.

Before configuring the inbound rules for a security group, you should have learnt about the following information:

-    [Security group restrictions](../../../../reseller.en-US/Product Introduction/Network and security/Security group.md#)
-    [Default security group rules](../../../../reseller.en-US/User Guide/Security groups/Default security group rules.md#) 
-    [Set the inbound access of a security group](../../../../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#) 
-    [Set the outbound access of a security group](../../../../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md#) 

## General suggestions for security group practices {#section_imd_fn2_2fb .section}

Before you work with security groups, read the following suggestions:

-   The most important rule: A security group should be used as a whitelist.
-   The "minimum authorization" principle should be observed when you configure the inbound or outbound rules for applications. For example, you can allow a specific port \(such as port 80\).
-   It is not recommended to use one security group to manage all applications, because requirements must be different at different layers.
-   For distributed applications, different security groups should be used for different application types. For example, you should use different security groups for the Web, Service, Database and Cache layers to apply different inbound/outbound rules and permissions.
-   There is no need to set a separate security group for every instance, as this would unnecessarily add to management costs.
-   VPC should be preferred.
-   Do not assign Internet addresses to resources that require no Internet access.
-   Keep the rules of each security group as concise as possible. A single instance can join up to five security groups, and a security group can contain up to 100 security group rules, so an instance may be subject to hundreds of security group rules at the same time. You can aggregate all the assigned security rules to determine whether inbound or outbound traffic is permitted or not. However, overly complicated rules for a single security group can increase management complexity. For this reason, it is recommended to keep the rules of each security group as concise as possible.
-   The ECS console allows you to clone a security group and security group rules. If you want to modify an active security group and its rules, you should clone the security group and modify the cloned security group, avoiding any impacts on online applications.

    **Note:** Adjusting inbound or outbound rules of active security groups can be risky. Therefore, do not update those rules at will unless you know what you are doing.


## Set inbound access rules of security groups {#section_q3q_3n2_2fb .section}

The following are some suggestions about inbound rules of a security group.

## Do not use the 0.0.0.0/0 inbound rule {#section_sxy_jn2_2fb .section}

It is a common mistake to permit all inbound access without any restrictions. Using 0.0.0.0/0 means that all ports are open to external access. This is extremely insecure. The correct practice is to deny external access to all the ports first. Whitelist items should be configured for security groups. For example, if you need to expose web services, you should only open common TCP ports such as 80, 8080 and 443 by default. All other ports should be disabled.

```
{ "IpProtocol" : "tcp", "FromPort" : "80", "ToPort" : "80", "SourceCidrIp" : "0.0.0.0/0", "Policy": "accept"} ,
{ "IpProtocol" : "tcp", "FromPort" : "8080", "ToPort" : "8080", "SourceCidrIp" : "0.0.0.0/0", "Policy": "accept"} ,
{ "IpProtocol" : "tcp", "FromPort" : "443", "ToPort" : "443", "SourceCidrIp" : "0.0.0.0/0", "Policy": "accept"} ,
```

## Disable unneeded inbound rules {#section_eyb_nn2_2fb .section}

If your current inbound rules include 0.0.0.0/0, review the ports and services that must be exposed for your applications. If you do not want some ports to directly provide services for external applications, add denial rules for them. For example, if you have installed MySQL database services on the server, port 3306 should not be exposed to the Internet by default. You can add a denial rule, as shown below. Set the priority value to 100, which is the lowest priority.

```
{ "IpProtocol" : "tcp", "FromPort" : "3306", "ToPort" : "3306", "SourceCidrIp" : "0.0.0.0/0", "Policy": "drop", Priority: 100} ,
```

This setting prevents any other ports from accessing port 3306. However, this can block normal service requests as well. For this reason, you can authorize resources of another security group for inbound access.

## Authorize another security group for inbound access {#section_mp3_pn2_2fb .section}

Different security groups adopt inbound and outbound rules in accordance with the minimum authorization principle. Different application layers should use different security groups with corresponding inbound and outbound rules.

For example, different security groups are configured for distributed applications. However, directly authorizing IP addresses or CIDR network segments can be very difficult as different security groups cannot intercommunicate on the Internet. In this situation, you can authorize all resources of another security group to be directly accessible. For example, sg-web and sg-database security groups are created respectively for the Web and Database layers of your applications. In sg-database, you can add the following rule to authorize all resources in the sg-web security group to access port 3306.

```
{ "IpProtocol" : "tcp", "FromPort" : "3306", "ToPort" : "3306", "SourceGroupId" : "sg-web", "Policy": "accept", Priority: 2} ,
```

## Authorize another CIDR for inbound access {#section_lcj_sn2_2fb .section}

In classic networks, controlling network segments is difficult and you are recommended to use security group IDs to authorize inbound rules.

In VPC networks, you can plan IP addresses on your own and use different VSwitches to set different IP domains. Therefore, in VPC networks, you can deny any access by default but authorize access for your own VPC, namely directly authorizing trusted CIDR network segments.

```
{ "IpProtocol" : "icmp", "FromPort" : "-1", "ToPort" : "-1", "SourceCidrIp" : "10.0.0.0/24", Priority: 2} ,
{ "IpProtocol" : "tcp", "FromPort" : "0", "ToPort" : "65535", "SourceCidrIp" : "10.0.0.0/24", Priority: 2} ,
{ "IpProtocol" : "udp", "FromPort" : "0", "ToPort" : "65535", "SourceCidrIp" : "10.0.0.0/24", Priority: 2} ,
```

## Steps and instructions for changing security group rules {#section_o2h_5n2_2fb .section}

Changing security group rules can interrupt network communication among instances. To prevent required network communication from being impacted, try to permit required instances with the method below and then execute security group policies to narrow down your changes.

**Note:** After narrowing down the changes, check that service applications are running correctly before performing other required changes.

-   Create a new security group, add instances that need mutual access to it, and then perform the changes.
-   If the authorization type is **Security Group**, add the bound security group IDs of peer instances that require intercommunication into the authorization rules of the security group.
-   If the authorization type is **CIDR**, add Intranet IP addresses of peer instances that require intercommunication into the authorization rules of the security group.

For detailed instructions, see How to configure intercommunication among instances in the classic network.

