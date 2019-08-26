# 自定义 yum 源、NTP 服务和 DNS 服务 {#concept_52001_zh .concept}

实例自定义脚本是阿里云 ECS 为用户提供的一种自定义实例启动行为的脚本，详细信息请参考阿里云线上帮助文档：[实例自定义数据](../../../../intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例自定义数据.md)。

本文档主要介绍在创建实例时，您怎么使用这个自定义脚本来配置自己的 yum 源、NTP 服务和 DNS 服务。您也可以使用这个脚本自定义 Windows 实例的 NTP 服务和 DNS 服务。

## 场景 {#section_h5m_szv_kfb .section}

目前，实例启动时，阿里云会为实例自动配置预定义的 yum 源、NTP 服务和 DNS 服务。但是，您可能想拥有自己的 yum 源、NTP 服务和 DNS 服务，此时，您就可以使用实例自定义脚本来实现这个需求，此时您要注意：

-   如果您自定义了 yum 源，阿里云官方将不再提供 yum 源相关支持。
-   如果您自定义了 NTP 服务，阿里云官方不再提供相关时间服务。

## 配置方法 {#section_gt1_vzv_kfb .section}

您可以按以下步骤实现上述场景需求。

1.  登录 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)，创建实例，配置如下：
    -    **网络类型**：VPC 网络
    -    **实例规格**：I/O 优化实例
    -    **镜像**：公共镜像的 CentOS 7.2
2.  在创建页面的 自定义数据 输入框中输入如下内容：

    ```language-shell
    #!/bin/sh
    # Modify DNS
    echo "nameserver 8.8.8.8" | tee /etc/resolv.conf
    # Modify yum repo and update
    rm -rf /etc/yum.repos.d/*
    touch myrepo.repo
    echo "[base]" | tee /etc/yum.repos.d/myrepo.repo
    echo "name=myrepo" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "baseurl=http://mirror.centos.org/centos" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "gpgcheck=0" | tee -a /etc/yum.repos.d/myrepo.repo
    echo "enabled=1" | tee -a /etc/yum.repos.d/myrepo.repo
    yum update -y
    # Modify NTP Server
    echo "server ntp1.aliyun.com" | tee /etc/ntp.conf
    systemctl restart ntpd.service
    
    ```

    **说明：** 

    -   第一行必须是 `#!/bin/sh`，前面不能带空格。
    -   全文不能有多余的空格和回车。
    -   您可以根据实例情况定制具体的 DNS、NTP Server 和 yum 源 URL。
    -   上述内容适用于 CentOS 7.2 镜像，如果是其他镜像，请根据需要修改实例自定义脚本。
    -   您也可以使用 `cloud config` 类脚本更改 yum 源设置，但是不够灵活，不能适配阿里云对部分 yum 源进行预配置的情况。建议大家使用 `script` 类的脚本修改 yum 源设置。
3.  根据需要完成 **安全设置**。
4.  完成上述配置后，再单击 **立即购买**，并按页面指示开通实例。

    实例购买完成后，您就可以登录实例查看具体的效果，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9823/153923216812172_zh-CN.png)

    由上图可知，您已经成功自定义了 DNS 服务、NTP 服务和 yum 源。


