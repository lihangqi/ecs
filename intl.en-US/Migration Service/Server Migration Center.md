# Server Migration Center {#concept_1357671 .concept}

Server Migration Center \(SMC\) is a migration platform developed by Alibaba Cloud. SMC can help you migrate one or more source servers to Alibaba Cloud.

## Overview {#section_xey_7yk_n2o .section}

SMC can help you migrate one or more source servers to Alibaba Cloud. The source servers include IDC servers, virtual machines, cloud hosts on other cloud platforms, and other types of servers. For more information, see [SMC documentation](../../reseller.en-US/Product Introduction/What is SMC?.md#).

## Benefits {#section_atd_sc2_1ff .section}

SMC has the following benefits:

-   An underlying environment independent of migration sources

    SMC supports physical-to-cloud \(P2C\), virtual-to-cloud \(V2C\), and cloud-to-cloud \(C2C\) migrations for a variety of file systems and disk types.

-   Automatic collection of migration source information

    You do not need to manually configure system settings for migration sources. After running the relevant commands, the SMC client automatically collects the migration source information and imports it to the SMC console to prepare for subsequent migration operations.

-   Ease of use

    The SMC console allows you to easily configure migration tasks and migrate data to the cloud.

-   Support for batch migration

    You can select multiple migration tasks in the SMC console and perform a batch migration.

-   Central tracking of migration progress

    When migrating source servers to Alibaba Cloud in batches, you must track the migration status of each source server. The SMC console overview page displays the status of all your migration sources and tasks. It shows the overall migration progress and allows you to identify and troubleshoot problems that occur during migration.


## Migration process {#section_9ar_vcr_t2t .section}

SMC consists of a client and a console. Import the information of a source server to the console through the client. This step connects the source server with your Alibaba Cloud account. Then, create a migration task in the console for the source server and start the migration task to migrate the source server to Alibaba Cloud. For more information, see [Migration process](../../reseller.en-US/User Guide/Migration process.md#).

The following figure shows how to use SMC to migrate a source server.

![migrationFlow](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/475582/156652696050105_en-US.png)

