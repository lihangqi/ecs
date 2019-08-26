# Configure instances to access each other in classic networks {#concept_fnt_kch_ffb .concept}

A security group functions similar to a firewall for an instance. To ensure the security of an instance, the principle of least privilege should be observed when setting security group rules for it. This topic describes four recommended methods of enabling intranet intercommunication for instances by means of applying security groups.

## Method 1. Authorize access to IP addresses {#section_gdp_wch_ffb .section}

-   Application scenario: Intercommunication of a small number of instances over an intranet.
-   Advantage: Authorizing access to IP addresses makes the security group rules clear and easy to understand.
-   Disadvantage: When a large number of instances need to access each other over the intranet, the quota of 100 security group rules will become a restriction. In addition, the maintenance workload will be high.
-   Configuration:
    1.  Click the ID of the instance that requires intranet intercommunication, and click **Security Groups**.
    2.  Select the target security group and click **Add Rules**.
    3.  Click **Ingress** and then click **Add Security Group Rule**.
    4.  Add the following security group rules:
        -   **Action**: Allow.
        -   **Protocol Type**: Select the protocol type as needed.
        -   **Port Range**: Set the port range as needed. The format is “start port number/end port number”.
        -   **Authorization Type**: CIDR.
        -   **Authorization Objects**: Enter the target intranet IP address for intranet intercommunication. The format must be a.b.c.d/32. Note that the subnet mask must be /32.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/156162470112634_en-US.png)


## Method 2. Join the same security group {#section_y3z_xch_ffb .section}

-   Application scenario: If your application architecture is relatively simple, you can add all of your instances to the same security group. Such instances then require no custom rules as they can access each other over the intranet by default.
-   Advantage: Security group rules are clear and easy to understand.
-   Disadvantage: It is only applicable to a simple network architecture. When the network architecture is adjusted, the authorization method should be modified accordingly.
-   For more information, see [Add an instance to a security group](../../../../intl.en-US/Security/Security groups/Add an instance to a security group.md#).

## Method 3. Add instances to a security group that is created solely for intercommunication {#section_y3g_ych_ffb .section}

-   Application scenario: You can add the target instances to a dedicated security group for intercommunication. This method is recommended for a network architecture with multiple layers of applications.
-   Advantage: This method is easy to implement, and allows you to quickly establish interconnection between instances. Additionally, it is applicable to complicated network architectures.
-   Disadvantage: The instances need to be added to multiple security groups and the security group rules may be complex.
-   Configuration:
    1.  Create a new security group with the name of “security group for intercommunication”. No rules are required for the new security group.
    2.  Add the target instances to the newly created “security group for intercommunication”. The instances are then interconnected over the intranet by default.

## Method 4. Security group authorization {#section_g4x_fdh_ffb .section}

-   Application scenario: If your network architecture is complicated, and the applications deployed on different instances have different service roles, you can select security group authorization.
-   Advantage: The security group rules are clear and easy to understand, and intercommunication can be implemented across accounts.
-   Disadvantage: A large number of security group rules need to be correctly configured.
-   Configuration:
    1.  Select the target instance, and enter the **Security Groups** page.
    2.  Select the target security group and click **Add Rules**.
    3.  Click **Ingress**, and then click **Add Security Group Rule**.
    4.  Add security group rules as described below:
        -   **Action**: Allow.
        -   **Protocol Type**: Select the protocol type as needed.
        -   **Port Range**: Set the port range as needed. The format is “start port number/end port number”.
        -   **Authorization Type**: Security Group.
        -   **Authorization Objects**:
            -   **Allow Current Account**: Based on your networking requirements, select the security group IDs of the peer instances for intranet intercommunication in **Authorized Objects**.
            -   **Allow Other Accounts**: Enter the security group IDs of the peer instances in **Authorized Objects**. Enter the peer account ID in **Account ID**. You can query it in **Account Management** \> **Security Settings**.

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/156162470112635_en-US.png)

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/156162470212636_en-US.png)


## Suggestions {#section_gyk_5ch_ffb .section}

If you determine that a disproportionate level of access is granted by the applied security group, we recommend that you reduce the scope of authorization according to the following procedure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9796/156162470212637_en-US.png)

In the figure, Delete 0.0.0.0 means to delete the original security group rule that allows the inbound access from the 0.0.0.0/0 address segment.

If one or some security group rules are improperly configured, the communication between your instances may be affected. We recommend that you back up the security group rules you want to change before changing the settings so that you can easily recover the rules if an issue occurs.

A security group maps the role of an instance in the overall application architecture. We recommend that you plan the firewall rules based on the application architecture. For example, in a common three-tier Web application architecture, you can plan three security groups and associate them to instances deployed with applications or databases as follows:

-   Web layer security group: Open port 80.
-   Application layer security group: Open port 8080.
-   DB layer security group: Open port 3306.

