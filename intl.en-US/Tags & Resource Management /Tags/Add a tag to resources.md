# Add a tag to resources {#concept_a5f_p2j_zdb .concept}

If your account maintains multiple resources that are associated with each other in different ways, you can attach tags to your resources to categorize and manage the resources in a unified manner.

You can attach a maximum of 20 tags to each resource. You can attach and detachup to 20 tags \(separately or at a time\)toeach resource.

To attach resources with tags, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home).
2.  In the left-side navigation pane, select the resource type for the attach operation, such as **Instance**, **Disks**, **Snapshots**, **Images**, and **Security Groups**.
3.  Select the target region.
4.  Select the target resources in the resource list to attach tags.
5.  Click **Edit Tags** at the bottom of the resource list.

    **Note:** If the selected resources are instances, select **More** \> **Instance Settings** \> **Edit Tags**.

6.  In the dialog box:
    -   If the selected resource already has a created tag, click an existing tag, or select from the available tags.
    -   If the selected resource has no tags or you want to create a new tag, click **Create** and set **Key** and **Value**.

        **Note:** 

        -   **Key** is required whereas **Value** is optional.
        -   **Key** cannot start with aliyun, http://, or https://. The key is case-insensitive and can contain up to 64 characters.
        -   **Value** cannot start with http:// or https://. The value is case-insensitive and can contain up to 128 characters. It can also be empty.
        -   Any tag **Key** of a resource must be unique. An existing tag with the same key as a newly created tag will be overwritten.
        -   **Available Tags** and **Create** are grayed out if the selected resources are already attached with 20 tags. You must detach some tags before attaching new tags.
7.  Click **Confirm**.

To check if tags are successfully attached, use the **Edit Tags** function of the resource or click **Tags** in the left-side navigation pane of the ECS console. You can also click **Tags** with a tag symbol at the top of the resource list to filter resources.

