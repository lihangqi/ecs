# 自定义yum源、NTP服务和DNS服务 {#concept_52001_zh .concept}

本文档主要介绍在创建Linux实例时如何使用实例自定义数据配置 yum 源、NTP 服务和 DNS 服务。您也可以使用这个脚本自定义 Windows 实例的 NTP 服务和 DNS 服务。

## 注意事项 {#section_h5m_szv_kfb .section}

目前，实例启动时，阿里云会为实例自动配置预定义的 yum 源、NTP 服务和 DNS 服务。如果您需要自行管理 yum 源、NTP 服务和 DNS 服务，可以使用实例自定义数据，但需要注意：

-   如果您自定义了 yum 源，阿里云官方将不再提供 yum 源相关支持。
-   如果您自定义了 NTP 服务，阿里云官方不再提供相关时间服务。

## 操作步骤 {#section_gt1_vzv_kfb .section}

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
3.  创建一台实例。

    步骤请参见[使用向导创建实例](cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。但需要注意以下配置项：

    -   在基础配置页面中，注意以下实例自定义数据相关的配置。
        -   **实例规格**：选择 I/O 优化实例。
        -   **镜像**：选择支持的镜像，例如，公共镜像的 CentOS 7.2。
    -   在网络和安全组页面中，注意**网络类型**配置为**专有网络**。
    -   在系统配置页面中，在自定义数据输入框中输入如下内容：

        ``` {#codeblock_nun_aye_vd6 .language-shell}
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
        -   您也可以使用 `cloud config` 类脚本更改 yum 源设置，但是不够灵活，不能适配阿里云对部分 yum 源进行预配置的情况。建议使用 `script` 类的脚本修改 yum 源设置。

实例启动完成后，登录实例查看具体的效果，如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9823/156082817149570_zh-CN.png)

由上图可知，您已经成功自定义了 DNS 服务、NTP 服务和 yum 源。

