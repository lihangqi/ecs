# Notes for importing images {#concept_d53_2jm_xdb .concept}

To guarantee a successful image import and usability of the image, the following considerations must be noted before you import an image:

## Windows images {#windows .section}

**Considerations**

-   Verify the integrity of the file system before you import images.
-   Do not modify critical system files.
-   Check that there is enough space on the system disk for the image to be installed.
-   Configure the system disk size for importing the image based on the virtual disk size rather than the used space of the image. The system disk size ranges from 40 GiB to 500 GiB.
-   Disable the firewall and allow access to RDP port 3389.
-   The logon password for the administrator account must be 8 to 30 characters in length and must contain three out of the four types of characterss, namely small and capital letters, numbers, and special characters. Specifically, special characters can be `( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /`.Additionally, the forward slash \(/\) cannot be the first character of the password.

**Not supported**

-   ISO images are not supported. However, you can create ISO images by using tools such as VirtualBox installed on-premises, and then convert the images to the RAW, VHD, or qcow2 format before importing them to Alibaba Cloud ECS.
-   qemu-ga cannot be installed in the image because it will impact the availability of services needed by ECS.
-   Images with the following operating systems cannot be imported: Windows XP, Windows 7 \(professional and enterprise editions\), Windows 8, and Windows 10.

**Supported**

-   Multi-partition system disks.
-   NTFS file systems and MBR partitions.
-   Images in RAW, qcow2, or VHD format. If the target image is not in any of the preceding formats, you need to [convert image file format](reseller.en-US/Images/Custom image/Import images/Convert image file format.md#) before importing it.
-   Images of the following operating systems can be imported:
    -   Windows Server 2016
    -   Windows Server 2012 R2
    -   Windows Server 2012
    -   Windows Server 2008 R2
    -   Windows Server 2008
    -   Windows Server 2003 with Service Pack 1 \(SP1\) or higher

## Linux images {#linux .section}

**Considerations**

-   Verify the integrity of the file system before you import images.
-   Do not modify critical system files, such as `/sbin`, `/bin`, and `/lib*`.
    -   Do not modify `/etc/issue*`. Otherwise, the system release cannot be identified by ECS, which means the system cannot be created.
    -   Do not modify `/boot/grub/menu.lst`. Otherwise, the ECS instance cannot be started.
    -   Do not modify `/etc/fstab`. Otherwise, the exception partition cannot be loaded, which means the ECS instance cannot be started.
    -   Do not modify `/etc/shadow` as **Read-Only**. Otherwise, the password file cannot be modified, which means the system cannot be created.
    -   Do not modify `/etc/selinux/config` to enable SELinux. Otherwise, the system cannot be started.
-   Check that there is enough space on the system disk for the image to be installed.
-   Disable the firewall and allow access to SSH port 22.
-   Enable Dynamic Host Configuration Protocol \(DHCP\).
-   Install the virtualization platform XEN or KVM drives. For more information, see [Install the virtio driver](reseller.en-US/Images/Custom image/Import images/Install virtio driver.md#).
-   We recommended that you [install cloud-init](reseller.en-US/Images/Custom image/Import images/Install cloud-init for Linux images.md#), so as to guarantee that hostname, NTP, and yum sources can be configured successfully.
-   The logon password for the root account must be 8 to 30 characters in length and must contain three out of the four types of characterss, namely small and capital letters, numbers, and special characters. Specifically, special characters can be `( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /`.

**Not supported**

-   ISO images are not supported. However, you can create ISO images by using tools such as VirtualBox installed on-premises, and then convert the images to the RAW, VHD, or qcow2 format before importing them to Alibaba Cloud ECS.
-   Multiple network interfaces.
-   IPv6 addresses.
-   System disk partitions cannot be adjusted. Currently, only a single root partition is supported.
-   qemu-ga cannot be installed in the image because it will impact the availability of services needed by ECS.

**Supported**

-   Images in RAW, qcow2, or VHD format. If the target image is not in any of the preceding formats, you need to [convert image file format](reseller.en-US/Images/Custom image/Import images/Convert image file format.md#) before importing it.
-   xfs, ext3, and ext4 file systems and MBR partitions.

    **Note:** The ext4 file system cannot contain the feature `64bit`, and the features `project` and `quota` cannot appear in pairs. To check the features, run the `tune2fs -l <ext4 file system disk directory\> | grep features` command to view a list of features contained in the ext4 file system.

-   Images of the following operating systems can be imported:
    -   Aliyun Linux
    -   CentOS 5/6/7
    -   CoreOS 681.2.0 and later
    -   Debian 6/7
    -   FreeBSD
    -   OpenSUSE 13.1
    -   RedHat
    -   RHEL \(Red Hat Enterprise Linux\)
    -   SUSE Linux 10/11/12
    -   Ubuntu 10/12/13/14/16/18

## Non-standard image usage notes \(Linux\) {#section_q1g_qcd_bhb .section}

Any Linux images that are not listed as public images provided by ECS are considered as non-standard platform images. Such images do not comply with ECS requirements for a standard operating system regarding critical system configuration files, basic system environments, and applications. If you want to use a non-standard platform image, perform the following actions as indicated by the image type:

-   Others Linux: Alibaba Cloud identifies all images of this type as other Linux systems. Alibaba Cloud does not handle any instances created if you import an image of Others Linux type. If you enable DHCP before you create an image, Alibaba Cloud automatically configures your network. After creating the instance, you need to connect to the instance by using the [Management Terminal](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#) feature in the console, and then manually configure the IP address, router, and password.
-   Customized Linux: Customized images. After importing a customized Linux image, configure the network and password of the instance according to the standard system configuration mode of Alibaba Cloud. For more information, see [customize Linux images](reseller.en-US/Images/Custom image/Import images/Customize Linux images.md#).

