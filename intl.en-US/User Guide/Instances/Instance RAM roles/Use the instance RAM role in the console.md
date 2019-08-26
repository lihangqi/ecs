# Use the instance RAM role in the console {#concept_v3v_zct_xdb .concept}

## Limits {#section_x4c_cdt_xdb .section}

Instance RAM roles have the following limits:

-   Instance RAM roles are only applicable to VPC-Connected instances.
-   An ECS instance can only be authorized to one instance RAM role at a time.
-   After an instance RAM role is bound to an ECS instance, if you want to access other cloud services \(such as OSS, SLB, or ApsaraDB for RDS\) from applications within the ECS instance, you must obtain the authorization credential of the instance RAM role by using [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#). For more information, see [obtain authorization credentials](#).
-   If you are using an instance RAM role through a RAM user account, you must use a primary account to [authorize a RAM user to use the instance RAM role](#).

## Prerequisites {#section_z4c_cdt_xdb .section}

You must have activated the RAM service. See [activation method](../../../../reseller.en-US/Pricing/Activation method.md#) to activate the RAM service.

## 1. Create an instance RAM role {#step2 .section}

1.  Log on to the [RAM console](https://partners-ram.console.aliyun.com/#/overview).
2.  In the left-side navigation pane, click **Roles**.
3.  Click **Create Role**.
4.  In the dialog box:
    1.  Select **Service Role** for **Role Type**.
    2.  Select **ECS Elastic Compute Service** for **Type**.
    3.  Enter a role name and description, for example, EcsRamRoleDocumentTesting.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15432152595501_en-US.png)

    4.  Click **Create**.

## 2. Authorize the instance RAM role {#section_q1m_sst_xdb .section}

1.  Log on to the [RAM console](https://partners-ram.console.aliyun.com/#/overview).
2.  In the left-side navigation pane, click **Policies**.
3.  Click **Create Authorization Policy**.
4.  In the dialog box:
    1.  Select **Blank Template** for **authorization policy template**.
    2.  Enter a **Authorization Policy Name** and **Policy Content**. In this example, they are EcsRamRoleDocumentTestingPolicy.

        **Note:** For information about how to write the authorization policy in JSON format, see [policy syntax structure](../../../../reseller.en-US//Policy Language/Policy syntax structure.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15432152605502_en-US.png)

    3.  Click **Create Authorization Policy**.
5.  In the left-side navigation pane, click **Roles**.
6.  Select a role, for example, EcsRamRoleDocumentTesting, and click **Authorize**.
7.  Enter the **Authorization Policy Name** and select it from the drop-down menu. In this example, EcsRamRoleDocumentTestingPolicy is selected.
8.  Click the icon **\>** to select the policy name, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15432152605503_en-US.png)


## 3. Bind an instance RAM role {#section_mpc_cdt_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target ECS instance and select **More** \> **Instance Settings** \> **Bind/Unbind RAM Role**.
5.  Select **Bind** for Action, select a role \(for example, EcsRamRoleDocumentTesting\), and then click **OK**.

## 4. \(Optional\). Unbind an instance RAM role {#section_wn3_bwt_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target ECS instance and select **More** \> **Instance Settings** \> **Bind/Unbind RAM Role**.
5.  Select **Unbind** for **Action**, and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15432152605506_en-US.png)


## 5. \(Optional\). Replace an instance RAM role {#section_wfl_2wt_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target ECS instance and select **More** \> **Instance Settings** \> **Bind/Unbind RAM Role**.
5.  Select **Bind** for **Action**, select another instance RAM role in the list of **RAM Role**, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9665/15432152605507_en-US.png)


## 6. \(Optional\). Obtain authorization credentials {#Token .section}

To access an internal application of an ECS instance, you can obtain STS credentials of the instance RAM role \(which is part of the metadata of an instance\) to access the role-authorized permissions and resources. The credential is updated periodically. To access an instance by STS, follow these steps:

1.  Connect to the target ECS instance.
2.  Obtain the STS credential of the instance RAM role. In this example, it is EcsRamRoleDocumentTesting:
    -   For a Linux instance: run `curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting`.
    -   For a Windows instance: see [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#).
3.  Get the credential. An example return is as follows:

    ```
    
    {
    "AccessKeyId" : "XXXXXXXXX",
    "AccessKeySecret" : "XXXXXXXXX",
    "Expiration" : "2017-11-01T05:20:01Z",
    "SecurityToken" : "XXXXXXXXX",
    "LastUpdated" : "2017-10-31T23:20:01Z",
    "Code" : "Success"
    }
    ```


## 7. \(Optional\). Authorize a RAM user to use the instance RAM role {#Authorize .section}

**Note:** You must grant the RAM user with the **PassRole** permission to use the instance RAM role feature. Without the **PassRole** permission, a RAM user cannot carry out the permission of the authorization policy that is attached to the RAM user.

Log on to the RAM console and authorize the target RAM user by means of [authorizing RAM users](../../../../reseller.en-US/Quick Start/Authorize RAM users.md#) to complete the authorization. The following is an authorization policy example:

```
{
        "Version": "2016-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": [
                "ecs: [ECS RAM Action]",
                "ecs: CreateInstance",
                "ecs: AttachInstanceRamRole",
                "ecs: DetachInstanceRAMRole"
            ],
            "Resource": "*"
            },
            {
        "Effect": "Allow",
        "Action": "ram:PassRole",
        "Resource": "*"
            }
        ]
}
```

The parameter \[ECS RAM Action\] indicates that a RAM user can be authorized for certain actions. For more information, see [authorization rules](../../../../reseller.en-US/API Reference/Authorization rules.md#).

## References {#section_bxr_pwt_xdb .section}

-   Click the following link to learn how to [use the instance RAM role by calling APIs](reseller.en-US/User Guide/Instances/Instance RAM roles/Use the instance RAM role by calling APIs.md#).
-   Click the following link to see how to [access other cloud products by using the instance RAM role](https://partners-intl.aliyun.com/help/doc-detail/54579.htm).

