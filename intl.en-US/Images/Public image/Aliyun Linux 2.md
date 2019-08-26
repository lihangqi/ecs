# Aliyun Linux 2 {#concept_rgv_rvd_2hb .concept}

Aliyun Linux 2 is a next-generation Aliyun Linux operating system developed by Alibaba Cloud. It is intended to provide a safer, more stable, and high-performance running environment for applications on ECS instances. You can create an instance by using the Aliyun Linux 2 public image for free.

## Scope of application {#section_b4m_8xg_r4b .section}

-   Various workloads on cloud. For example, you can run databases, data analytics, Web applications, and other workloads in a production environment on Aliyun Linux 2.
-   [Various instance type families](../../../../reseller.en-US/Instances/Instance type families.md#), including ECS Bare Metal Instances. The supported instance specifications are as follows:

    -   vCPU: 1 vCPU - 160 vCPU
    -   Memory: 0.5 GiB - 3,840 GiB
    **Note:** Aliyun Linux 2 does not support instances that use the Xen virtual infrastructure or instances that use the classic network.


## Advantages {#section_1bw_jbc_wi3 .section}

Compared with other Linux systems, Aliyun Linux 2 has the following advantages:

-   Tailor-made for Alibaba Cloud ECS instances, featuring faster system startup and better runtime performance.
-   Provides richer operating system features through the updated Linux kernel, user-mode software, and toolkits.
-   Streamlined kernel and reduced potential security risks.
-   Free to use \(technical support is available\).

## Features {#section_k9x_1ke_ylp .section}

**New version of the Alibaba Cloud kernel**

Aliyun Linux 2 is equipped with the latest version of the Alibaba Cloud kernel, which provides the following features:

-   Customized based on version 4.19.24 that has been supported by the kernel community by adding new features for cloud scenarios, improving performance, and fixing major bugs.
-   Customized and optimized kernel startup parameters and system configuration parameters intended for the ECS instance environment.
-   Kernel crash dumping \(Kdump\). You can enable or disable it without rebooting the operating system.
-   Kernel Live Patching \(KLP\).

**Software package**

Aliyun Linux 2 is equipped with the Alibaba Cloud command line tool by default. The package updates are as follows:

-   `network.service` is changed to `systemd-networkd`.
-   The user mode package is compatible with CentOS 7.6.1810. That is, the user mode package of CentOS 7.6.1810 can be used on Aliyun Linux 2 directly.
-   Fixes for Common Vulnerabilities and Exposures \(CVEs\) are continuously updated until the end of life \(EOL\) of Aliyun Linux 2 is reached. For information about the release notes of Aliyun Linux 2, see [Release notes](reseller.en-US/Images/Public image/Release notes.md#).

**Performance optimization**

Aliyun Linux 2 increases the boot speed and improves system performance at runtime, including:

-   Greatly optimized startup speed for ECS instance environments.
-   Optimized multi-threaded scenarios for ECS instance environments and improved multi-threaded performance for large-scale instances.
-   Significantly improved performance thanks to full link optimization for MySQL database scenarios \(combined with ESSD cloud disks\).

## Get Aliyun Linux 2 {#section_0tz_709_gj4 .section}

Aliyun Linux 2 is officially available in the ECS console of Alibaba Cloud. You can use Aliyun Linux 2 in the following ways:

-   Select **Public Image** and then **Aliyun Linux 2** when creating an ECS instance. For more information, see [Create an instance by using the wizard](../../../../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).
-   Update the operating system of an existing ECS instance to Aliyun Linux 2 by replacing its system disk. For more information, see [Replace the system disk by using a public image](../../../../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (public image).md#).

## Use Aliyun Linux 2 {#section_pwb_nz0_sxd .section}

**Updated system parameters**

Aliyun Linux 2 updated the following kernel configuration parameters in the configuration file /etc/sysctl.d/50-aliyun.conf:

-   `kernel.hung_task_timeout_secs = 240`: Increases the kernel hung\_task timeout seconds to avoid frequent hung\_task prompts.
-   `kernel.panic_on_oops = 1`: Throws the Kernel Panic exception when the kernel is experiencing an Oops error. Moreover, crash details are automatically captured if Kdump is configured.
-   `kernel.watchdog_thresh = 50`: Increases the thresholds for events such as hrtimer, NMI, Soft Lockup, and Hard Lockup to avoid possible kernel false positives.
-   `kernel.hardlockup_panic = 1`: Throws the Kernel Panic exception when the kernel is experiencing a Hard Lockup error. Moreover, crash details are automatically captured if Kdump is configured.

You can use the `sysctl` command to view or modify the system parameters of Aliyun Linux 2 at runtime.

**Updated kernel parameters**

Aliyun Linux 2 updated the following kernel parameters:

-   `crashkernel=0M-2G:0M,2G-8G:192M,8G-:256M`: Reserves the memory space for the Kdump function.
-   `cryptomgr.notests`: Turns off the self-check of crypto during kernel startup to speed up the startup.
-   `cgroup.memory=nokmem`: Turns off the kernel memory statistics function of Memory Cgroup to avoid potential kernel instability.
-   `rcupdate.rcu_cpu_stall_timeout=300`: Increases the timeout threshold of RCU CPU Stall Detector to 300 seconds to avoid kernel false positives.

Run the `cat /proc/cmdline` command to view the kernel startup parameters of Aliyun Linux 2 at runtime.

**Kernel version**

Aliyun Linux 2 is equipped with the 4.19.24 version of Alibaba Cloud kernel by default \(the current version is kernel-4.19.24-9.al7\).

You can install and switch to a v3.10 series kernel compatible with CentOS 7.6.1810 as needed, and run the following command to roll back to a v3.10 kernel:

**Note:** Replacing the kernel version may result in boot failure. Exercise caution when you perform this operation.

``` {#codeblock_2xb_4gh_xnj}
sudo yum install -y kernel-3.10.0
sudo grub2-set-default "$(grep ^menuentry /boot/grub2/grub.cfg | grep 3.10.0 | awk -F\' '{ print $2 }')"
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
# Restart the system
sudo reboot
```

**Kdump**

Aliyun Linux 2 provides the Kdump service. Kernel errors can be captured after the service is turned on, allowing you to analyze kernel crashes.

You can turn on/off the Kdump service by using the following command:

-   Run the following command to turn on the Kdump service:

    ``` {#codeblock_oi0_8ya_7cy}
    sudo systemctl enable kdump.service
    sudo systemctl restart kdump.service
    ```

    **Note:** If the memory of the selected [instance type](../../../../reseller.en-US/Instances/Instance type families.md#) is less than or equal to 2 GiB, the Kdump service cannot be used.

-   Run the following command to return the memory address space reserved by the Kdump service to the operating system and turn off the Kdump service:

    ``` {#codeblock_00i_u8p_ous}
    sudo sh -c 'echo 0 > /sys/kernel/kexec_crash_size'
    sudo systemctl disable kdump.service
    sudo systemctl stop kdump.service
    ```

    **Note:** After the memory address space reserved by the Kdump service is returned to the operating system, the operating system must be restarted in order to enable the Kdump service again.


**Configure the network**

Aliyun Linux 2 uses `systemd-networkd` to configure the network by default. When you configure the network, note the following:

-   The configuration file for DHCP or static IP addresses is located in the /etc/systemd/network/ directory.
-   The command to restart the network is `sudo systemctl restart systemd-networkd`.

**Get the Debuginfo package and the source code package**

-   Run the following command to get the Debuginfo package:

    ``` {#codeblock_vnd_gfo_aw7}
    sudo yum install -y yum-utils
    sudo debuginfo-install -y <packageName>
    ```

-   Run the following command to get the source package:

    ``` {#codeblock_c9v_54j_5jd}
    sudo yum install -y alinux-release-source
    sudo yum install -y yum-utils
    sudo yumdownloader --source <sourcePackageName>
    ```


**Experimental software packages**

Experimental software packages are provided by Alibaba Cloud, but not rigorously tested. Therefore, their quality is not guaranteed. Aliyun Linux 2 provides the following types of experimental packages:

-   Ordinary experimental software packages
    -   `Python 3.6`
    -   `Golang 1.11` and `Golang 1.12`
-   Experimental software packages that support SCL plugins
    -   `GCC 7.3.1`
    -   `GDB 8.0.1`
    -   `Binutils 2.28`
    -   `Make 4.2.1`

Install a package:

-   Ordinary experimental software packages
    1.  Run the following command to enable YUM store:

        ``` {#codeblock_3ts_c7c_1c3}
        sudo yum install -y alinux-release-experimentals
        ```

    2.  Run the following command to install a package:

        ``` {#codeblock_f53_buu_o6h}
        sudo yum install -y <package name>
        ```

-   Experimental software packages that support SCL plugins
    1.  Run the following command to install `scl-utils`:

        ``` {#codeblock_926_h03_hi1}
        sudo yum install -y scl-utils
        ```

    2.  Run the following command to enable YUM store:

        ``` {#codeblock_fry_uvb_y67}
        sudo yum install -y alinux-release-experimentals
        ```

    3.  Install the packages you need from the YUM source. The following command installs GCC, GDB, Binutils, and Make tools.

        ``` {#codeblock_ds6_1qw_0zp}
        sudo yum install -y devtoolset-7-gcc devtoolset-7-gdb devtoolset-7-binutils devtoolset-7-make
        ```

        After the installation is complete, you can use the newer version of GCC and related tools. The sample code is as follows:

        ``` {#codeblock_91k_gbc_o8m}
        # To view an existing SCL, you need to specify the library name:
        scl -l devtoolset-7
        # Run the related SCL software:
        scl enable devtoolset-7 'gcc --version'
        ```


## Technical support {#section_6bz_416_i2g .section}

Alibaba Cloud provides the following technical support for Aliyun Linux 2:

-   The version support period is 3 years, and the version life cycle is ended by March 31, 2022.
-   Security updates in the YUM source. You can run the `yum update` command to update to the latest version.

