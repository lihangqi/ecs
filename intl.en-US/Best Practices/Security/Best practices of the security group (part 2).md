# Best practices of the security group \(part 2\) {#concept_51171_zh .concept}

This document introduces the following:

-   [Authorize](../../../../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#) and [revoke](../../../../reseller.en-US/API Reference/Security groups/RevokeSecurityGroup.md#) security groups.
-   [Join](../../../../reseller.en-US/API Reference/Security groups/JoinSecurityGroup.md#) and [leave](../../../../reseller.en-US/API Reference/Security groups/LeaveSecurityGroup.md#) security groups.

Alibaba Cloud provides two types of networks, namely **classic networks** and **VPC networks**. They support different security group rules:

-   For classic networks, you can set the following rules: intranet inbound, intranet outbound, Internet inbound and Internet outbound.
-   For VPC networks, you can set the following rules: intranet inbound and intranet outbound.

## Basic knowledge of intranet communication for security groups {#section_n13_bp2_2fb .section}

Firstly, learn about the following points about intranet communication for security groups:

-   By default, only the ECS instances in the same security group can access each other. In other words, the instances of the same account in different security groups are inaccessible to each other on the intranet. This applies to both classic and VPC networks. Therefore, the ECS instances in classic networks are secure over the intranet.
-   If you have two ECS instances in different security groups, and you want them to be inaccessible to each other over the intranet but they are actually accessible, you should check the intranet rule settings of your security group. If the intranet rules include the following items, you are recommended to reconfigure them.
    -   Allow all ports;
    -   The authorized object is a CIDR segment \(SourceCidrIp\): 0.0.0.0/0 or 10.0.0.0/8. For classic networks, the above rules can expose your intranet to external access.
-   If you want to implement network intercommunication among the resources of different security groups, you should adopt security group authorization. For intranet access, you are recommended to adopt the source security group authorization, instead of CIDR segment authorization.

## Attributes of security rules {#section_kqd_3p2_2fb .section}

Security rules mainly describe different access permissions with the following attributes:

-   Policy: authorization policies. The parameter value can be accept or drop.
-   Priority: priority levels. The priority levels are sorted by creation time in descending order. The rule priority ranges from 1 to 100. The default value is 1, which is the highest priority. A greater value indicates a lower priority.
-   NicType: network type. In security group authorization \(namely SourceGroupId is specified while SourceCidrIp is not\), you must specify NicType as intranet.
-   Description:
    -   IpProtocol: IP protocol. Values: tcp, udp, icmp, gre or all. The value "all" indicates all the protocols.
    -   PortRange: the range of port numbers related to the IP protocol:
        -   When the value of IpProtocol is tcp or udp, the port range is 1-65535. The format must be "starting port number/ending port number". For example, "1/200" indicates that the port range is 1-200. If the input value is "200/1", an error will be reported when the interface is called.
        -   When the value of IpProtocol is icmp, gre or all, the port range is -1/-1, indicating no restriction on ports.
    -   If security group authorization is adopted, the SourceGroupId \(namely the source security group ID\) should be specified. In this case, you can choose to set SourceGroupOwnerAccount based on whether it is cross-account authorization. SourceGroupOwnerAccount indicates the account to which the source security group belongs.
    -   If CIDR authorization is adopted, SourceCidrIp should be specified. SourceCidrIp is the source IP address segment, which must be in the CIDR format.

## Create a rule to authorize inbound requests {#section_ujb_mp2_2fb .section}

When you create a security group in the console or through the API, the default inbound rule is deny all, that is, all the inbound requests are rejected by default. This does not apply to all the situations, so you need to configure inbound rules accordingly.

If you need to enable port 80 on the Internet to provide HTTP services for external applications, do not impose any restrictions on IP network segments but set it to 0.0.0.0/0 in order to allow all inbound requests. For this purpose, you can refer to the following properties where console parameters are outside of brackets and OpenAPI parameters are within brackets \(no difference is made if both parameters are the same\).

-   NIC Type \(NicType\): Internet \(internet\). For VPCs, simply enter intranet to implement Internet access through EIP.
-   Action \(Policy\): allow \(accept\).
-   Rule Direction \(NicType\): inbound.
-   Protocol Type \(IpProtocol\): TCP \(tcp\).
-   Port Range \(PortRange\): 80/80.
-   Authorized Objects \(SourceCidrIp\): 0.0.0.0/0.
-   Priority \(Priority\): 1.

**Note:** These recommended values apply only to the Internet. For intranet requests, you are not recommended to use CIDR network segments. Please refer to [Do not use CIDR or IP authorization for intranet security group rules of classic networks](#section_plq_zn2_2fb).

## Create a rule to deny inbound requests {#section_lr5_pp2_2fb .section}

To deny inbound requests, you only need to configure a denial policy with a low priority. In this way, you can configure another rule with a higher priority to overwrite this rule when needed. For example, the following explains how to deny access to port 6379.

-   NIC Type \(NicType\): Intranet \(intranet\).
-   Action \(Policy\): forbid \(drop\).
-   Rule Direction \(NicType\): inbound.
-   Protocol Type \(IpProtocol\): TCP \(tcp\).
-   Port Range \(PortRange\): 6379/6379.
-   Authorized Objects \(SourceCidrIp\): 0.0.0.0/0.
-   Priority \(Priority\): 100.

## Do not use CIDR or IP authorization for intranet security group rules of classic networks {#section_plq_zn2_2fb .section}

For ECS instances in classic networks, no intranet inbound rules are enabled by default. Always exercise caution for intranet authorization.

**Note:** For the sake of security, it is not recommended to enable any authorization that is based on CIDR network segments.

For elastic computing, intranet IP addresses change frequently and the network segment to which the IP addresses map varies dynamically. For this reason, you are only recommended to authorize intranet access through security groups in classic networks.

For example, if you build a Redis cluster in the sg-redis security group and only permit certain computers \(such as those in sg-web\) to access the servers of this Redis cluster, you do not need to configure CIDR. Instead, you only need to add an inbound rule to specify relevant security group IDs.

-   NIC Type \(NicType\): Intranet \(intranet\).
-   Action \(Policy\): allow \(accept\).
-   Rule Direction \(NicType\): inbound.
-   Protocol Type \(IpProtocol\): TCP \(tcp\).
-   Port Range \(PortRange\): 6379/6379.
-   Authorized Objects \(SourceGroupId\): sg-web.
-   Priority \(Priority\): 1.

For instances in a VPC, if you have planned an IP address range through multiple VSwitches, you can use the CIDR settings as the security group inbound rules. However, if your VPC network segment is ambiguous, you are recommended to prioritize security groups for inbound rules.

## Add ECS instances requiring intercommunication into the same security group {#section_bwv_sp2_2fb .section}

A single ECS instance can join up to five security groups, and the ECS instances in the same security group can intercommunicate over the intranet. If you have created multiple security groups during planning and directly setting multiple security rules is too complicated, you can create a security group and add the instances that require intranet communication to it.

Different security groups may have different network types. More importantly, an ECS instance in a classic network can only join a security group created for classic networks. An ECS instance in a VPC can only join a security group created for the same VPC.

Additionally, you are not recommended to add all the ECS instances into the same security group as this will make the configuration of security group rules quite messy. For a large or medium-sized application, each server group has a different role and it is important to plan inbound and outbound requests in a rational manner.

In the console, you can add an instance to a security group by following the description in [Join a security group](../../../../reseller.en-US/Security/Security groups/Add an instance to a security group.md#).

``` {#codeblock_7hs_17c_dli}
def join_sg(sg_id, instance_id):
    request = JoinSecurityGroupRequest()
    request.set_InstanceId(instance_id)
    request.set_SecurityGroupId(sg_id)
    response = _send_request(request)
    return response
# send open api request
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
```

## Remove an ECS instance from a security group {#section_w1t_lq2_2fb .section}

If an ECS instance is added to an inappropriate security group, your services may be exposed or blocked. In this case, you can remove the ECS instance from the security group. Before the removal, however, you must ensure that your ECS instance has been added to another security group.

**Note:** You are recommended to perform sufficient tests before the removal as this may cause intercommunication failure between the instance and other instances in the current security group.

The corresponding Python snippets are as follows:

``` {#codeblock_zhh_e7w_4on}
def leave_sg(sg_id, instance_id):
    request = LeaveSecurityGroupRequest()
    request.set_InstanceId(instance_id)
    request.set_SecurityGroupId(sg_id)
    response = _send_request(request)
    return response
# send open api request
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
```

## Define reasonable names and tags for security groups {#section_dx4_4q2_2fb .section}

Reasonable names and descriptions for security groups help you quickly identify the meanings of complicated rule combinations. You can change security group names and descriptions as needed.

Also, you can set tags for security groups. You can manage your own security groups by grouping them with tags. To [set tags](../../../../reseller.en-US/Tags & Resource Management /Tags/Add a tag to resources.md#), you can directly configure them in the console or by using APIs.

## Delete undesired security groups {#section_f3r_tq2_2fb .section}

Security rules of security groups are like whitelist and blacklist items. Therefore, you are recommended to delete unnecessary security groups to prevent unexpected problems caused by adding an ECS instance to those groups by mistake.

