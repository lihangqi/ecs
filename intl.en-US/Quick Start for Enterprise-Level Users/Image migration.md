# Image migration {#concept_kqd_yjw_wdb .concept}

## Feasibility {#section_u24_mkw_wdb .section}

Before migrating an image, you must conduct a survey on the server to be migrated and evaluate whether image migration is used and whether this operation is feasible.

-   If the number of servers to be migrated is large, most servers contain system disks, and network conditions are unfavorable, image migration is not recommended. Image files are large, and image migration performed under such conditions may increase the migration time and labor costs.

-   If the application configurations on the servers to be migrated are complicated and not manually maintained, and network conditions are favorable, image migration is recommended. Although data disks do not support image migration, you can migrate images of system disks to Alibaba Cloud, and then synchronize data of data disks to data disks of Alibaba Cloud by means of file synchronization.


## Migration tools {#section_w24_mkw_wdb .section}

Alibaba Cloud Migration Tool, or Cloud Migration Tool for short, is a proprietary resource migration tool of Alibaba Cloud.

It supports resource migration, such as the operating system, applications, and application data in a computer disk, of physical machines, VMs \(virtual machines\), or cloud hosts to the image list in the ECS. Being lightweight and handy, Alibaba Cloud Migration Tool helps you balance the workload between your local and cloud hosts, or cloud hosts from different cloud platforms. For more information, see [what is Alibaba Cloud Migration Tool](../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool overview.md#).

## Procedure {#section_x24_mkw_wdb .section}

To migrate an image, follow these steps:

1.  Prepare for the migration.
    -   Prepare for the migration.
    -   Prepare the image format conversion tools and platforms.
    -   Check and prepare the operating system before exporting image files.
2.  Migrate your on-premises server. For more information, see [migrate to Alibaba Cloud by using Cloud Migration Tool](../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).
3.  Start ECS instances based on images. You can go to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) page, and create instances based on the new image files.

