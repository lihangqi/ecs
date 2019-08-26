# Migrate your server to Alibaba Cloud by using the Cloud Migration tool {#ServerMigrationOperation .concept}

This topic describes how to use the Cloud Migration tool to migrate your server to Alibaba Cloud ECS.

**Note:** In this topic, the source server refers to your on-premises server, VM, or cloud host. The steps described in this topic also apply to the migration of other types of servers. If you only want to migrate a database, see [Data migration](https://partners-intl.aliyun.com/help/doc-detail/26594.htm).

## Preparations {#section_alx_phh_dgb .section}

Before you use the Cloud Migration tool, ensure that you have made the following preparations:

**Account and permissions**

1.  Create an Alibaba Cloud account. If you want to migrate the source server to an Alibaba Cloud region in the Mainland China area, you need to complete real-name authentication.
2.  Ensure that your account balance has at least USD 100.

    **Note:** The Cloud Migration tool is provided free of charge. However, some [Pay-As-You-Go](../reseller.en-US/Pricing/Pay-As-You-Go.md#) resources are created during a migration, and the creation of these resources incurs a small fee charged to your account.

3.  If you want to use a RAM user account, you need to first use your Alibaba Cloud account to grant permissions to the RAM user so that the RAM user has permission to read and write ECS and VPC resources. We recommend that you grant permissions to the RAM account to use the AliyunECSFullAccess policy and AliyunVPCFullAccess policy. For more information, see [Permission granting in RAM](../../../../../reseller.en-US/User Guide/Permission management/Permission granting/Permission granting in RAM.md#).
4.  Activate the snapshot service in the ECS console.
5.  If you use a service provider account, ensure that you can call ECS APIs to order and purchase resources.

**Source server**

1.  Ensure that the local time of the source server is the same as the actual time. Otherwise, the error message IllegalTimestamp will occur during a migration.
2.  Ensure that the source server can access the following service addresses and ports:
    -   ECS: `https://ecs.aliyuncs.com:443`. For information about ECS service addresses in other regions, see [Endpoints](../reseller.en-US/API Reference/Getting started/Request structure.md#).
    -   VPC: `https://vpc.aliyuncs.com:443`.
    -   STS: `https://sts.aliyuncs.com:443`.
    -   ECS intermediate instance: port 8080 and port 8703 of Internet IP addresses. When you perform a [cloud migration through VPC intranet](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud migration through VPC intranet.md#), the source server accesses private IP addresses.
3.  If your source server runs a Linux operating system, ensure that:
    1.  The Rsync database is installed.

        -   CentOS: Run the `yum install rsync –y` command.
        -   Ubuntu: Run the `apt-get install rsync –y` command.
        -   Debian: Run the `apt-get install rsync –y` command.
        -   Other platforms: See their respective official websites for installation documentation.
        **Note:** By default, mainstream servers are installed with the Rsync database. No manual installation is required.

    2.  The SELinux feature of the source server is disabled. You can run the `setenforce 0` command to disable SELinux temporarily, or edit the /etc/selinux/config file to set the field `SELINUX=disabled` to disable SELinux permanently.

        **Note:** In most cases, SELinux is disabled only for CentOS and Red Hat.

    3.  The virtio \(KVM\) driver is installed. For more information, see [Install the virtio driver](../reseller.en-US/Images/Custom image/Import images/Install virtio driver.md#).

        **Note:** In most cases, mainstream servers are installed with the virtio \(KVM\) driver by default. No manual installation is required.

    4.  The latest version of Grand Unified Bootloader \(GRUB\) is installed. For earlier versions of operating systems \(such as CentOS 5, Red Hat 5, and Debian 7\), the GRUB version must be V1.9 or later. For more information, see [Update GRUB 1.99 for a Linux server](https://partners-intl.aliyun.com/help/doc-detail/62807.html). 

        **Note:** For some operating systems, such as Amazon Linux, the GRUB version must be V2.02 or later.


## Limits {#section_kwq_sxz_jfb .section}

To ensure that one or more server migrations are successful, we recommend that you pay attention to the following precautions:

-   Do not operate the intermediate instance. During a migration, a temporary intermediate instance named `INSTANCE_FOR_GOTOALIYUN` is created automatically under your Alibaba Cloud account. Do not stop, restart, or release the intermediate instance. After the migration, the intermediate instance is released automatically.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9833/155566776338950_en-US.png)

-   Incremental data migration is not allowed. We recommend that you pause such applications as databases and containers, or filter specified data directories before a migration and then synchronize these data directories after the migration.

-   By default, the following data directories are migrated:

    -   For Windows servers: By default, only data on the C drive \(including shared directories attached to the C drive\) is migrated as a partition of the system disk. If you want to migrate data on other partitions such as the D drive, see [Data disk parameter settings](#DataDiskSet).

    -   For Linux servers: By default, data on the subdirectories \(including shared directories\) under the root directory \(/\) is migrated as a partition of the system disk. If you want to migrate data on other directories such as /disk1, see [Data disk parameter settings](#DataDiskSet).


## Procedure {#section_egm_zx3_fgb .section}

The overall procedure for a server migration to Alibaba Cloud is as follows:

1.  [Download and install the Cloud Migration tool](#section_twq_sxz_jfb).
2.  [Configure the user\_config.json file](#section_p5x_xzz_jfb).
3.  [\(Optional\) Exclude files or directories from migration](#section_tzq_sxz_jfb).
4.  [Run the Cloud Migration tool](#section_uz1_md1_kfb).

## Step 1: Download and install the Cloud Migration tool {#section_twq_sxz_jfb .section}

Download the [Cloud Migration tool package](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip) and decompress it to the source server.

**Note:** The Cloud Migration tool is available for Windows and Linux in both the 32-bit and 64-bit versions. i386 refers to the 32-bit version and x86\_64 refers to the 64-bit version. You can select a version compatible with the source server.

![](images/34986_en-US.png "Version list")

|File or folder|Description|
|--------------|-----------|
|go2aliyun\_client.exe|The Windows CLI executable file.|
|go2aliyun\_gui.exe|The Windows GUI executable file. For more information, see [Windows GUI of Cloud Migration tool](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#).|
|go2aliyun\_client|The Linux CLI executable file.|
|user\_config.json|The configuration file of the migration source and migration destination.|
|Excludes folder|The folder in which to add directories to exclude from the migration.|
|client\_data|The migration data file, which includes such information as the intermediate instance and migration progress.|

## Step 2: Configure the user\_config.json file {#section_p5x_xzz_jfb .section}

Open and edit the user\_config.json file. For a description of the parameters, see [Server parameter description](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#ServerSet) and [Data disk parameter description](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#DataDiskSet). The initial content of the user\_config.json file is as follows:

```
{
    "access_id": "",
    "secret_key": "",
    "region_id": "",
    "image_name": "",
    "system_disk_size": 40,
    "platform": "",
    "architecture": "",
    "bandwidth_limit":0,
    "data_disks": []
}
```

**Note:** 

If you are using Windows GUI, you can configure the user\_config file on the GUI. For more information, see [Windows GUI of Cloud Migration tool](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#).

|Name|Type|Required?|Description|
|:---|:---|:--------|:----------|
|access\_id|String|Yes|Your AccessKeyID for accessing Alibaba Cloud APIs. For more information, see [Create an AccessKey](https://www.alibabacloud.com/help/doc-detail/53045.htm). **Note:** 

When you migrate your server, the Cloud Migration tool requires your AccessKeyID and AccessKeySecret. We recommend that you securely store these credentials and keep them strictly confidential.

 |
|secret\_key|String|Yes|Your AccessKeySecret for accessing Alibaba Cloud APIs. For more information, see [Create an AccessKey](https://www.alibabacloud.com/help/doc-detail/53045.htm).|
|region\_id|String|Yes|The ID of the Alibaba Cloud region to which your server is migrated, for example, cn-hangzhou \(China East 1 \(Hangzhou\)\). For more information, see [Region and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).|
|image\_name|String|Yes|Set a name for the image of the source server. The name must be unique in the Alibaba Cloud region. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|system\_disk\_size|Integer|No|Specify the system disk size. Unit: GiB. Value range: 40 to 500. **Note:** The value must be greater than the space occupied by the system disk on the source server. For example, if the system disk size is 500 GiB and the occupied space is 100 GiB, set this parameter to a value greater than 100 GiB.

 |
|platform|String|No|The operating system of the source server. Valid values: Windows Server 2003 | Windows Server 2008 | Windows Server 2012 | Windows Server 2016 | CentOS | Ubuntu | SUSE | OpenSUSE | Debian | RedHat | Others Linux **Note:** 

The value of the `platform` parameter is case-sensitive.

 |
|architecture|String|No|System architecture. Valid values: i386 | x86\_64|
|bandwidth\_limit|Integer|No|The maximum bandwidth of data transmission. Unit: KB/s. The default value is 0, which indicates that the bandwidth is not limited.

 |
|data\_disks|Array|No|A list of data disks. A maximum of 16 data disks are supported. For more information about specific parameters, see the following table. This parameter can be set to a value \(in GiB\) required to shrink disk volume. However, it cannot be less than the actual space used by the data disk.|

|Name|Type|Required?|Description|
|:---|:---|:--------|:----------|
|data\_disk\_index|Integer|No|The serial number of a data disk. Value range: 1 to 16. Default value: 1.

 |
|data\_disk\_size|Integer|No|The size of a data disk. Unit: GiB. Value range: 20 to 32768. **Note:** The value must be greater than the space occupied by the data disk on the source server. For example, if the source data disk size is 500 GiB and the occupied space is 100 GiB, set this parameter to a value greater than 100 GiB.

 |
|src\_path|String|Yes|The source directory of a data disk. Examples: -   In Windows, specify a drive letter, such as D:, E:, or F:.

-   In Linux, specify a directory, such as /mnt/disk1, /mnt/disk2, or /mnt/disk3.

**Note:** It cannot be the root directory or system directories, such as /bin, /boot, /dev, /etc, /lib, /lib64, /sbin, /usr, or /var.


 |

Four scenarios are provided as follows to describe how to edit the user\_config.json file. In each scenario, the migration destination of the target server is the Alibaba Cloud region of China East 1 \(Hangzhou\).

 **Scenario 1: Migrate a Windows server without data disk** 

-   The source server is configured as follows:
    -   Operating system: Windows Server 2008
    -   System architecture: 64-bit
    -   System disk size: 30 GiB
-   Migration destination:
    -   Image name: CLIENT\_IMAGE\_WIN08\_01
    -   System disk setting: 50 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_WIN08_01",
    "system_disk_size": 50,
    "platform": "Windows Server 2008",
    "architecture": "x86_64",
    "data_disks": [],
    "bandwidth_limit": 0
}
```

 **Scenario 2: Migrate a Windows server with data disk** 

In this scenario, two more data disks are attached to the Windows server that was used in Scenario 1. The drive letters and sizes of the data disks are as follows:

-   Partitions of the source data disk:
    -   D: 50 GiB
    -   E: 100 GiB
-   Partitions of the target data disk:
    -   D: 100 GiB
    -   E: 150 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_WIN08_01",
    "system_disk_size": 50,
    "platform": "Windows Server 2008",
    "architecture": "x86_64",
    "data_disks":  [ {
            "data_disk_index": 1,
            "data_disk_size": 100,
            "src_path": "D:"
        }, {
            "data_disk_index": 2,
            "data_disk_size": 150,
            "src_path": "E:"
        }
    ],
    "bandwidth_limit": 0
}
```

 **Scenario 3: Migrate a Linux server without data disk** 

-   The source server is configured as follows:
    -   Operating system: CentOS 7.2
    -   System architecture: 64-bit
    -   System disk size: 30 GiB
-   Migration destination:
    -   Image name: CLIENT\_IMAGE\_CENTOS72\_01
    -   System disk setting: 50 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_CENTOS72_01",
    "system_disk_size": 50,
    "platform": "CentOS",
    "architecture": "x86_64",
    "data_disks": [],
    "bandwidth_limit": 0
}
```

 **Scenario 4: Migrate a Linux server with data disks** 

In this scenario, two more data disks are attached to the Linux server that was used in Scenario 1. The drive letters and sizes of the data disks are as follows:

-   Partitions of the source data disk:
    -   /mnt/disk1: 50 GiB
    -   /mnt/disk2: 100 GiB
-   Partitions of the target data disk:
    -   /mnt/disk1: 100 GiB
    -   /mnt/disk2: 150 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_CENTOS72_01",
    "system_disk_size": 50,
    "platform": "CentOS",
    "architecture": "x86_64",
    "data_disks":  [ {
            "data_disk_index": 1,
            "data_disk_size": 100,
            "src_path": "/mnt/disk1"
        }, {
            "data_disk_index": 2,
            "data_disk_size": 150,
            "src_path": "/mnt/disk2"
        }
    ],
    "bandwidth_limit": 0
}
```

## Step 3: \(Optional\) Exclude files or directories from migration {#section_tzq_sxz_jfb .section}

The configuration files are located in the Excludes directory, including:

-   A system disk configuration file: rsync\_excludes\_win.txt or rsync\_excludes\_linux.txt

-   A data disk configuration file: named by adding the suffix disk\[disk index number\] to the system disk, for example, rsync\_excludes\_win\_disk1.txt or rsync\_excludes\_linux\_disk1.txt


**Note:** If the configuration file is lost or is accidentally deleted, you can create another one.

**Example 1: Exclude files or directories from migration of a Windows server**

-   **System disk**:

-   Specify the files or directories to be excluded:

    ```
    C:\MyDirs\Docs\Words
    C:\MyDirs\Docs\Excels\Report1.xlsx
    ```

-   Add the information to the rsync\_excludes\_win.txt file:

    ```
    /MyDirs/Docs/Words/
    /MyDirs/Docs/Excels/Report1.xlsx
    ```

-   **Data disk**:

-   Specify the files or directories to be excluded:

    ```
    D:\MyDirs2\Docs2\Words2
    D:\MyDirs2\Docs2\Excels\Report2.xlsxx
    ```

-   Add the following information to the rsync\_excludes\_win\_disk1.txt file:

    ```
    /MyDirs2/Docs2/Words2/
    /MyDirs2/Docs2/Excels2/Report2.xlsx
    ```

    **Note:** If you want to exclude a Windows directory, you need to remove the prefix of the directory \(scr\_path\). In the preceding example, you need to remove D:\\.


**Example 2: Exclude files or directories from migration of a Linux server**

-   **System disk \(root directory /\)**:

-   Specify the files or directories to be excluded:

    ```
    /var/mydirs/docs/words
    /var/mydirs/docs/excels/report1.shx
    ```

-   Add the following information to the rsync\_excludes\_linux.txt file:

    ```
    /var/mydirs/docs/words/
    /var/mydirs/docs/excels/report1.sh
    ```

-   **Data disk**:

-   Specify the files or directories to be excluded:

    ```
    /mnt/disk1/mydirs2/docs2/words2
    /mnt/disk1/mydirs2/docs2/excels2/report2.shx
    ```

-   Add the following information to the rsync\_excludes\_linux\_disk1.txt file:

    ```
    /mydirs2/docs2/words2/
    /mydirs2/docs2/excels2/report2.sh
    ```

    **Note:** If you want to exclude a Linux directory, you need to remove the prefix of the directory \(scr\_path\). In the preceding example, you need to remove /mnt/disk1.


## Step 4: Run the Cloud Migration tool {#section_uz1_md1_kfb .section}

**For Windows servers**

-   If you use the [Windows GUI](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#), in the directory where the Cloud Migration tool is located, run go2aliyun\_gui.exe.

-   If you use the Windows CLI, run go2aliyun\_client.exe.


**Note:** When you run the program, you need to confirm your administrator privileges by clicking **OK**.

**For Linux servers**

-   In the directory where the Cloud Migration tool is located, run the following command as the root user:

    ```
    chmod +x ./go2aliyun_client
    ./go2aliyun_client
    ```

-   For users with lower privileges, run the following command:

    ```
    sudo chmod +x ./go2aliyun_client
    sudo ./go2aliyun_client
    ```


**Note:** After you run the Cloud Migration tool, you do not need to perform any other operation.

After you run the Cloud Migration tool, it automatically obtains source server information \(the number of CPU cores, CPU usage, memory size, memory usage, disk size, and disk usage\) and prints the information on the terminal. Additionally, the migration status is also printed on the terminal as a log stream.

## What to do next {#section_qzt_t21_kfb .section}

When the `Goto Aliyun Finished!` message is displayed, it means that the migration is completed.

 ![](images/34987_en-US.png "Successful server migration")

You can then perform the following operations:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs), and then select the target region to view the generated custom image.
2.  [Use the custom image to create a Pay-As-You-Go ECS instance](../reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#) or [replace the system disk](../reseller.en-US/Block storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#) to check whether the custom image runs normally.

    **Note:** You can use a custom image without data disks to replace the system disk of the instance.

3.  Start the target instance. For more information, see [How can I check my system after migrating a Windows server?](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#AfterWindows) or [How can I check my system after migrating a Linux server?](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#AfterLinux)

## Troubleshooting {#section_g1r_sxz_jfb .section}

If the `Goto Aliyun Not Finished!` message is displayed, it means that the migration has failed.

 ![](images/34988_en-US.png "Failed server migration")

You then need to perform the following operations:

1.  Check the error message in the log file of the Logs folder in the same directory, and then follow the instructions in [Troubleshooting](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Troubleshooting.md#) and [Cloud Migration tool FAQ](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#) to fix the error.
2.  Run the Cloud Migration tool again.

    **Note:** If the intermediate instance is released, a new migration is required. For more information, see [What do I do if I released an intermediate instance by mistake?](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#Release) and [When do I need to clear the client\_data file?](../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#ClearClient_data)


