# Disaster recovery solutions {#concept_qzk_qjv_xfb .concept}

Disaster recovery solutions help guarantee the running stability and data security of your IT system. Specifically, the solutions incorporate data backup and disaster recovery of systems and applications. Alibaba Cloud ECS allows you to use snapshots and images for data backup.

## Disaster recovery methods {#section_ogk_ynv_xfb .section}

-   **Snapshot backup**

    Alibaba Cloud ECS allows you to back up system disks and data disks with snapshots. Currently, Alibaba Cloud provides the Snapshot 2.0 service, which features a higher snapshot quota and a more flexible automatic task strategy than previous snapshot services, helping to reduce impact on business I/O. When snapshots are used for data backup, the first backup is a full backup, followed by incremental backups. The backup duration depends on the amount of data to be backed up.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9575/15554085725243_en-US.jpg)

    As shown in the preceding figure, Snapshot 1, Snapshot 2, and Snapshot 3, are the first, second, and third snapshots of a disk. The file system checks the disk data by blocks. When a snapshot is created, only the blocks with changed data are copied to the snapshot. Alibaba Cloud ECS allows you to configure manual or automatic snapshot backup. With automatic backup, you can specify the time of day \(24 options, on the hour\), recurring day of week \(Monday through Sunday\), and retention time for snapshot creation. The retention time is customizable, and you can set a value from 1 to 65,536 days or choose to save snapshots permanently.

-   **Snapshot rollback**

    If exceptions occur in your system and you need to roll back a disk to a previous state, you can [roll back the disk](../reseller.en-US/Block storage/Block storage/Roll back a cloud disk.md#) so long as it has a corresponding snapshot created. Note:

    -   Rolling back a disk is an irreversible action. After disk rollback is completed, data cannot be restored. Exercise caution when performing this action.

    -   After a disk is rolled back, data will be irretrievably lost from the creation time of the snapshot to the current time.

-   **Image backup**

    An image file is equivalent to a replica file that contains all the data from one or more disks \(a system disk or both the system disk and data disks\). All image backups are full backups and can only be triggered manually.

-   **Image recovery**

    You can create custom images from snapshots to include the operating system and data environment in the image. The custom images can then be used to create multiple instances with the same operating system and data environment. For the configuration of snapshots and images, see [Snapshots](../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) and [Images](../reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

    **Note:** Custom images cannot be used across regions.


## Technical metrics {#section_lzx_ynv_xfb .section}

RTO and RPO: related to the amount of data, usually at an hourly level.

## Scenarios {#section_qq5_znv_xfb .section}

-   **Backup and restoration**

    Alibaba Cloud ECS allows you to back up system disks and data disks with snapshots and images. If incorrect data is stored on a disk due to data errors caused by application errors, or hackers exploiting application vulnerabilities for malicious access, you can use the snapshot service to restore the disk to a desired state. In addition, Alibaba Cloud ECS allows you to reinitialize disks with images or purchase new ECS instances with a custom image.

-   **Disaster recovery application**

    Alibaba Cloud ECS supports the implementation of disaster recovery architecture. For example, you can buy and use a Server Load Balancer \(SLB\) at the front end of an application, and deploy at least two ECS instances at the back end of the same application. Alternatively, you can implement an Auto Scaling solution using the auto scaling technology provided by Alibaba Cloud by defining how to use the ECS resources. In this way, even if one of the ECS instances fails or resources are overused, business continuity will not be interrupted, thus realizing disaster recovery. Take the deployment of ECS instances in two Internet Data Centers \(IDCs\) in the same city for example:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65023/155540857234740_en-US.png)

    -   A cluster of ECS instances is deployed in both IDCs. At the access side, SLBs are used for load balancing between the two IDCs.
    -   The Region Master nodes in both IDCs are identical and operate in active/standby mode. The failure of one node does not affect the ECS control function.
    -   To switch the control node of ECS instances in the case of IDC failure, the middleware domain name is associated anew as it is used for controlling the cluster. If the IDC of the control node experiences problems, the middleware domain name needs to be associated with the control node of the other IDC.

