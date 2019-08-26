# 历史Linux镜像的问题修复方案 {#concept_228687 .concept}

历史Linux镜像创建的ECS云服务器，可能存在NTP、YUM没有配置，还可能存在最近暴漏较高的安全漏洞。请按照本文中介绍的操作步骤进行修复，可以让您的云服务器更加安全，可以使用免费的阿里云提供的NTP进行时间同步，还可以使用阿里云提供的YUM服务进行安装软件。

## 1. 配置NTP {#section_lwx_qi2_fqc .section}

不区分发行版，先备份/etc/ntp.conf，然后将其内容替换为如下：

``` {#codeblock_0h0_wan_f53}
# ntp.conf
#
# ntpd config for aliyun ecs.
#
# 6LAN+6LAN+3WAN
#               shijun.cao@alibaba-inc.com
#               2014.8.11
#
driftfile  /var/lib/ntp/drift
pidfile   /var/run/ntpd.pid
logfile /var/log/ntp.log
# Access Control Support
restrict    default ignore
restrict -6 default ignore
restrict 127.0.0.1
restrict 192.168.0.0 mask 255.255.0.0 nomodify notrap nopeer noquery
restrict 172.16.0.0 mask 255.240.0.0 nomodify notrap nopeer noquery
restrict 100.64.0.0 mask 255.192.0.0 nomodify notrap nopeer noquery
restrict 10.0.0.0 mask 255.0.0.0 nomodify notrap nopeer noquery
restrict ntp1.aliyun.com nomodify notrap nopeer noquery
restrict ntp2.aliyun.com nomodify notrap nopeer noquery
restrict ntp3.aliyun.com nomodify notrap nopeer noquery
restrict ntp4.aliyun.com nomodify notrap nopeer noquery
restrict ntp5.aliyun.com nomodify notrap nopeer noquery
restrict ntp6.aliyun.com nomodify notrap nopeer noquery
# local clock
server 127.127.1.0
fudge  127.127.1.0 stratum 10
#public ntp server
server ntp1.aliyun.com iburst minpoll 4 maxpoll 10
server ntp2.aliyun.com iburst minpoll 4 maxpoll 10
server ntp3.aliyun.com iburst minpoll 4 maxpoll 10
server ntp4.aliyun.com iburst minpoll 4 maxpoll 10
server ntp5.aliyun.com iburst minpoll 4 maxpoll 10
server ntp6.aliyun.com iburst minpoll 4 maxpoll 10
#Private ntp server
server ntp1.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp2.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp3.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp4.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp5.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp6.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
#New private ntp server
server ntp7.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp8.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp9.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp10.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp11.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
server ntp12.cloud.aliyuncs.com iburst minpoll 4 maxpoll 10
```

## 2. 更新软件源 {#section_ecs_jri_6e8 .section}

1.  先确认镜像当前的 Linux 系统发行版和版本号。
    -   如果有lsb\_release命令，执行`lsb_release -a`。
    -   否则，执行`cat /etc/issue`。
2.  对于CentOS，备份/etc/yum.repos.d/下的CentOS-Base.repo和epel.repo文件。根据CentOS版本，执行如下相应的命令:

    -   CentOS 5：

        ``` {#codeblock_mkk_4ro_0g5}
        wget -qO /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
        wget -qO /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-5.repo
        ```

    -   CentOS 6：

        ``` {#codeblock_shw_ceh_z0i}
        wget -qO /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
        wget -qO /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
        ```

    -   CentOS 7：

        ``` {#codeblock_m5h_qmp_e9w}
        wget -qO /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
        wget -qO /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
        ```

    repo文件下载完成后，执行`yum makecache`命令。

3.  对于Aliyun 5.7，备份/etc/yum.repos.d/CentOS-Base.repo后，执行以下命令：

    ``` {#codeblock_8nv_10x_t62}
    wget -qO /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/aliyun-5.repo
    ```

    repo文件下载完成后，执行`yum makecache`。

4.  对于Ubuntu，备份/etc/apt/sources.list文件。然后根据发行版版本，执行相应的命令：

    -   Ubuntu 12.04：

        ``` {#codeblock_lfa_8e1_k4k}
        wget -qO  /etc/apt/sources.list http://mirrors.aliyun.com/repo/ubuntu1204-lts.list
        ```

    -   Ubuntu 14.04：

        ``` {#codeblock_hds_yn4_j0j}
        wget -qO  /etc/apt/sources.list http://mirrors.aliyun.com/repo/ubuntu1404-lts.list
        ```

    然后，执行`apt-get update`。

5.  对于Debian，备份/etc/apt/sources.list文件。然后根据发行版版本，执行相应的命令：

    -   Debian 6：

        ``` {#codeblock_vnu_iab_swc}
        wget -qO /etc/apt/sources.list http://mirrors.aliyun.com/repo/debian6-lts.list
        ```

    -   Debian 7：

        ``` {#codeblock_rmc_gka_3mk}
        wget -qO /etc/apt/sources.list http://mirrors.aliyun.com/repo/debian7-lts.list
        ```

    然后，执行`apt-get update`。


## 3. 安全漏洞修复补丁 {#section_52y_p32_9q9 .section}

主要修复目前已知的重大安全漏洞，需要升级的软件包括： bash 、glibc 、 openssl 、wget 、ntp 。

在执行如下命令之前，需要确保系统当前的软件源已经设置正确。

-   对于CentOS和Aliyun Linux，执行`yum update bash glibc openssl wget ntp`。
-   对于Ubuntu和Debian，执行`apt-get install bash libc6 libc-bin openssl wget ntp`。

