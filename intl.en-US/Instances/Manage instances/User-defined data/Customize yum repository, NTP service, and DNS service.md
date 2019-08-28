# Customize yum repository, NTP service, and DNS service {#concept_52001_zh .concept}

This topic describes how to use a user-defined script to configure your own yum repository, NTP service, and DNS service when creating a Linux instance. User-defined scripts also enable you to configure NTP service and DNS service for a Windows instance.

## Scenarios {#section_adj_21w_kfb .section}

When a Linux instance is started, Alibaba Cloud automatically configures a pre-defined yum repository, NTP service, and DNS service for the instance. However, if you want to have your own yum repository, NTP service, and DNS service, use user-defined scripts to implement them.

-   If you are using a custom yum repository, Alibaba Cloud does not provide support for it.
-   If you are using a custom NTP service, Alibaba Cloud does not provide time service.

## Procedure {#section_nvj_h1w_kfb .section}

To customize your yum repository, NTP service, and DNS service for a Linux instance when creating it, follow these steps:

1.  Create an instance [by using the wizard](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). Be aware of the following configuration items:
    -   On the Basic Configurations page, note the following customized configurations:
        -   **Instance Type**: Select an I/O-optimized instance.
        -   **Image**: Select a supported image type, for example, CentOS 7.2 on the **Public Image** tab.
2.  On the **Networking** page, set **Network Type** to VPC
3.  On the System Configurations page, enter the following script in the **User Data** text box in the **Advanced** area:

    ``` {#codeblock_3z1_10l_bkn .language-shell}
    #! /bin/sh
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

    **Note:** 

    -   The first line must be `#!, with no leading space. /bin/sh`, with no leading space.
    -   Do not add unnecessary spaces or carriage return characters in the full text.
    -   You can customize URLs of your own DNS server, NTP Server, and yum repository based on the instance situations.
    -   The preceding content applies to CentOS 7.2. If you are using other images, modify the scripts as needed.
    -   You can also define the yum repository in the scripts of the `cloud config` type, but it is not recommended because it is not flexible enough to get adapted to Alibaba Cloud that may pre-configure some yum repository. Scripts of `script` type is recommended for changing the yum repository.

After the instance is created, you can connect to the instance to view the implementation details, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9823/156678812912172_en-US.png)

The preceding figure shows that you have successfully customized the DNS service, the NTP service, and the yum repository.

