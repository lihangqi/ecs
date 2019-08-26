# Aliyun Linux 17.01 特性说明 {#concept_53091_zh .concept}

Aliyun Linux镜像是公共镜像的一种，是阿里云针对 ECS 实例提供的定制化原生操作系统。本文介绍Aliyun Linux镜像 17.01（Golden Toad）版本的特性。

-   集成阿里云内核组维护的 4.4 系列 Kernel
    -   支持 swap 内存压缩可保证显著减少 I/O；
    -   支持动态补丁机制 kpatch，升级内核无需重启系统；
    -   支持超大内存 kdump（至多 3 TB）；
    -   支持 Automatic NUMA；
    -   用户态 vsyscall 获取时间戳性能提升；
    -   全面支持 Docker 技术栈；
    -   支持 pv panic，方便协助云用户快速定位内核问题；
    -   重新设计的无锁 TCP listener，提升 2 ~ 3 个数量级防 SYN 攻击能力。
-   高效创建和启动
    -   基于虚拟化级优化栈创建实例，有效降低创建虚拟机所需时间。
    -   OS 搭载阿里云定制启动服务，提升启动速率，使创建到可登录时间控制在 30 秒内。
-   文件系统

    新增支持文件系统：XFS、Btrfs、AUFS 和 OverlayFS。

-   全新工具链

    GCC 4.8.x glibc 2.17 GDB 7.6.1。

-   安全提升
    -   OpenSSH 支持 chroot shell 登录，限制用户登录在一个受限的根文件系统中。
    -   OpenSSH 可指定多个验证条件以加强登录访问。
-   兼容CentOS 7.2

