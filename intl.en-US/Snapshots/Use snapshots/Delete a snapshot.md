# Delete a snapshot {#task_1478465 .task}

You can delete snapshots that are no longer needed to free up space or when the maximum number of snapshots has been reached. This topic describes the procedure to delete a snapshot in the ECS console. This procedure applies to both manual snapshots and automatic snapshots.

-   You have created a snapshot. For more information, see [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#).
-   If a snapshot has been used to create custom images, you must delete those custom images before the snapshot can be deleted. For more information, see [Delete custom images](../reseller.en-US/Images/Custom image/Delete custom images.md#).

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.
3.  In the top navigation bar, select a region.
4.  Select one or more snapshots to be deleted and click **Delete** at the bottom of the page. 
5.  In the Delete dialog box that appears, select **Delete** or **Force Delete**. 

    **Note:** To delete snapshots that have been used to create cloud disks, you must select **Force Delete** and then Proceed to Forcibly Delete. After a snapshot is deleted, you cannot perform operations that depend on the status of the original snapshot data, such as the operation to [reinitialize a cloud disk](../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#).

6.  Click **OK**.

**More information**  


[../DNA0011860945/EN-US\_TP\_9908.md\#](../reseller.en-US/API Reference/Snapshots/DeleteSnapshot.md#)

