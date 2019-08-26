# User-defined yum sources, NTP services and DNS services {#concept_52001_zh .concept}

User-defined scripts are a type of script provided by Alibaba Cloud for users to customize the startup behaviors of ECS instances. For more information, see [User-defined data](../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/User data.md).

This example uses a Linux instance to demonstrate how to use a user-defined script to configure your own yum repository, NTP service, and DNS service when creating a Linux instance. User-defined scripts also enable you to configure NTP service and DNS service for a Windows instance.

## Scenarios {#section_adj_21w_kfb .section}

When a Linux instance is started, Alibaba Cloud automatically configures a pre-defined yum repository, NTP service, and DNS service for the instance. However, if you want to have your own yum repository, NTP service, and DNS service, use user-defined scripts to implement them.

-   If you are using a custom yum repository, Alibaba Cloud does not provide support for it.
-   If you are using a custom NTP service, Alibaba Cloud does not provide time service.

## Procedure {#section_nvj_h1w_kfb .section}

To customize your yum repository, NTP service, and DNS service for a Linux instance when creating it, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) and create an instance. Configure the instance as follows:
    -    **Network Type**: Select VPC.
    -    **Instance Type**: Select an I/O-optimized instance.
    -    **Operating System**: Select CentOS 7.2 in Public Image tab.
2.  Enter the following script in the User Data box on the instance creation page.

    ```language-shell
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

    -   The first line must be `#!, with no leading space. /bin/sh`,with no leading space.
    -   Do not add unnecessary spaces or carriage return characters in the full text.
    -   You can customize URLs of your own DNS server, NTP Server, and yum repository based on the instance situations.
    -   The preceding content applies to CentOS 7.2. If you are using other images, modify the scripts as needed.
    -   You can also define the yum repository in the scripts of the `cloud config`type, but it is not recommended because it is not flexible enough to get adapted to Alibaba Cloud that may pre-configure some yum repository. Scripts of `script` type is recommended for changing the yum repository.
3.  Complete the **security settings** as needed.
4.  After you complete the configuration, click **Buy Now** and activate the instance following the instructions on the page.

    After the instance is created, you can connect to the instance to view the implementation details, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9823/153923217412172_en-US.png)

    The preceding figure shows that you have successfully customized the DNS service, the NTP service, and the yum repository.


