# 自动配置IPv6 {#concept_sq5_gvp_yfb .concept}

IPv6地址不仅可以手工配置，还能够自动配置。您可以使用ecs-util-ipv6工具来自动配置IPv6。

## 工具介绍 {#section_bdz_tvp_yfb .section}

-   工具名称：ecs-util-ipv6
-   程序类型：Linux bash shell、Windows exe
-   版本号：1.0.0
-   功能作用：为已绑定IPv6地址的ECS实例一键配置静态IPv6，或者为没有绑定IPv6的ECS实例一键清理静态IPv6配置。

## 注意事项 {#section_rqf_bwp_yfb .section}

-   该工具仅适用于VPC网络实例，依赖实例元数据服务，使用前请勿将网络禁用或者将相关出口IP端口（100.100.100.200:80）禁用。详情请参见 [实例元数据](cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)。

-   该工具运行时会自动重启网卡、网络服务，短时间内网络可能会不可用，请慎重执行。


## 使用说明 {#section_bjl_hwp_yfb .section}

**Linux版本**

-   执行方式

    下载对应系统版本工具到目标系统，赋予执行权限后使用管理员权限执行：

    ```
    chmod +x ./ecs-utils-ipv6
    ./ecs-utils-ipv6
    ```

-   执行效果

    如果当前ECS已绑定IPv6地址，则会自动配置；否则会自动清理原有静态IPv6地址配置。

-   命令行参数

    ```
    ecs-utils-ipv6 --help           # show usage
    ecs-utils-ipv6 --version        # show version
    ecs-utils-ipv6                  # auto config all dev ipv6
    ecs-utils-ipv6 --static [dev] [ip6s] [prefix_len] [gw6] # config dev static ipv6
    e.g. ecs-utils-ipv6 --static eth0
           ecs-utils-ipv6 --static eth0 xxx::x1 64 xxx::x0
           ecs-utils-ipv6 --static eth0 "xxx::x1 xxx:x2 xxx:x3" 64 xxx::x0
    ecs-utils-ipv6 --enable         # enable ipv6
    ecs-utils-ipv6 --disable        # disable ipv6
    ```

    可以开启、禁用、手动配置、自动配置（默认）IPv6。

    ```
    ./ecs-utils-ipv6                 #默认可不带参数，自动静态配置多网卡多IPv6
    ./ecs-utils-ipv6 --enable    #开启IPv6
    ./ecs-utils-ipv6 --disable    #禁用IPv6
    ./ecs-utils-ipv6 --static <dev>      #自动配置网卡IPv6
    ./ecs-utils-ipv6 --static <dev> <ip6s> <prefix_len> <gw6>     #手动配置网卡IPv6，支持多IPv6，请用""包含，多个IPv6用空格隔开
    ```


**Windows版本**

-   执行方式

    下载对应系统版本脚本到目标系统，使用管理员权限执行：

    ```
    ecs-utils-ipv6.exe
    ```

-   执行效果

    如果当前ECS已绑定IPv6地址，则会自动配置；否则会自动清理原有静态IPv6地址配置。


## 下载地址 {#section_pxd_lyp_yfb .section}

-   RHEL系列

    支持CentOS 5/6/7， Red Hat 5/6/7，Aliyun Linux 17

    [下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6)

-   Debian系列

    支持Ubuntu 14/16， Debian/8/9

    [下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/debian/ecs-utils-ipv6)

-   SLES系列

    支持SUSE 11/12， OpenSUSE 42

    [下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/sles/ecs-utils-ipv6)

-   CoreOS系列

    支持CoreOS 14/17

    [下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/coreos/ecs-utils-ipv6)

-   FreeBSD系列

    支持FreeBSD 11

    [下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/freebsd/ecs-utils-ipv6)

-   Windows系列

    支持Windows Server 2003/2008/2012/2016（32、64位）

    -   [64位下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/64/ecs-utils-ipv6.exe)
    -   [32位下载地址](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/32/ecs-utils-ipv6.exe)

## 自动化脚本示例 {#section_ykn_bzp_yfb .section}

对于需要自动化配置IPv6实例的需求，比如大批量配置，建议您使用 [云助手](../../../../cn.zh-CN/产品简介/云助手.md#) 或者 [实例自定义数据](cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例自定义数据.md#) 配合脚本的方式来调用。以下为脚本示例。

-   Linux版本（假设是RHEL系列，Bash Shell脚本）：

```
#!/bin/sh
install_dir=/usr/sbin
install_path="$install_dir"/ecs-utils-ipv6
if [ ! -f "$install_path" ]; then
    tool_url="http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6"
    # download the tool
    if ! wget "$tool_url" -O "$install_path"; then
        echo "[Error] download tool failed, code $?"
        exit "$?"
    fi
fi
# chmod the tool
if ! chmod +x "$install_path"; then
    echo "[Error] chmod tool failed, code $?"
    exit "$?"
fi
# run the tool
"$install_path"
```

-   Windows版本（假设是64位，PowerShell脚本）：

```
#powershell
$install_dir="C:\Windows\system32"
$install_path = "$install_dir\ecs-utils-ipv6.exe"

if(-not (Test-Path -Path $install_path)){
    # download the tool
    $tool_url = 'http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/64/ecs-utils-ipv6.exe' 
    Invoke-WebRequest -uri $tool_url -OutFile $install_path
    Unblock-File $install_path
}

# run the tool
Start-Process -FilePath "$install_path" -ArgumentList "--noenterkey" -NoNewWindow
```


