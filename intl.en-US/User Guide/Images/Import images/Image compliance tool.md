# Image compliance tool {#StandardImageFacilitator .concept}

This topic introduces how to use the image compliance tool to automatically locate the operating system settings of non-Alibaba Cloud specification through operation examples, parameter description, and output details. The tool is suitable for importing custom images scenarios.

## Introduction {#section_sjs_mc4_fgb .section}

ECS allows you to create instances from imported custom images. Imported custom images can be created based on your offline server, virtual machine, or a cloud host on any cloud platform. The images you import must meet certain requirements. For more information, see [Notes for importing images](reseller.en-US/User Guide/Images/Import images/Notes for importing images.md#).

To reduce the time required for creating images and instances, we recommend that you use the **image compliance tool** of ECS \(referenced in this document as **compliance tool**\) to create images that comply with the relevant standards. The compliance tool can detect non-compliance of various configuration indicators and locations based on a given server environment, generate TXT and JSON detection reports, and offer possible solutions.

## Limits {#section_o54_lr1_b2b .section}

The compliance tool currently supports Linux images only, such as Ubuntu, CentOS, Debian, RedHat, SUSE Linux Enterprise Server \(SLES\), OpenSUSE, FreeBSD, CoreOS, and other Linux versions.

## Sample {#section_n4v_kp1_b2b .section}

The following example use a CentOS 7.4 64-bit server.

1.  Log on to your server, virtual machine, or cloud host.
2.  [Download](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/84961/cn_zh/1534906727238/image_check) the compliance tool.
3.  Run `image_check` with root permissions to guarantee that the compliance tool can read configuration files under permission control.

    ```
    chmod +x image_check
    sudo image_check –p [destination path]
    ```

    **Note:** You can use `-p [destination path]` to specify the path where detection reports are generated. If you do not set this parameter, reports are generated in the compliance tool path by default.

4.  Wait for the compliance tool to detect the system configuration.

    ```
    Begin check your system...
     The report is generating.
     -----------------------------------------
     The information you need to enter when you import your image to the Alibaba Cloud website:
     Current system: CentOS # System information 1: Server operating system
     Architecture: x86_64 # System information 2: System architecture
     System disk size: 42 GB # System information 3: Server system disk capacity
     -----------------------------------------
     # Detection item
     Check driver [ OK ]
     Check shadow file authority [ OK ]
     Check security [ OK ]
     Check qemu-ga [ OK ]
     Check network [ OK ]
     Check ssh [ OK ]
     Check firewall [ OK ]
     Check filesystem [ OK ]
     Check device id [ OK ]
     Check root account [ OK ]
     Check password [ OK ]
     Check partition table [ OK ]
     Check lvm [ FAILED ]
     Check lib [ OK ]
     Check disk size [ OK ]
     Check disk use rate [ WARNING ]
     Check inode use rate [ OK ]
     -----------------------------------------
     15 items are OK
     1 items are failed
     1 items are warning
     -----------------------------------------
     The report is generated: /root/image_check_report_2018-05-14_18-18-10.txt
     Please read the report to check the details
    ```

5.  View the detection report. The report is generated in the format of `image_check_report_date_time.txt` or `image_check_report.json`.

## Detection items {#section_dpv_kp1_b2b .section}

The compliance tool detects the following server configuration items to ensure that the ECS instances created from your custom image are fully functional.

|Detection item|Non-compliance issue|Suggestion|
|:-------------|:-------------------|:---------|
|driver|The ECS instance cannot start normally.|Install a virtualization driver. For example, [install a virtio driver](reseller.en-US/User Guide/Images/Import images/Install virtio driver.md#)|
|/etc/shadow|You cannot modify the password file, so you cannot create an ECS instance from the custom image.|Do not use the `chattr` command to lock the /etc/shadow file.|
|SElinux|The ECS instance cannot start normally.|Do not modify /etc/selinux/config to start SELinux.|
|qemu-ga|Some of the services required by ECS are unavailable, and the instance is not fully functional.|Uninstall qemu-ga.|
|network|Network functions of the ECS instance are unstable.|Disable or delete the Network Manager and enable the network service.|
|ssh|You cannot [connect](reseller.en-US/User Guide/Connect to instances/Overview.md#) to the ECS instance from the console.|Enable the SSH service and do not set PermitRootLogin.|
|firewall|The system does not automatically configure your ECS instance environment.|Disable the firewall iptables, firewalld, IPFilter \(IPF\), IPFireWall \(IPFW\), or PacketFilter \(PF\).|
|file system|You cannot [resize the disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Overview.md#).|The XFS, Ext3, and Ext4 file systems are used, and the Ext2, UFS, and UDF file systems are allowed. The Ext4 file system does not support 64-bit features.|
|root|You cannot use your username and password to remotely connect to the ECS instance.|Reserve the root account.|
|passwd|You cannot add users to the ECS instance.|Retain or reinstall the passwd command.|
|Partition table|The ECS instance cannot start normally.|Use MBR partitioning.|
|Logical Volume Manager \(LVM\)|The ECS instance cannot start normally.|Switch to another partitioning service.|
|/lib|The ECS instance cannot be automatically configured.|The /lib and /lib64 files cannot be stored in absolute paths. Modify the storage paths of /lib and /lib64 to their relative paths.|
|system disk|N/A|Increase the system disk capacity. The optimal system disk capacity is 40 GiB to 500 GiB. When you import images, configure the system disk capacity based on the virtual file size of images, instead of the usage capacity of images.|
|disk\_usage|You cannot install the necessary drivers or services for the ECS instance.|Make sure that sufficient disk space is available.|
|inode usage|You cannot install the necessary drivers or services for the ECS instance.|Make sure that sufficient inode resources are available.|

The compliance tool provides a detection result `OK`, `FAILED`, or `WARNING` based on detection items.

-   `OK`: The detection items all comply with requirements.
-   `FAILED`: The detection items do not comply with requirements, which means a ECS instance created from the custom image cannot start normally. We recommend that you rectify the non-compliant items and recreate the image to improve instance startup efficiency.
-   `WARNING`: The detection items do not comply with requirements, which means an ECS instance created from the custom image can start normally, but ECS cannot use valid methods to configure your instance. You can choose to immediately rectify the non-compliant items or temporarily retain the items and create an image.

## Output items {#section_qpv_kp1_b2b .section}

The compliance tool provides detection reports in both TXT and JSON formats after it detects the system environment. You can use `-p [destination path]` to specify the path where detection reports are generated. If you do not specify this parameter, reports are generated in the compliance tool path by default.

-   Reports in TXT format are named `image_check_report_date_time.txt`. The reports include server configuration information and detection results. The following example uses a CentOS 7.4 64-bit server.

    ```
    The information you need to input when you import your image to Alibaba Cloud Website:
      Current system is: CentOS #Server operating system
      Architecture: x86_64 #System architecture
      System disk size: 42 GB #Server system disk capacity
      -----------------------------------------
       Check driver #Detection item name
       Pass: kvm drive is exist #Detection result
       Alibaba Cloud supports kvm virtualization technology
       We strongly recommend installing kvm driver.
    ```

-   Reports in JSON format are named `image_check_report.json`. The reports include server configuration information and detection results. The following example uses a CentOS 7.4 64-bit server.

    ```
    "platform": "CentOS", \\Server operating system
      "os_big_version": "7", \\Operating system version number (major)
      "os_small_version": "4", \\Operating system version number (minor)
      "architecture": "x86_64", \\System architecture
      "system_disk_size": "42", \\Server system disk capacity
      "version": "1.0.2", \\Compliance tool version
      "time": "2018-05-14_19-18-10", \\Detection time
      "check_items": [{
          "name": "driver", \\Detection item name
          "result": "OK", \\Detection result
          "error_code": "0", \\Error code
          "description": "Pass: kvm driver exists.", \\Description
          "comment": "Alibaba Cloud supports kvm virtualization technology. We strongly recommend installing kvm driver."
      }]
    }
    ```


## What to do next {#section_mb3_ct1_b2b .section}

1.  View the [notes for importing images](reseller.en-US/User Guide/Images/Import images/Notes for importing images.md#).
2.  [Install the virtio driver.](reseller.en-US/User Guide/Images/Import images/Install virtio driver.md#)
3.  \(Optional\) [Convert the image file format.](reseller.en-US/User Guide/Images/Import images/Convert image file format.md#)
4.  [Import custom images.](reseller.en-US/User Guide/Images/Import images/Import custom images.md#)
5.  [Create an instance from a custom image.](reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#)

