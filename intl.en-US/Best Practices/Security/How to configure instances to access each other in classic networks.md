# How to configure instances to access each other in classic networks {#concept_fnt_kch_ffb .concept}

A security group is an instance-level firewall. To ensure the instance security, the minimum authorization principle should be observed for the setting of security group rules. This document introduces four safe methods of enabling intranet intercommunication for instances.

## Method 1. Authorize access to a single IP address {#section_gdp_wch_ffb .section}

-   Application scenario: intercommunication of a small number of instances over the intranet.
-   Advantage: Authorizing access to IP addresses makes the security group rules clear and easy to understand.
-   Disadvantage: When a great number of instances need to access each other over the intranet, it is limited by the quota of 100 security group rules. In addition, the maintenance workload will be high.
-   Configuration:
    1.  Select the instance that requires intercommunication, and click **Security Groups**.
    2.  Select the expected security group and click **Add Rules**.
    3.  Click **Ingress** and then click **Add Security Group Rule**.
    4.  Add security group rules as instructed below:
        -   **Action**: Allow.
        -   **Protocol Type**: Select the protocol type as needed.
        -   **Port Range**: Set the port range as needed. The format is “start port number/end port number”.
        -   **Authorization Type**: CIDR.
        -   **Authorization Objects**: Enter the expected intranet IP address for intranet intercommunication. The format must be a.b.c.d/32. Where, the subnet mask must be /32.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/154684304212634_en-US.png)


## Method 2. Join the same security group {#section_y3z_xch_ffb .section}

-   Application scenario: If your application architecture is relatively simple, you can add all the instances to the same security group. Such instances need no special rules as they can access each other over the intranet by default.
-   Advantage: Security group rules are clear and easy to understand.
-   Disadvantage: It is only applicable to simple application network architecture. When the network architecture is adjusted, the authorization method should be modified accordingly.

## Method 3. Bind instances with a security group that is created solely for intercommunication {#section_y3g_ych_ffb .section}

-   Application scenario: You can bind expected instances to a dedicated security group for intercommunication. This method applies to the network architecture with multiple layers of applications.
-   Advantage: This method is easy to implement, and allows you to quickly establish interconnection between instances. It is applicable to complicated network architecture.
-   Disadvantage: The instances need to be bound to multiple security groups and the security group rules are hard to comprehend.
-   Configuration:
    1.  Create a new security group with the name of “security group for intercommunication”. No rules are required for the new security group.
    2.  Add the expected instances to the newly created “security group for intercommunication”. The instances will be interconnected over the intranet as this is a default feature for instances in the same security group.

## Method 4. Security group authorization {#section_g4x_fdh_ffb .section}

-   Application scenario: If your network architecture is complicated, and the applications deployed on different instances have different service roles, you can select security group authorization.
-   Advantage: The security group rules are clear and easy to understand. Besides, intercommunication can be implemented across accounts.
-   Disadvantage: You need to configure a lot of security group rules.
-   Configuration:
    1.  Select the expected instance, and enter the **Security Groups** page.
    2.  Select the expected security group and click **Add Rules**.
    3.  Click **Ingress**, and then click **Add Security Group Rule**.
    4.  Add security group rules as described below:
        -   **Action**: Allow.
        -   **Protocol Type**: Select the protocol type as needed.
        -   **Port Range**: Set it as needed.
        -   **Authorization Type**: Security Group.
        -   **Authorization Objects**:
            -   **Allow Current Account**: Based on your networking requirements, select the security group IDs of the peer instances for intranet intercommunication in **Authorized Objects**.
            -   **Allow Other Accounts**: Enter the security group IDs of the peer instances in **Authorized Objects**. Enter the peer account ID in **Account ID**. You can query it in **Account Management** \> **Security Settings**.

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/154684304212635_en-US.png)

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/154684304212636_en-US.png)


## Suggestions {#section_gyk_5ch_ffb .section}

If too much access is granted by the security group in the early stage, it is recommended to reduce the authorization scope with the following procedure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/154684304212637_en-US.png)

In the figure, Delete 0.0.0.0 means to delete the original security group rule that allows the inbound access from the 0.0.0.0/0 address segment.

If the security group rules are changed improperly, the communications between your instances may be affected. Please back up the security group rules you want to change before changing the settings for timely recovery upon intercommunication problems.

A security group maps the role of an instance in the overall application architecture. We recommend that you plan the firewall rules based on the application architecture. For example, in the common three-tier Web application architecture, you can plan three security groups and bind them to instances deployed with applications or databases respectively:

-   Web layer security group: Open port 80.
-   Application layer security group: Open port 8080.
-   DB layer security group: Open port 3306.

