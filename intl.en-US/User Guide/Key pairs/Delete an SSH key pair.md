# Delete an SSH key pair {#concept_zzg_fq1_ydb .concept}

If you no longer require a key pair, you can delete it. Note that a deleted key pair is not recoverable. Existing instances that have used the key pair are not affected, and the deleted key pair name remains associated to the instance.

**Note:** 

-   If you delete a key pair that is still bound to an instance, its name is not available for you to create or import a key pair again. Otherwise, an error message “The key pair already exists” appears when you are using the same name to create or import a key pair.
-   If you delete a key pair that is not bound to an instance, its name is still available for you to create or import a key pair again.

Follow these steps to delete one or more key pairs:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Networks and Security** \> **SSH Key Pair**.
3.  Select one or more key pairs.
4.  Click **Delete**.

