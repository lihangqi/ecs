# Aliyun Linux 2 {#concept_rgv_rvd_2hb .concept}

Aliyun Linux 2是阿里云研发的新一代Aliyun Linux操作系统，旨在为ECS实例上的应用程序提供更加安全、稳定、高性能的运行环境。您可以免费使用Aliyun Linux 2公共镜像创建实例。

## 适用范围 {#section_pqg_rzh_fhb .section}

-   各种云场景工作负载。例如，您可以在Aliyun Linux 2上运行数据库、数据分析、Web应用程序，以及生产环境中的其他工作负载。
-   [各规格族实例](../../../../intl.zh-CN/实例/实例规格族.md#)，包括弹性裸金属服务器。支持的实例规格vCPU为1 vCPU~160 vCPU，内存大小为0.5 GiB~3840 GiB。

    **说明：** Aliyun Linux 2不支持使用经典网络的实例和非I/O优化实例。


## 优势 {#section_ecp_myh_fhb .section}

与其他Linux系统相比，Aliyun Linux 2具有以下优势：

-   专门为阿里云云服务器ECS定制，系统启动更快并且运行时性能更好。
-   通过更新的Linux内核、用户态软件及工具包提供更丰富的操作系统特性。
-   精简内核，减少潜在安全隐患。
-   既可免费使用，又可获得由阿里云提供的技术支持。

## 特性 {#section_ckq_fzh_fhb .section}

**新版云内核**

Aliyun Linux 2默认搭载并启用最新版本阿里云云内核。新版云内核提供了以下特性：

-   基于内核社区长期支持的4.19.24版本定制而成，增加适用于云场景的新特性、改进内核性能并修复重大缺陷。
-   提供针对ECS实例环境定制优化的内核启动参数和系统配置参数。
-   提供操作系统崩溃后的内核转储（Kdump）能力，您可根据需要在线打开或者关闭该功能，无需重启操作系统。
-   提供内核热补丁升级（Live Patch）能力。

**软件包**

Aliyun Linux 2默认搭载[阿里云命令行工具](https://www.alibabacloud.com/help/product/29991.htm)。

软件包更新如下：

-   网络服务从`network.service`切换为`systemd-networkd`。
-   用户态软件包与CentOS 7.6.1810版本兼容，该版本用户态软件包可直接在Aliyun Linux 2使用。
-   软件包安全漏洞（CVE）修复在Aliyun Linux 2版本支持期限内会持续更新，详情请参见[镜像发布记录](intl.zh-CN/镜像/公共镜像/镜像发布记录.md#)。

**性能优化**

Aliyun Linux 2优化了开机启动速度并提升了运行时的系统性能，包括：

-   针对ECS实例环境大幅优化启动速度。
-   针对ECS实例环境优化多线程场景，提升大规格实例多线程性能。
-   针对MySQL数据库场景进行全链路优化，与[ESSD云盘](https://www.alibabacloud.com/help/faq-detail/64950.htm)配合使用，显著提升性能。

## 获取Aliyun Linux 2 {#section_u2k_nyh_fhb .section}

阿里云官方在ECS控制台提供了Aliyun Linux 2公共镜像，您可通过下列方法获取并使用Aliyun Linux 2：

-   创建ECS实例时选择**公共镜像**，并选择Aliyun Linux 2的相应版本，详情请参见[使用向导创建实例](../../../../intl.zh-CN/实例/创建实例/使用向导创建实例.md#)。
-   已创建的ECS实例可通过更换系统盘，将现有操作系统更换为Aliyun Linux 2。在更换系统盘页面，选择**公共镜像**并选择Aliyun Linux 2的相应版本，详情请参见[更换系统盘（公共镜像）](../../../../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（公共镜像）.md#)。

## 使用Aliyun Linux 2 {#section_n2q_pb3_fhb .section}

**更新的系统参数**

Aliyun Linux 2在配置文件/etc/sysctl.d/50-aliyun.conf中更新了下列内核配置参数：

-   `kernel.hung_task_timeout_secs = 240`：延长内核hung\_task超时秒数，避免频繁的hung\_task提示。
-   `kernel.panic_on_oops = 1`：允许内核发生Oops错误时抛出Kernel Panic异常，如果配置了Kdump则可自动捕获崩溃详情。
-   `kernel.watchdog_thresh = 50`：延长hrtimer、NMI、Soft Lockup以及Hard Lockup等事件的阈值，避免可能出现的内核误报。
-   `kernel.hardlockup_panic = 1`：允许内核发生Hard Lockup错误时抛出Kernel Panic异常，如果配置了Kdump则可自动捕获崩溃详情。

使用`sysctl`命令，可查看或修改Aliyun Linux 2运行时的系统参数。

**更新的内核参数**

Aliyun Linux 2更新了下列内核参数：

-   `crashkernel=0M-2G:0M,2G-8G:192M,8G-:256M`：为内核转储（Kdump）功能预留的内存空间。
-   `cryptomgr.notests`：关闭crypto在内核启动时的自检行为，加快启动速度。
-   `cgroup.memory=nokmem`：关闭Memory Cgroup的内核内存统计功能，避免出现潜在的内核不稳定问题。
-   `rcupdate.rcu_cpu_stall_timeout=300`：延长RCU CPU Stall Detector的超时阈值为300秒，避免内核误报。

运行`cat /proc/cmdline`命令，可查看Aliyun Linux 2运行时的内核参数。

**内核版本**

Aliyun Linux 2默认搭载4.19.24版本云内核（当前版本号为kernel-4.19.24-9.al7）。

您可以根据需要，安装并切换至兼容CentOS 7.6.1810版本的3.10系列内核，运行以下命令可回退至3.10内核版本。

**说明：** 更换内核版本可能导致无法开机等风险，请谨慎操作。

```
sudo yum install -y kernel-3.10.0
sudo grub2-set-default "$(grep ^menuentry /boot/grub2/grub.cfg | grep 3.10.0 | awk -F\' '{ print $2 }')"
sudo grub2-mkconfig -o /boot/grub2/grub.cfg

#重启系统
sudo reboot
```

**内核转储（Kdump）功能**

Aliyun Linux 2提供了Kdump服务。开启该服务后可捕获内核错误，方便您对内核崩溃现象进行分析。

您可以使用下列命令开启或彻底关闭Kdump服务：

-   运行以下命令可开启Kdump服务。

    ```
    sudo systemctl enable kdump.service
    sudo systemctl restart kdump.service
    ```

    **说明：** 所选[实例规格](../../../../intl.zh-CN/实例/实例规格族.md#)的内存小于或等于2GiB时，无法使用Kdump服务。

-   运行以下命令可将Kdump服务预留的内存地址空间归还给操作系统，并彻底关闭Kdump服务。

    ```
    sudo sh -c 'echo 0 > /sys/kernel/kexec_crash_size'
    sudo systemctl disable kdump.service
    sudo systemctl stop kdump.service
    ```

    **说明：** Kdump服务预留的内存地址空间归还给操作系统后，必须重启操作系统才可再次开启Kdump服务。


**配置网络**

Aliyun Linux 2默认使用`systemd-networkd`配置网络。配置网络时，需注意以下两点：

-   DHCP或静态IP的配置文件位于/etc/systemd/network/目录。
-   重启网络的命令为`sudo systemctl restart systemd-networkd`。

**获取Debuginfo包和源码包**

-   运行以下命令获取Debuginfo包。

    ```
    sudo yum install -y yum-utils
    sudo debuginfo-install -y <packageName>
    ```

-   运行以下命令获取源码包。

    ```
    sudo yum install -y alinux-release-source
    sudo yum install -y yum-utils
    sudo yumdownloader --source <sourcePackageName>
    ```


**试验性支持的软件包**

试验性支持的软件包是指由阿里云官方提供，但未经严格测试、不保证质量的软件包。Aliyun Linux 2提供了下列两种类型的试验性软件包：

-   普通试验性软件包
    -   `Python 3.6`
    -   `Golang 1.11`和`Golang 1.12`
-   SCL插件方式支持的试验性软件包
    -   `GCC 7.3.1`
    -   `GDB 8.0.1`
    -   `Binutils 2.28`
    -   `Make 4.2.1`

安装软件包操作步骤：

-   普通试验性软件包
    1.  运行以下命令打开YUM仓库支持。

        ```
        sudo yum install -y alinux-release-experimentals
        ```

    2.  运行以下命令安装软件包。

        ```
        sudo yum install -y <软件包名称>
        ```

-   SCL插件方式支持的试验性软件包
    1.  运行以下命令安装`scl-utils`。

        ```
        sudo yum install -y scl-utils
        ```

    2.  运行以下命令打开YUM仓库支持。

        ```
        sudo yum install -y alinux-release-experimentals
        ```

    3.  从YUM源安装您需要的软件包。以下命令同时安装了GCC、GDB、Binutils和Make工具。

        ```
        sudo yum install -y devtoolset-7-gcc devtoolset-7-gdb devtoolset-7-binutils devtoolset-7-make
        ```

        安装成功后，您即可使用高版本的GCC以及相关工具。示例代码如下：

        ```
        # 查看现有的SCL，需要指定库名。本示例代码中，库名为devtoolset-7。
        scl -l devtoolset-7
        # 运行相关的SCL软件
        scl enable devtoolset-7 'gcc --version'
        ```


## 技术支持 {#section_enr_5zh_fhb .section}

阿里云官方为Aliyun Linux 2提供如下技术支持：

-   版本支持期限为3年，到2022年3月31日结束版本生命周期。
-   在YUM源提供安全更新（Security Updates），运行`yum update`命令可更新至新版本。

