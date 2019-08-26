# Image compliance tool {#StandardImageFacilitator .concept}

This topic describes how to use the image compliance tool provided by Alibaba Cloud to check the validity of a custom Linux image and whether it meets the image import conditions.

## Background information {#section_sjs_mc4_fgb .section}

ECS allows you to create instances from custom images. However, the custom images must meet certain requirements before they can be used in Alibaba Cloud. For more information, see [Notes for importing images](intl.en-US/Images/Custom image/Import images/Notes for importing images.md#).

To reduce the time needed to create a custom image, we recommend that you use the image compliance tool of ECS. The image compliance tool is designed to automatically validate configuration items in a target Linux server environment to locate non-compliant items, generate TXT and JSON detection reports, and provide possible troubleshooting actions if required.

This topic uses a server running the CentOS 7.4 64-bit OS as an example.

## Scenarios {#section_o54_lr1_b2b .section}

The image compliance tool currently supports Linux images only, such as Ubuntu, CentOS, Debian, RedHat, SUSE Linux Enterprise Server \(SLES\), OpenSUSE, FreeBSD, CoreOS, and other Linux versions.

## Procedure {#section_n4v_kp1_b2b .section}

1.  Log on to your server, VM, or cloud host.
2.  Download the image compliance tool to the current directory of your server:

    ``` {#codeblock_mkg_w4k_qcf}
    wget http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/73848/cn_zh/1557459863884/image_check
    ```

    You can also [download the image compliance tool directly](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/73848/cn_zh/1557459863884/image_check).

3.  Run the image compliance tool with root privileges to ensure that the image compliance tool can read configuration files under permission control.

    ``` {#codeblock_ney_0qw_lru}
    chmod +x image_check
    sudo <path of the image compliance tool>/image_check –p [destination path] 
    ```

    In the preceding code example, <path of the image compliance tool\> is also the path where the detection report is generated. Therefore, run the following command to start the image compliance tool:

    ``` {#codeblock_f0y_pqx_vlf}
    sudo ./image_check
    ```

    **Note:** You can use the `-p [destination path]` command to specify the path where the detection report is generated. If this parameter is not specified, the detection report will be generated in the path of the image compliance tool by default.

4.  Wait for the image compliance tool to check the system configuration.

    ``` {#codeblock_jdb_330_6my}
    Begin check your system......
    The report is generating.
    ---------------------------------------
    The information you need to input when you import your image to Alibaba Cloud website:
    Current system: CentOS
    Architecture: x86_64
    System disk size: 42 GB
    ---------------------------------------
    Check driver                                               [  OK  ]
    Check shadow file authority                                [  OK  ]
    Check security                                             [  OK  ]
    Check qemu-ga                                              [  OK  ]
    Check network                                              [  OK  ]
    Check ssh                                                  [  OK  ]
    Check firewall                                             [  OK  ]
    Check filesystem                                           [  OK  ]
    Check device id                                            [  OK  ]
    Check root account                                         [  OK  ]
    Check password                                             [  OK  ]
    Check partition table                                      [  OK  ]
    Check lib                                                  [  OK  ]
    Check disk size                                            [  OK  ]
    Check disk use rate                                        [  OK  ]
    Check inode use rate                                       [  OK  ]
    ---------------------------------------
    16 items are OK.
    0 items are failed.
    0 items are warning.
    ---------------------------------------
    The report is generated: /root/image_check_report_2019-05-10_13-28-21.txt
    Please read the report to check the details.
    ```

5.  View the detection report.

    The path of the detection report is displayed in the tool execution result. In this example, the path is /root. The report is named in the format of `image_check_report_date_time.txt` or `image_check_report.json`.


## Detection items {#section_dpv_kp1_b2b .section}

The compliance tool detects the following server configuration items to ensure that the ECS instances created from your custom image are fully functional.

|Detection item|Non-compliance issue|Suggestion|
|:-------------|:-------------------|:---------|
|driver|The ECS instance cannot start normally.|Install a virtualization driver. For more information, see [EN-US\_TP\_9707.md\#](intl.en-US/Images/Custom image/Import images/Install virtio driver.md#).|
|/etc/shadow|You cannot modify the password file. As a result, you cannot create an ECS instance from the custom image.|Do not use the `chattr` command to lock the /etc/shadow file.|
|SElinux|The ECS instance cannot start normally.|Do not start SELinux by modifying /etc/selinux/config.|
|qemu-ga|Some of the services required by ECS are unavailable, and the instance is not fully functional.|Uninstall qemu-ga.|
|network|Network functions of the ECS instance are unstable.|Disable or delete the Network Manager and enable the network service.|
|ssh|You cannot [connect](intl.en-US/Instances/Connect to instances/Overview.md#) to the ECS instance from the console.|Enable the SSH service and do not set PermitRootLogin.|
|firewall|The system does not automatically configure your ECS instance environment.|Disable the firewall iptables, firewalld, IPFilter \(IPF\), IPFireWall \(IPFW\), or PacketFilter \(PF\).|
|file system|You cannot [resize the disk](intl.en-US/Block Storage/Block storage/Resize cloud disks/Disk resizing overview.md#).| -   The XFS, Ext3, and Ext4 file systems are recommended.
-   The Ext2, UFS, and UDF file systems are allowed.
-   Do not use the `64 bit` feature for the Ext4 file system.

 **Note:** The `64 bit` feature is one feature of the Ext4 file system. You can use the man ext4 command to view detailed descriptions.

 |
|root|You cannot use your username and password to remotely connect to the ECS instance.|Reserve the root account.|
|passwd|You cannot add users to the ECS instance.|Retain or reinstall the passwd command.|
|Partition table|The ECS instance cannot start normally.|Use MBR partitioning.|
|/lib|The ECS instance cannot be automatically configured.|The /lib and /lib64 files cannot be stored in absolute paths. Modify the storage paths of the files to their relative paths.|
|system disk|N/A|Increase the system disk capacity. The optimal system disk capacity is 40 GiB to 500 GiB. When you import images, configure the system disk capacity based on the virtual file size of images, instead of the usage capacity of images.|
|disk\_usage|You cannot install the necessary drivers or services for the ECS instance.|Make sure that sufficient disk space is allocated.|
|inode usage|You cannot install the necessary drivers or services for the ECS instance.|Make sure that sufficient inode resources are allocated.|

The image compliance tool provides a detection result `OK`, `FAILED`, or `WARNING` based on detection items.

-   `OK`: The detection items all comply with requirements.
-   `FAILED`: The detection items do not comply with requirements, which means an ECS instance created from the custom image cannot start normally. We recommend that you rectify the non-compliant items and recreate the image to improve instance startup efficiency.
-   `WARNING`: The detection items do not comply with requirements, which means an ECS instance created from the custom image can start normally, but ECS cannot use valid methods to configure your instance. You can choose to immediately rectify the non-compliant items or temporarily retain the items and create an image.

## Output items {#section_qpv_kp1_b2b .section}

The image compliance tool generates detection reports in both TXT and JSON formats in the destination path after it detects the system environment.

**Note:** You can use the `-p [destination path]` command to specify the path where the detection report is generated. If this parameter is not specified, the detection report will be generated in the path of the compliance tool by default.

-   Reports in TXT format are named `image_check_report_date_time.txt`. The reports include server configuration information and detection results. The following example uses a server running the CentOS 7.4 64-bit OS.

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

-   Reports in JSON format are named `image_check_report.json`. The reports include server configuration information and detection results. The following example uses a server running the CentOS 7.4 64-bit OS.

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

1.  View the [notes for importing images](notes for importing imagesEN-US_TP_9702.dita#concept_d53_2jm_xdb).
2.  [EN-US\_TP\_9707.md\#](intl.en-US/Images/Custom image/Import images/Install virtio driver.md#).
3.  \(Optional\) [Convert the image file format.](intl.en-US/Images/Custom image/Import images/Convert image file format.md#)
4.  [EN-US\_TP\_9706.md\#](intl.en-US/Images/Custom image/Import images/Import custom images.md#).
5.  [../../../../dita-oss-bucket/SP\_2/DNECS19100341/EN-US\_TP\_9627.md\#](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

