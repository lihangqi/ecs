# Migrate to Alibaba Cloud by using Cloud Migration tool {#ServerMigrationOperation .concept}

This topic describes how to migrate your physical machines, VMs, or cloud hosts to Alibaba Cloud ECS. In this topic, we use on-premise server or server to represent the source of migration to make it easy to read. Thus, the migration steps also applies to your physical machines, VMs, or cloud hosts.

**Note:** For on-premises databases to cloud migration, see [Data migration](https://partners-intl.aliyun.com/help/doc-detail/26594.htm).

## Precautions {#section_kwq_sxz_jfb .section}

To use Cloud Migration tool, consider the following:

-   The system time of the on-premises server is synchronized with the real time. Otherwise, an error indicating abnormal TimeStamp is recorded in the migration log file.

-   The on-premises server must be able to reach the following network address and communication port to access the related Alibaba Cloud services, uninterruptedly:

-   The nearest ECS endpoint: `https://ecs.aliyuncs.com:443`. For other regional endpoints, see API Reference [Request structure](../reseller.en-US/API Reference/Getting started/Request structure.md#).

-   Virtual Private Cloud \(VPC\): `http://vpc.aliyuncs.com:443`.

-   Security Token \(STS\): `https://sts.aliyuncs.com:443`.

-   The intermediate instance: `https://xxx.xx.xxx.xx:8080` and `https://xxx.xx.xxx.xx:8703`. The `xxx.xx.xxx.xx` indicates the Internet IP address of the intermediate instance.

-   Incremental data migration is not allowed. We recommend that applications such as databases and container services are paused, or related directories are filtered before migration to Alibaba Cloud. Synchronize any data related to those applications after the migration has been completed.

-   During migration, an ECS instance named INSTANCE\_FOR\_GOTOALIYUN is created by default under your Alibaba Cloud account. It acts as an intermediate station. To avoid migration failure, do not stop, restart, or release the intermediate ECS instance. The intermediate ECS instance is automatically released once the migration completes.

-   If the AccessKey that you create belongs to a RAM user, you must make sure that the specified RAM user is granted with `AliyunECSFullAccess` and `AliyunVPCFullAccess` role to operate the Alibaba Cloud resources. For more information, see *RAM* document [Authorization policies](../../../../../../reseller.en-US//Authorization management/Policy management.md#).

-   If shared memory is used in your on-premises server:

    -   **Default action**:
        -   For Windows servers: By default, Cloud Migration tool recognizes and uploads the data on a shared memory that is attached to the C drive as one part of the system disk.

        -   For Linux servers: By default, Cloud Migration tool recognizes and uploads the data on a shared memory as one part of the system disk.

    -   **Custom action**:
        -   You can set the mount point directory of the shared memory as a data disk, and migrate it as an independent data disk.

        -   Alternatively, you can filter out the directory of the shared memory from migration and the data on the shared memory will not be migrated.


## For on-premises servers running Linux OS {#section_pwq_sxz_jfb .section}

When your on-premise server runs a Linux operation system, additional requirements is required:

-   The Rsync library must have been pre-installed.

    -   CentOS: Run `yum install rsync –y`.

    -   Ubuntu: Run `apt-get install rsync –y`.

    -   Debian: Run `apt-get install rsync –y`.

    -   Other releases: See the installation documents of the releases on their official website.

-   SELinux must be deactivated. You can temporarily deactivate SELinux by running `setenforce 0`. However, we recommend that you disable the SELinux for better experience by specifying the `SELINUX=disabled` in the /etc/selinux/config file.

-   The Kernel-based Virtual Machine \(KVM\) driver is installed. For more information about how to install a KVM driver, see [Install virtio driver](reseller.en-US/User Guide/Images/Import images/Install virtio driver.md#).

-   For server such as CentOS 5, Red Hat 5, or Debian that has a too old kernel, and the version of GRUB \(GRand Unified Bootloader\) is earlier than 1.9. You may [update the boot loader GRUB to a version later than 1.9](https://partners-intl.aliyun.com/help/doc-detail/62807.html).


## Prerequisite {#section_jvk_ghd_nfb .section}

You must have signed up for ECS snapshot service in the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).

## Step 1: Download and install the Cloud Migration tool {#section_twq_sxz_jfb .section}

1.  Download the [Cloud Migration tool package](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip)accordingly. The lists of the decompressed files are as follows:

    |File or file folder|Description|
    |-------------------|-----------|
    |Excludes folder|Filters out the directories from the migration. An rsync\_excludes\_win.txt file is included by default.|
    |client\_data|Maintains the record of transmission data during a migration. Transmission data includes the attributes of the intermediate instance for cloud migration, the process information of data disk migration, the generated custom image name, the region you plan to migrate to and so on.|
    |user\_config.json|The configuration file of your on-premise server|
    |go2aliyun\_gui.exe|A GUI wizard for Windows OS. For more information, see [Windows GUI of Cloud Migration tool](reseller.en-US/User Guide/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#).|
    |go2aliyun\_client.exe|Main program of Cloud Migration tool.|

    |File or file folder|Description|
    |-------------------|-----------|
    |Check|An image compliance detection tool. It contains a client\_check program by default.|
    |client\_data|Maintains the record of transmission data during a migration. Transmission data includes the attributes of the intermediate instance for cloud migration, the process information of data disk migration, the generated custom image name, the region you plan to migrate to and so on.|
    |user\_config.json|The configuration file of the on-premise server.|
    |Excludes folder|Filters out the directories from the migration. An rsync\_excludes\_win.txt file is included by default.|
    |go2aliyun\_client|The main program of Cloud Migration tool.|

2.  Log on to the on-premise server, virtual machine, or cloud host to be migrated.

3.  Decompress the Cloud Migration tool package to the specified directory.


## Step 2: Edit the user\_config.json file {#section_p5x_xzz_jfb .section}

The user\_config.json configuration file is edited in JSON. It contains necessary configuration information when you migrate the target on-premises server, including your AccessKey and target custom image name. You are required to manually configure a few parameters.

**Note:** 

If you are using the Windows GUI version, you can complete the user\_config on the GUI interface. For more information, see [Windows GUI of Cloud Migration tool](reseller.en-US/User Guide/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#).

1.  Open the user\_config.json file in the decompressed Cloud Migration tool. The following is the initial file:

    ```
    {
        "access_id": "",
        "secret_key": "",
        "region_id": "region",
        "image_name": "",
        "system_disk_size": 40,
        "platform": "",
        "architecture": "",
        "bandwidth_limit":0,
        "data_disks": []
    }
    ```

2.  Edit the file according to the parameters described in the following tables.

    |Name|Type|Required|Description|
    |:---|:---|:-------|:----------|
    |access\_id|String|Yes|Your AccessKeyID for accessing Alibaba Cloud API. For more information, see [Create AccessKey](https://partners-intl.aliyun.com/help/doc-detail/53045.htm).**Note:** 

Migrating servers by using Cloud Migration tool requires your AccessKeyID and AccessKeySecret, which are important credentials, and you must keep them confidential and secured.

|
    |secret\_key|String|Yes|Your AccessKeySecret for accessing Alibaba Cloud API. For more information, see [Create AccessKey](https://partners-intl.aliyun.com/help/doc-detail/53045.htm).|
    |region\_id|String|Yes|Alibaba Cloud Region ID to which your server is migrated, for example, `cn-hangzhou` \(China East 1\). For details about values, see [Region and Zones](https://partners-intl.aliyun.com/help/doc-detail/40654.htm).|
    |image\_name|String|Yes|Set a name for your server image, which must be different from all existing image names in the same Alibaba Cloud region. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
    |system\_disk\_size|Integer|No|Specify the system disk size in the unit of GiB. Value range: \[20, 500\].**Note:** The value must be greater than the occupied space of the system disk on the on-premise server. For example, if the maximum system disk capacity is 500 GiB while the occupied space is 100 GiB, set this value to be greater than 100 GiB.

|
    |platform|String|No|Operating system of the on-premise server. Optional values: Windows Server 2003 | Windows Server 2008 | Windows Server 2012 | Windows Server 2016 | CentOS | Ubuntu | SUSE | OpenSUSE | Debian | RedHat | Others Linux**Note:** 

The value of `platform` parameter is case-sensitive.

|
    |Architecture|String|No|Processor architecture. Optional values: i386 | x86\_64|
    |bandwidth\_limit|Integer|No|The maximum bandwidth of data transmission, in the units of measurement KB/s.The default value is 0, and 0 indicates no limit for the bandwidth.

|
    |data\_disks|Array|No|List of data disks. A maximum of 16 data disks are supported. List of data disks in your on-premises server, in the units of measurement GiB. For more information about specific parameters, see the table Parameters for data disk configuration. A maximum of 16 data disks are supported. This parameter can be set to the expected value to shrink disk, however, it cannot be less than the actual space used by the data disk.|

    |Name|Type|Required|Description|
    |:---|:---|:-------|:----------|
    |data\_disk\_index|Integer|No|Data disk serial number. Value range: \[1, 16\].Default value: 1.

|
    |data\_disk\_size|Integer|No|Data disk size. In the units of measurement GiB. Value range: \[20, 32768\].**Note:** The value must be greater than the actual used space of the data disk on the on-premises server. For example, if the source data disk capacity is 500 GiB while the actually occupied space is 100 GiB, set this value to be greater than 100 GiB.

|
    |src\_path|String|Yes|The directory of a source data disk. Examples:    -   In Windows, specify a drive letter, such as D:, E:, or F:.

    -   In Linux, specify a path, such as /mnt/disk1, mnt/disk2, or /mnt/disk3.

**Note:** It cannot be the /root directory or system directories, such as /bin, /boot, /dev, /etc, /lib, /lib64, /sbin, /usr or /var.

|

3.  Proofread the file and make sure that the configuration complies with the JSON syntax. For more information about JSON syntax, see [RFC 7159](https://tools.ietf.org/html/rfc7159).


Here are four scenarios that describe how to customize user\_config.json based on the initial configuration file.

**Scenario 1. Migrate a Windows server without data disk**

-   Assuming that the configuration of your on-premise server is as follows:
    -   Operating system: Windows Server 2008
    -   Used space of system disk: 30 GiB
    -   System architecture: 64-bit
-   Migration destination:
    -   Target migration region: Alibaba Cloud China East 1 region \(`cn-hangzhou`\)
    -   Image name: P2V\_CLIENT\_IMAGE\_WIN08\_01
    -   Expected size of system disk: 50 GiB

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

**Scenario 2. Migrate a Windows server with data disks**

Assuming that the three data disks are attached to the Windows server in Scenario 1. The drive letter and sizes of the data disks are as follows:

-   D: 100 GiB
-   E: 150 GiB
-   F: 200 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_WIN08_01",
    "system_disk_size": 50,
    "platform": "Windows Server 2008",
    "architecture": "x86_64",
    "data_disks": [ {
            "data_disk_index": 1,
            "data_disk_size": 100,
            "src_path": "D:"
        }, {
            "data_disk_index": 2,
            "data_disk_size": 150,
            "src_path": "E:"
        }, {
            "data_disk_index": 3,
            "data_disk_size": 200,
            "src_path": "F:"
        }
    ],
    "bandwidth_limit": 0
}
```

**Scenario 3. Migrate a Linux server without data disk**

-   Assuming that the configuration of your on-premise server is as follows:
    -   Version: CentOS 7.2
    -   Used space of system disk: 30 GiB
    -   System architecture: 64-bit
-   Migration destination:
    -   Target migration region: Alibaba Cloud China East 1 region \(`cn-hangzhou`\)
    -   Image name: CLIENT\_IMAGE\_CENTOS72\_01
    -   Size of system disk: 50 GiB

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

**Scenario 4. Migrate a Linux server with data disks**

Assuming that the three data disks are attached to the Linux server in Scenario 3. The source path and sizes of the data disks are as follows:

-   /mnt/disk1: 100 GiB
-   /mnt/disk2: 150 GiB
-   /mnt/disk3: 200 GiB

```
{
    "access_id": "YourAccessKeyID",
    "secret_key": "YourAccessKeySecret",
    "region_id": "cn-hangzhou",
    "image_name": "CLIENT_IMAGE_CENTOS72_01",
    "system_disk_size": 50,
    "platform": "CentOS",
    "architecture": "x86_64",
    "data_disks": [ {
            "data_disk_index": 1,
            "data_disk_size": 100,
            "src_path": "/mnt/disk1"
        }, {
            "data_disk_index": 2,
            "data_disk_size": 150,
            "src_path": "/mnt/disk2"
        }, {
            "data_disk_index": 3,
            "data_disk_size": 200,
            "src_path": "/mnt/disk3"
        }
    ],
    "bandwidth_limit": 0
}
```

## Step 3: Filter out directories from migration {#section_tzq_sxz_jfb .section}

Cloud Migration tool can filter out files or directories that are not migrated to Alibaba Cloud. You can configure [rsync](https://download.samba.org/pub/rsync/rsync.html) to filter out files and directories from migrating to Alibaba Cloud.

**Note:** Cloud migration is a time-consuming task, and we recommend that you filter out the unnecessary directories and data disks. At the same time, the used storage space of cloud disks after the migration is reduced.

**How to filter files for Windows server**

Default filtered files \(folders\) include pagefile.sys, $RECYCLE.BIN, and System Volume Information.

-   System disk: Write down the file paths in rsync\_excludes\_win.txt.

-   Data disk: Create and open new TXT files with specific file names. Write down the file paths to be filtered in the TXT files and save to Excludes directory. The following are examples of TXT file names:

    -   rsync\_excludes\_win\_disk1.txt
    -   rsync\_excludes\_win\_disk2.txt
    -   rsync\_excludes\_win\_disk3.txt

        ……


**Windows server example**

-   Assuming that you want to filter out the folder `C:\MyDirs\Docs\Words` and file `C:\MyDirs\Docs\Excels\Report1.xlsx` on a Windows server. You can write the configuration in the file rsync\_excludes\_win.txt as follows:

    ```
    /Mydirs/docs/words/
    /MyDirs/Docs/Excels/Report1.xlsx
    ```

-   Assuming that you want to filter out the folder `D:\MyDirs\Docs\Words` and file `D:\MyDirs\Docs\Excels\Report1.xlsx` on a Windows server. You can write the configuration in the file rsync\_excludes\_win\_disk1.txt as follows:

    ```
    /Mydirs/docs/words/
    /MyDirs/Docs/Excels/Report1.xlsx
    ```


**How to filter files for Linux server**

Default filtered files or directories include /dev/\*, /sys/\*, /proc/\*, /media/\*, lost+found/\*, /mnt/\*, and /var/lib/lxcfs/\*.

**Note:** The /var/lib/lxcfs/\\\* directory is only applicable to some versions. For example, when you do not have the access permission on the cache directory for Linux containers of Ubuntu, /var/lib/lxcfs/\\\* must be filtered out before migration.

-   System disk: Write down the file paths in rsync\_excludes\_linux.txt.

-   Data disk: Create and open new TXT files with specific file names. Write down the file paths to be filtered in the TXT files and save to Excludes directory. The following are examples of TXT file names:

    -   rsync\_excludes\_linux\_disk1.txt
    -   rsync\_excludes\_linux\_disk2.txt
    -   rsync\_excludes\_linux\_disk3.txt

        ……


**Linux server example**

-   Assuming that you want to filter out the root folder `/var/mydirs/docs/words` and file `/var/mydirs/docs/excels/report1.sh` on a Linux server. You can write the configuration in the file rsync\_excludes\_Linux.txt as follows:

    ```
    /var/mydirs/docs/words/
    /var/mydirs/docs/excels/report1.sh
    ```

-   Assuming that you want to filter out the folder `/mnt/disk1/mydirs/docs/words` and file `/mnt/disk1/mydirs/docs/excels/report1.sh` on a data disk for Linux server. You can write the configuration in the file rsync\_excludes\_linux\_disk1.txt as follows:

    ```
    /mydirs/docs/words/
    /mydirs/docs/excels/report1.sh
    ```

    **Note:** To filter out files and paths in data disk for Linux server, remove the data disk src\_path prefix path, for example, remove /mnt/disk1 from the preceding example.


## Step 4: \(Optional\) Edit the client\_data file {#section_jk5_tv1_kfb .section}

**Warning:** Only when you can directly access a VPC in an Alibaba Cloud region from your Integrated Data Center \(IDC\), virtual machines, or cloud hosts, you are recommended to edit the client\_data file. Otherwise, the modification may affect cloud migration and running processes.

The client\_data file maintains the record of transmission data during migration. For more information about how to edit the client\_data file, see [Cloud migration through VPC intranet](reseller.en-US/User Guide/Cloud Migration tool for P2V and V2V/Cloud migration through VPC intranet.md#).

After each successful migration, information about the intermediate ECS instance in the ECS is automatically recorded in the client\_data configuration file. For the next migration, you must clear the current client\_data file or use the default client\_data file to override the current file.

## Step 5: Run the Cloud Migration tool {#section_uz1_md1_kfb .section}

Windows server: Right-click go2aliyun\_client.exe and select **Run as administrator**. If you are using the Windows GUI version, see [Windows GUI of Cloud Migration tool](reseller.en-US/User Guide/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#).

Linux server: Run Cloud Migration tool as a root user.

1.  Run `chmod +x go2aliyun_client`.

2.  Run `./go2aliyun_client`.


## Results {#section_qzt_t21_kfb .section}

If `Goto Aliyun Finished!` is displayed, go to the image page in the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to check the results. After migration, the resource of your on-premises server, such as the operating system, applications, and application data, are convert to a custom image, which is displayed in the image page of the ECS console.

If `Goto Aliyun Not Finished!` is displayed, check the log files in the logs folder for [troubleshooting](reseller.en-US/User Guide/Cloud Migration tool for P2V and V2V/Troubleshooting.md#). After the problem is rectified, run go2aliyun\_client again, and it continues to proceed from where it was suspended during the preceding execution.

**Note:** 

-   The Cloud Migration tool reads data that is recorded in the client\_data upon the beginning of each migration attempt, whether the previous task is interrupted or complete. For the next migration, you must clear the current client\_data file or use the initial client\_data file to override the current file.
-   After the client\_data file is initialized, the task progress information is lost and the on-going migration is set to the beginning. In cases where cloud migration fails, such as when the intermediate instance, VPC, VSwitch, or other security groups do not exist, you can try clearing the client\_data operation to resolve the issue.

## What to do next {#section_g1r_sxz_jfb .section}

You can [create a Pay-As-You-Go instance by using the custom image](reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#) or [change the system disk by using the custom image](reseller.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#) to test whether the custom image works or not.

After you migrate an on-premises Linux server, the data disks are not mounted by default. You may run `ls /dev/vd*` in the instances to mount the data disks manually as needed, and edit configuration file `/etc/fstab` to configure the mounting file systems. For more information, see [Linux\_Format and mount a data disk](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).

