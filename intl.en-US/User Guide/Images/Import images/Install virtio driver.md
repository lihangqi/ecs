# Install virtio driver {#concept_dvq_cqs_xdb .concept}

This topic details which images do and do not require the virtio driver to be installed on the source server before import.

## Images requiring no manual installation {#section_lby_pqs_xdb .section}

After you [import custom images](reseller.en-US/User Guide/Images/Import images/Import custom images.md#), if the operating systems of your images are listed as follows, Alibaba Cloud automatically processes the virtio driver for you:

-   Windows Server 2008
-   Windows Server 2012
-   Windows Server 2016
-   CentOS 6/7
-   Ubuntu 12/14/16
-   Debian 7/8/9
-   SUSE 11/12

You can skip to recover the temporary root file system of initramfs or initrd.

## Images requiring manual installation {#section_nqx_yqs_xdb .section}

For Linux images that are not included in the preceding list, you must install the virtio driver on-premises before importing the images.

**To check the availability of virtio driver on a server**

1.  Run `grep -i virtio /boot/config-$(uname -r)` to inspect whether the  virtio driver is already built in the kernel of your server.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075784632_en-US.png)

    **Note:** 

    -   If VIRTIO\_BLK and VIRTIO\_NET do not exist in the output, the virtio driver  is not built in the kernel. You must install and configure the virtio driver on your server [to compile and install virtio driver](#).
    -   If the values of parameter CONFIG\_VIRTIO\_BLK and parameter CONFIG\_VIRTIO\_NET are y, the virtio driver is already built in the kernel. For more information, see [notes for importing images](reseller.en-US/User Guide/Images/Import images/Notes for importing images.md#) and [import custom images](reseller.en-US/User Guide/Images/Import images/Import custom images.md#).
    -   If the values of parameter CONFIG\_VIRTIO\_BLK and parameter CONFIG\_VIRTIO\_NET are m, continue to step 2.
2.  Run `lsinitrd /boot/initramfs-$(uname -r).img | grep virtio` to make sure the virtio driver has been complied in the temporary root file system of initramfs or initrd.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075784633_en-US.png)

    **Note:** 

    -   According to the preceding figure, the virtio\_blk driver, including its dependency virtio.ko, virtio\_pci.ko and  virtio\_ring.ko, has been compiled in the temporary root file system initramfs. For more information, see [notes for importing images](reseller.en-US/User Guide/Images/Import images/Notes for importing images.md#) and [import custom images](reseller.en-US/User Guide/Images/Import images/Import custom images.md#).
    -   If virtio driver is unavailable in the initramfs, you must recover the temporary root file system of initramfs or initrd before importing images or migration.

**To recover the temporary root file system**

If the virtio driver is supported by the kernel but not compiled in the temporary root file system,  you must recover the temporary root file system. The following example uses CentOS:

-   CentOS/RedHat 5

    ```
    mkinitrd -f --allow-missing \
                --with=xen-vbd  --preload=xen-vbd \
                --with=xen-platform-pci --preload=xen-platform-pci \
                --with=virtio_blk --preload=virtio_blk \
                --with=virtio_pci --preload=virtio_pci \
                --with=virtio_console --preload=virtio_console \
    ```

-   CentOS/RedHat 6/7

    ```
    mkinitrd -f --allow-missing \
                --with=xen-blkfront --preload=xen-blkfront \
                --with=virtio_blk --preload=virtio_blk \
                --with=virtio_pci --preload=virtio_pci \
                --with=virtio_console --preload=virtio_console \
                /boot/initramfs-$(uname -r).img $(uname -r)
    ```

-   Debian/Ubuntu

    ```
    echo -e 'xen-blkfront\nvirtio_blk\nvirtio_pci\nvirtio_console' >> \
    /etc/initramfs-tools/modules
    mkinitramfs -o /boot/initrd.img-$(uname -r)"
    ```


## To compile and install virtio driver {#compile .section}

The following example uses a Red Hat server:

**To download the kernel package**

1.  Run `yum install -y ncurses-devel gcc make wget` to install necessary components to compile the kernel.
2.  Run `uname -r` to query the kernel version of your server, such as 4.4.24-2.a17.x86\_64.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075784634_en-US.png)

3.  Visit [published Linux Kernel Archives](https://www.kernel.org/pub/linux/kernel/) to download the source codes of kernel, for example, the download link of kernel version starting with 4.4.24 is [https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.24.tar.gz](https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.24.tar.gz).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075794638_en-US.png)

4.  Run `cd /usr/src/` to change the directory.
5.  Run `wget https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.4.24.tar.gz` to download the installation package.
6.  Run `tar -xzf linux-4.4.24.tar.gz` to decompress the package.
7.  Run `ln -s linux-4.4.24 linux` to establish a link.
8.  Run `cd /usr/src/linux` to change the directory.

**To compile the kernel**

1.  Run the following commands to compile the driver into the kernel.

    ```
    make mrproper
     symvers_path=$(find /usr/src/ -name "Module.symvers")
     test -f $symvers_path && cp $symvers_path .
     cp /boot/config-$(uname -r) ./.config
     make menuconfig
    ```

2.  Configure the corresponding settings of virtio driver in the following windows:

    **Note:** Select \* to build the driver in the kernel, select m to compile it as a module.

    1.  Press the space bar to select Virtualization.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075794639_en-US.png)

        Make sure that you have selected  the option of KVM \(Kernel-based Virtual Machine\).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075794640_en-US.png)

        ```
        Processor type and features  --->
           [*] Paravirtualized guest support  --->
             --- Paravirtualized guest support
         (128)   Maximum allowed size of a domain in gigabytes
         [*]   KVM paravirtualized clock
         [*]   KVM Guest support
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9707/15433075794641_en-US.png)

        ```
        Device Drivers  --->
          [*] Block devices  --->
         <M>   Virtio block driver (EXPERIMENTAL)
         -*- Network device support  --->
             <M>   Virtio network driver (EXPERIMENTAL)
        ```

    2.  Press the Esc key to exit the kernel configuration windows, and save changes to file .config according to the dialog box.
    3.  Inspect whether all the corresponding settings of virtio driver has been correctly configured or not.
    4.  \(Optional\) If no configuration of virtio driver is settled after the inspect, run the following commands to edit the file .config manually.

        ```
        make oldconfig
        make prepare
        make scripts
        make
        make install
        ```

    5.  Run the following commands to check whether the virtio driver is installed.

        ```
        
        find /lib/modules/"$(uname -r)"/ -name "virtio.*" | grep -E "virtio.*"
        grep -E "virtio.*" < /lib/modules/"$(uname -r)"/modules.builtin
        ```

        **Note:** If any of the output includes virtio\_blk and virtio\_pci.virtio\_console, your server has correctly installed the virtio driver.


## What to do next {#section_e12_gws_xdb .section}

After compiling the virtio driver, you can [migrate your server to Alibaba Cloud by using the Cloud Migration Tool](../../../../reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

