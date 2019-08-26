# User data {#concept_fgf_tjn_xdb .concept}

You can use user data of an ECS instance to customize its startup behavior and to pass data into the instance. You can specify user data when creating an instance \([../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9856.md\#](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#)\) and customize startup behavior such as automatically update software packages, enable services, print logs, install dependencies, initialize web services, and more. User data of an ECS instance is implemented primarily through different types of scripts. User data can also be used as common data to be referenced in the instances.

## Instructions for use {#instructions .section}

To configure instance user data, note that:

-   Only VPC-Connected instances are supported.

-   For [phased-out instance types](https://partners-intl.aliyun.com/help/faq-detail/55263.htm), they must be I/O optimized. Other [instance type families](../../../../reseller.en-US/Instances/Instance type families.md#) are not limited for I/O optimized.

-   Instance user data requires Base64 encoding before being passed in, and the user data before encoding cannot exceed 16 KB.

-   The instance must use an official image or a user image that is created from an official image. The operating system must be one of the following:

    |Windows instances|Linux instances|
    |:----------------|:--------------|
    |Windows Server 2008 R2 and later version|     -   CentOS
    -   Ubuntu
    -   SUSE Linux Enterprise
    -   OpenSUSE
    -   Debian
    -   Aliyun Linux
 |


## Module frequency {#section_uf5_ryn_xdb .section}

After the instance enters the **Running** state, use your Alibaba Cloud primary account to run the user data of the instance, followed by the initialization or `/etc/init` information.

After you modify the instance user data, depending on the type of scripts and modules that are used, the modified user data is or is not run. For example:

-   If you configure user data by using a shell script, such as a [user-data script](#User-DataScript), the modified user data is not run.

-   If the user data configures modules such as Byobu, Set Hostname, and Set Passwords, the modified user data is not run.

-   If the user data configures modules such as bootcmd, update\_etc\_hosts, and yum\_add\_repo, the modified user data is run.

    For more information, see [modules](http://cloudinit.readthedocs.io/en/latest/topics/modules.html).


## Set user data {#SetUserDataExample .section}

For this example, assume that you write user data development in a Windows environment, and you use [Upstart Job](#UpstartJob) to configure the user data.

1.  Use an editor to create a text file, such as Notepad++.
2.  Edit the script related to the user data in the text file.

    **Note:** The first line must meet the format requirements of the instance user data script, such as \#! /bin/sh, \#cloud-config, \#upstart-job, \[bat\] and \[powershell\]. For more information , see [Linux instance user data](#linuxCustomScripts) and [Windows instance user data](#windowsCustomScripts).

3.  Debug the script file to confirm that the content is valid.
4.  \(Optional\) If you make a [Gzip compression content](#Gzip), compress the script file in .gz format.
5.  \(Optional\) If you are creating an [Include file](#Include) or a [Gzip compression script](#Gzip), upload script file to available storage services, obtain the link, and set the valid period of the link.

    We recommend that you use Alibaba Cloud OSS to create links. For more information, see [upload an object](../../../../reseller.en-US/Quick Start/Upload an object.md#) or [set lifecycle](../../../../reseller.en-US/Console User Guide/Manage buckets/Set lifecycle.md#).

6.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
7.  Follow the instructions in [creating an instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) to create a Linux instance.

    **Note:** The instance must be VPC-Connected, and you must select a [image](#Image) that meets the requirement. For [phased-out instance types](https://partners-intl.aliyun.com/help/faq-detail/55263.htm), I/O optimized instances are required. Other [instance type families](../../../../reseller.en-US/Instances/Instance type families.md#) are not limited in terms of I/O optimized.

    After creating the instance, select **Advanced \(based on instance RAM roles or cloud-init\) use text form** and enter your **user data**. If your user data has been encrypted by Base64 encoding, click **The text is Base64-encoded**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9660/15647248745484_en-US.png)

8.  Wait for the instance to be created.
9.  [Connect](reseller.en-US/Instances/Connect to instances/Overview.md#) to your instance.
10. View the results of the user data. If a failure occurs, check the relevant log files. The following is an output example of user data on a CentOS instance by using the upstart job script:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9660/15647248755485_en-US.png)

    In the preceding figure, the startup job file part-001.conf is generated in the /etc/init folder.


Related API: [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9856.md\#](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#)

## View user data {#linuxCustomData .section}

You can view user data of an instance from the server `100.100.100.200`. To do so, follow these steps:

1.  Connect to the target instance.
2.  In the instance, depending on your OS, run one of the following:
    -   For Linux, run `curl http://100.100.100.200/latest/user-data` to view the user data.
    -   For Windows, run `Invoke-RestMethod http://100.100.100.200/latest/user-data/` to view the user data.

Related API: [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9867.md\#](../../../../reseller.en-US/API Reference/Instances/DescribeUserData.md#)

## Modify user data {#linuxCustomData2 .section}

You must stop the instance before modifying its current user data. If you need to restart a Pay-As-You-Go VPC-Connected instance immediately after you modify the user data, we recommend that you disable the No fees for stopped instances option. To modify user data of an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Select the target instance and then, in the **Actions** column, click **Sets User Data**.
5.  Enter the user data and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9660/15647248755486_en-US.png)


**Note:** After you modify the user data, depending on the script type and the module type, the modified user data is or is not run.

Related API: [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9874.md\#](../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#)

## Linux instance user data {#linuxCustomScripts .section}

Linux instance user data can be configured by several types of script, such as [User-data Script](#User-DataScript), [Cloud Config](#CloudConfigData), [Include Files](#Include), [Gzip compression scripts](#Gzip), and [Upstart Job](#UpstartJob). The scripts follow the format of open source cloud-init, and reference the [Metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#) for data sources. The configuration of Linux instances are automated at boot. For more information, see [formats](http://cloudinit.readthedocs.io/en/latest/topics/format.html).

**User-data script** 

User-data can be a shell script. It runs once at the instance first boot. The first line is fixed as `#!`, for example `#! /bin/sh`. The content of user-data script before Base64 encoding cannot exceed 16 KB. The following is a User-Data script example:

``` {#codeblock_gl7_wre_4da}

#! /bin/sh
echo "Hello World. The time is now $(date -R)!" | tee /root/output10.txt
service httpd start
chkconfig httpd on
```

After the instance has been created, connect to the instance and run `cat [file]` to view the results of the user-data script.

``` {#codeblock_gzx_5jd_hn0}

[root@XXXXX2z ~]# cat output.txt
Hello World. The time is now Mon, 24 Jul 2017 13:03:19 +0800!
```

**Cloud-Config** 

You can use Cloud-Config to configure services such as updating yum sources, importing SSH keys, installing dependency packages, and more. The first line of Cloud-Config is fixed as `#cloud-config`, and the header cannot have spaces. The file must be valid yaml syntax. Depending on the service you configured, the instance user data runs differently.

Cloud Instance user data requires Base64 encoding before being passed in, and the pre-encoding cloud config data cannot exceed 16 KB. The following is a Cloud-Config script example:

``` {#codeblock_pzh_rik_fxx}

#cloud-config
apt:
primary:
- arches: [default]
uri: http://us.archive.ubuntu.com/ubuntu/
bootcmd:
- echo 192.168.1.130 us.archive.ubuntu.com >> /etc/hosts
```

After the instance has been created, connect to the instance to view the results.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9660/15647248755487_en-US.png)

**Include files** 

The contents of an Include File consist of a script link, with one link on one line. When the instance starts, cloud-init reads the contents of the script link in the Include File. If there is an error reading script content in a row, the instance stops performing user data. The first line of Include File is fixed as `#include` and the header cannot have spaces. The update frequency of the instance user data follows the script type configured in the include file.

Instance user data requires Base64 encoding before being passed in. The file before Base64 encoding cannot exceed 16 KB. The following is an Include File example:

``` {#codeblock_xib_pdj_7hn}

#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/UserData/myscript.sh
```

After the instance has been created, connect to the instance to view the results.

**Gzip compressed content** 

The content of a [User-Data Script](#User-DataScript), [Cloud-Config](#CloudConfigData), and [Include File](#Include) cannot exceed 16 KB. If your script content is larger than 16 KB, you can use Gzip to compress the content, the upload the compressed script to an available storage service \(we recommend OSS\), obtain the link, and use the Include File format to render the link. The first line of a Gzip compressed script is fixed as `#include` and the header cannot have spaces. The update frequency of the instance user data follows the script type configured in the Gzip file. The following is a Gzip compressed file example:

``` {#codeblock_4xu_fcy_tz6}

#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/config.gz
```

**Upstart Job** 

Upstart service is required for an init system if you use Upstart Job to configure user data. For example, CentOS 6, Ubuntu 10/12/14, and Debian 6/7 use upstart as the init system. Upstart Job script places your instance user data into a file in `/etc/init` directory. The first line of Upstart Job script is fixed as `#upstart-job` and the header cannot have spaces. We perform the instance user data for every instance boot. The following is a Upstart Job script example:

``` {#codeblock_ibd_ut6_kqb}

#upstart-job
description "upstart test"
start on runlevel [2345]
stop on runlevel [! 2345]
exec echo "Hello World. The time is now $(date -R)!" | tee /root/output.txt
```

## Windows instance user data {#windowsCustomScripts .section}

Windows instance user data is supported by Alibaba Cloud ECS, and offers Windows-based instances the ability to run initialization scripts. Instance user data requires Base64 encoding before being passed in, and the pre-encoding user data cannot exceed 16 KB . Only SBC case characters are allowed. You can write Bat script or PowerShell script to configure the instance user data.

**Bat scripts** 

The first line is fixed as `[bat]` and the header cannot have spaces. For example:

``` {#codeblock_uih_cjx_a4k}

[bat]
echo "bat test" > c:\1.txt
```

After the instance has been created, connect to the instance to view the results. In the following example, a 1.txt text file is shown under the C:\\ drive.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9660/15647248755488_en-US.png)

**The first line of PowerShell scripts** 

is fixed as `[powershell]` and the header cannot have spaces. For example:

``` {#codeblock_dt0_9xw_7he}

[powershell] 
write-output "Powershell Test" | Out-File C:\2.txt
```

## Reference {#Reference .section}

For more information about Linux instance user data, see cloud-init [formats](http://cloudinit.readthedocs.io/en/latest/topics/format.html).

For more information about the update frequency of Linux instance user data, see cloud-init [modules](http://cloudinit.readthedocs.io/en/latest/topics/modules.html).

