# Implement access control by using RAM {#concept_stg_4pd_zdb .concept}

This topic describes how to use Resource Access Management \(RAM\) to control access to ECS resources at the account level.

## Scenarios {#section_hlx_szr_lgb .section}

RAM is a resource access control service provided by Alibaba Cloud. For more information, see [What is RAM?](../../../../intl.en-US/Product Introduction/What is RAM?.md). The following section describes how RAM is used to implement access control:

-   **RAM users**: If you have purchased one or more ECS instances and multiple RAM users in your organization \(such as employees, systems, or applications\) need to access the instances, you can create an authorization policy that only grants specific RAM users access to these instances. This eliminates the risk of disclosing the AccessKey of your Alibaba Cloud account, which helps maintain account security.
-   **RAM user groups**: You can create multiple user groups and grant different permissions to these user groups so that all RAM users in each user group are assigned the same permissions at the same time. For example:
    -   You can associate a user group with an authorization policy which denies access to specific ECS resources from IP addresses that are outside your corporate network.
    -   You can add and remove a RAM user to and from different user groups when the access control requirements of this RAM user change. For example, you have two user groups, SysAdmins and Developers, which grant different permissions for system administrators and developers.
        -   SysAdmins: This user group needs permissions to create and manage ECS instances. Therefore, you can associate the SysAdmins group with an authorization policy that allows its group members to perform all ECS operations, including the creation and management of ECS instances, images, snapshots, and security groups.
        -   Developers: This user group only needs permissions to use ECS instances. Therefore, you can associate the Developers group with an authorization policy that allows its group members to call the DescribeInstances, StartInstance, StopInstance, RunInstance, and DeleteInstance operations.

## Authorization policies {#section_vng_gv0_sch .section}

Authorization policies are categorized into **System Policy** and **Custom Policy**.

-   **System Policy**: the default authorization policies provided by Alibaba Cloud. Some commonly used system policies for ECS instances are as follows:
    -   AliyunECSReadOnlyAccess: grants read-only access to ECS instances.
    -   AliyunECSFullAccess: grants full administrative access to ECS instances.
    -   AliyunECSImageImportDefaultRole: grants the permission to [import custom images](../../../../intl.en-US/Images/Custom image/Import images/Import custom images.md#).
    -   AliyunECSImageExportDefaultRole: grants the permission to [export custom images](../../../../intl.en-US/Images/Custom image/Export custom images.md#).
    -   AliyunECSNetworkInterfaceManagementAccess: grants the permission to manage [ENIs](../../../../intl.en-US/Network/Elastic Network Interfaces/ENI overview.md#).
-   **Custom Policy**: the user-defined authorization policies. This policy type is suitable for users who are familiar with various Alibaba Cloud APIs and require fine-grained access control. For more information, see [Step 2](#).

## Step 1: Create a RAM user {#section_93p_xwm_1f5 .section}

Follow this procedure to create a RAM user:

1.  Log on to the [RAM console](https://ram.console.aliyun.com/policies/new).
2.  In the left-side navigation pane, choose **Identities** \> **Users**.
3.  On the Users page, click **Create User**. *For more information about how to create a RAM user, see* [Create a RAM user](../../../../intl.en-US/User Guide/RAM users/Create a RAM user.md#) in the RAM documentation.

## \(Optional\) Step 2: Create a custom authorization policy {#section_vjv_nz8_x3h .section}

Follow this procedure to create a custom authorization policy:

1.  In the left-side navigation pane, choose **Permissions** \> **Policies**.
2.  On the Policies page, click **Create Policy**.
3.  On the Create Custom Policy page, set **Policy Name** and **Note**. For example, set Policy Name to createEcs and Note to Permission to create ECS resources.
4.  Select **Script** for Configuration Mode.

    **Note:** You can also select **Visualized** for Configuration Mode to complete the policy settings without referring to [Authentication rules](../../../../intl.en-US/API Reference/Authentication rules.md#).

5.  Set the parameters in the **Policy Document** section based on the JSON template.

    For the values of the Action and Resource parameters, see [Authentication rules](../../../../intl.en-US/API Reference/Authentication rules.md#). *For the values of other parameters, see* [Policy elements](../../../../intl.en-US/User Guide/Policies/Policy language/Policy elements.md#) in the RAM documentation.

    -   Example policy 1: Allow a RAM user to create pay-as-you-go instances.

        ``` {#codeblock_2dl_2rw_333}
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeImages", 
                          "vpc:DescribeVpcs", 
                          "vpc:DescribeVSwitches", 
                          "ecs:DescribeSecurityGroups", 
                          "ecs:DescribeKeyPairs",
                          "ecs:DescribeTags", 
                          "ecs:RunInstances"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

    -   Example policy 2: Allow a RAM user to create subscription instances. Note that bss related operations are used to view and pay subscription orders, and the corresponding system policy is `AliyunBSSOrderAccess`.

        ``` {#codeblock_alp_hks_kfy}
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeImages", 
                          "vpc:DescribeVpcs", 
                          "vpc:DescribeVSwitches", 
                          "ecs:DescribeSecurityGroups", 
                          "ecs:DescribeKeyPairs",
                          "ecs:DescribeTags", 
                          "ecs:RunInstances",
                          "bss:DescribeOrderList",
                          "bss:DescribeOrderDetail",
                          "bss:PayOrder",
                          "bss:CancelOrder"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

    -   Example policy 3: Allow a RAM user to query instance and disk information after the RAM user creates an ECS instance.

        ``` {#codeblock_ndb_jdu_67h}
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                            "ecs:DescribeInstances", 
                            "ecs:DescribeDisks"
                  ],
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

6.  Click **OK**.

## Step 3: Authorize the RAM user {#section_u2f_nxl_87g .section}

Follow this procedure to authorize the RAM user:

1.  In the left-side navigation pane, choose **Identities** \> **Users**.
2.  On the Users page, find the RAM user created in step 1. Then in the **Actions** column, click **Add Permissions**.
3.  In the **Select Policy** section of the Add Permissions pane, select one or more system policies or custom policies to associate with the RAM user.
4.  Click **OK**.

