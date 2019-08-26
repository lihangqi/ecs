# Other migration solutions {#concept_lbp_wkk_yfb .concept}

If you are using an earlier server OS, or your server OS is not in the list of supported systems, you can contact Alibaba Cloud technical support for applicable cloud migration solutions.

## Migrate earlier server OSs to Alibaba Cloud {#section_u4f_xqq_yfb .section}

Some earlier server OSs, for example, OSs earlier than CentOS 5.5 and Red Hat 5.5, cannot be migrated to Alibaba Cloud directly because their kernels do not support the necessary virtualization drivers, such as virtio. The following procedure takes CentOS 5.1 \(old version, kernel version: 2.6.18-53.el5\) and CentOS 5.5 \(new version, kernel version: 2.6.18-194.el5\) as example OSs to describe how to upgrade the kernel version and migrate such systems to Alibaba Cloud.

**Procedure**

1.  Run the following command to confirm that the system version is CentOS 5.1 and the kernel version is 2.6.18-53.el5:

    ```
    cat /etc/redhat-release
    uname -r
    ```

2.  Run the following command to download and install the kernel installation package of CentOS 5.5:

    ```
    wget http://vault.centos.org/5.5/os/x86_64/CentOS/kernel-2.6.18-194.el5.x86_64.rpm
    rpm -ivh ./kernel-2.6.18-194.el5.x86_64.rpm
    ```

    **Note:** If an error occurs during the installation of the new kernel, you need to check the error log for details. If the error is caused by a conflict between the existing software and the new kernel, you need to manually uninstall the existing software and then reinstall the new kernel. After you install the new kernel successfully, you can reinstall the previous software.

3.  Upgrade the GRUB of your system to version 1.99. For more information, see [Update GRUB 1.99 for a Linux server](https://www.alibabacloud.com/help/faq-detail/62807.htm).

    **Note:** We recommend that you mask the old GRUB 0.97 program so that you do not mistake it for the new version.

4.  Run GRUB 1.99 as follows:
    1.  Run the `grub-mkconfig -o /boot/grub/grub.cfg` command to update the GRUB configuration file.
    2.  Run the `cat /boot/grub/grub.cfg` command to check whether the configuration file contains the old kernel 2.6.18-53.el5 and the new kernel 2.6.18-194.el5.
    3.  Run the `fdisk -l` command to find the system disk.
    4.  If your system disk is `/dev/sda`, run the `grub-install --no-floppy --modules=part_msdos --boot-directory=/boot /dev/sda` command.
    5.  Set the new kernel as a default startup item:
        1.  Run the `cat /boot/grub/grub.cfg |grep menuentry` command to check the startup item list of the kernel.
        2.  Find the label of the new kernel, and then run the following command to set the new kernel as a default startup item:

            ```
            mkdir /usr/local/etc/default/ -p
            echo "GRUB_DEFAULT=<label of the new kernel>" >> /usr/local/etc/default/grub
            grub-mkconfig -o /boot/grub/grub.cfg
            ```

            For example, if the new kernel is GNU/Linux \(with Linux 2.6.18-194.el5\) and the corresponding label is 2, run the following command:

            ```
            mkdir /usr/local/etc/default/ -p
            echo "GRUB_DEFAULT=2" >> /usr/local/etc/default/grub
            grub-mkconfig -o /boot/grub/grub.cfg
            ```

5.  Restart the OS. The GRUB menu page is displayed and the system is restarted using the new kernel 2.6.18-194.el5.
6.  [Download and install the Cloud Migration tool](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) to conduct the migration.

## Migrate other systems to Alibaba Cloud {#section_qr5_xqq_yfb .section}

If your system is not listed in [Supported systems and scopes of migration](intl.en-US/Migration service/Migration service/Supported systems and scopes of migration.md#), for example, Oracle Linux, Amazon Linux, and XenServer, [contact technical support](intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Feedback and support.md#) for custom system tests and migration solutions.

