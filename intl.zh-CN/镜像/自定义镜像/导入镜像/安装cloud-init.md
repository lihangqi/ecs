# 安装cloud-init {#concept_e3k_vnm_xdb .concept}

在使用Linux类型自定义镜像时，为保证运行该镜像的实例能成功完成初始化配置，建议您根据本文描述在源服务器上安装cloud-init。

## 什么是cloud-init {#section_ats_vz4_kgb .section}

cloud-init是云平台为Linux操作系统的虚拟机做系统初始化配置的开源服务软件。阿里云、AWS、Azure和OpenStack等主流云平台均支持cloud-init。更多详情，请参见[cloud-init官方文档](http://cloudinit.readthedocs.io/)。

阿里云cloud-init能在实例启动阶段完成初始化配置，包括网络、NTP、软件源、主机名和SSH密钥对等，同时进行[实例自定义数据（User data）](intl.zh-CN/实例/管理实例/使用实例自定义数据/生成实例自定义数据.md#)脚本的执行。

## 适用对象 {#section_rdw_dbp_kgb .section}

阿里云所有公共镜像默认安装cloud-init。如果您在以下场景中使用自定义镜像时，为保证创建的实例能自动初始化系统配置，建议您为Linux服务器安装阿里云版本cloud-init：

-   准备迁移上云的，但未安装cloud-init的Linux服务器。
-   已安装cloud-init，但版本低于0.7.9的Linux服务器。
-   已在阿里云运行的，但未安装cloud-init的ECS实例。

## 检查版本 {#section_ud5_5cp_kgb .section}

不同云平台及不同版本之间的cloud-init可能互相不兼容，请选择合适版本并配置合适的数据源（datasource）。其中阿里云cloud-init的版本为0.7.6a，数据源为`Aliyun`。

安装cloud-init后，默认开启开机自启动选项，若所选版本不兼容或数据源配置不当，下次重启服务器时可能导致cloud-init运行异常和系统启动缓慢，甚至无法正常启动系统。安装前请做好数据备份，不准备迁移上云的服务器需谨慎安装。

-   如何检查是否已安装cloud-init：`which cloud-init` 

**说明：** 无输出信息表示未安装，您需要安装阿里云版本cloud-init。

-   如何检查cloud-init版本号命令：`cloud-init --version` 

**说明：** 如果版本低于社区0.7.9版本（0.7.6a版本除外），您需要安装阿里云版本cloud-init。


## （推荐）安装阿里云版本cloud-init {#section_u4y_ytp_kgb .section}

1.  检查并安装python-pip依赖库。
2.  [下载阿里云版本cloud-init](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz)并解压到当前目录：

    ```
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ali-cloud-init-latest.tgz
    ```

3.  进入cloud-init的tools目录，执行cloud-init安装脚本deploy.sh：

    ```
    bash ./deploy.sh <issue> <major_version>
    ```

    -   参数说明如下：

        -   issue：操作系统平台类型，取值范围：centos | redhat |rhel | debian | ubuntu | opensuse | sles。参数取值均大小写敏感，其中sles表示SUSE/SLES。
        -   major\_version：操作系统平台主要版本号。例如，CentOS 6.5的主要版本号为6。
    -   命令示例如下：

        -   在CentOS 6.5中安装cloud-init：

            ```
            bash ./deploy.sh centos 6
            ```

        -   在Ubuntu 14.04中安装cloud-init：

            ```
            bash ./deploy.sh ubuntu 14
            ```

4.  确认是否成功安装。若返回`"description": "success"`，表示安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9704/155861125637025_zh-CN.png)


## 安装阿里云版本cloud-init示例 { .section}

以下为不同发行平台的安装命令示例供您参考：

-   CentOS 6/7

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      yum -y install python-pip
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$( cat /etc/redhat-release | awk '{printf $3}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh centos "$issue_major"
    ```

-   RHEL 6/7

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      yum -y install python-pip
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh rhel "$issue_major"
    ```

-   Ubuntu 14/16/18

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      apt-get install python-pip -y
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh ubuntu "$issue_major"
    ```

-   Debian 8/9

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      apt-get -y install python-pip
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh debian "$issue_major"
    ```

-   SUSE 11/12

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools'>& /dev/null; then
      zypper -n install python-pip
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud/etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh sles "$issue_major"
    ```

-   OpenSUSE 13/42

    ```
    # 检查安装python-pip
    if ! python -c 'import setuptools'>& /dev/null; then
      zypper -n install python-pip
    fi
    # 备份旧版cloud-init配置
    test -d /etc/cloud && mv /etc/cloud/etc/cloud-old
    # 下载并解压阿里云版本cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # 安装cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh opensuse"$issue_major"
    ```


## （可选）安装社区版cloud-init {#section_bw3_b4m_xdb .section}

**前提条件**

安装cloud-init之前，源服务器必须安装git、python 2.7和python-pip依赖软件，以下是安装命令供您参考：

-   CentOS/RedHat：

    ```
    yum -y install git python python-pip
    ```

-   Ubuntu/Debian：

    ```
    apt-get -y install git python python-pip
    ```

-   OpenSUSE/SUSE：

    ```
    zypper -n install git python python-pip
    ```


**操作步骤**

1.  登录源服务器。
2.  使用git下载cloud-init源码包，并进入cloud-init目录：

    ```
    git clone https://git.launchpad.net/cloud-init
    cd ./cloud-init
    ```

3.  安装所有依赖库：

    ```
    pip install -r ./requirements.txt
    ```

4.  安装cloud-init：

    ```
    python setup.py install
    ```

5.  运行`vi /etc/cloud/cloud.cfg`修改配置文件cloud.cfg。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9704/15586112564621_zh-CN.png)

    将`cloud_init_modules:`之前的配置修改为以下内容：

    ```
    # Example datasource config
    # The top level settings are used as module
    # and system configuration.
    # A set of users which may be applied and/or used by various modules
    # when a 'default' entry is found it will reference the 'default_user'
    # from the distro configuration specified below
    users:
       - default
    user:
        name: root
        lock_passwd: False
    # If this is set, 'root' will not be able to ssh in and they 
    # will get a message to login instead as the above $user
    disable_root: false
    # This will cause the set+update hostname module to not operate (if true)
    preserve_hostname: false
    syslog_fix_perms: root:root
    datasource_list: [ AliYun ]
    # Example datasource config
    datasource:
        AliYun:
            support_xen: false
            timeout: 5 # (defaults to 50 seconds)
            max_wait: 60 # (defaults to 120 seconds)
    #      metadata_urls: [ 'blah.com' ]
    # The modules that run in the 'init' stage
    cloud_init_modules:
    ```


## 下一步 {#section_p35_32q_kgb .section}

-   对于准备迁移上云的Linux服务器：您可以[使用迁云工具迁移](intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)或[导入自定义镜像](intl.zh-CN/镜像/自定义镜像/导入镜像/导入自定义镜像.md#)。
-   对于已在阿里云上运行的Linux自定义镜像ECS实例：您可以重启系统验证结果。如果系统自动配置了主机名、软件源和NTP等配置，则表示已成功安装cloud-init。

## 排查故障 {#section_xsx_t4m_xdb .section}

**说明：** 

-   不同镜像缺少的库可能不同，您都可以通过pip安装，之后再次安装cloud-init。
-   如果系统默认软件包管理器（例如yum）和pip管理器分别安装过不同版本的依赖库，可能造成库版本冲突，导致cloud-init运行异常。建议您根据报错信息按需下载依赖库。

**报错：no setuptools module in python**

报错信息提示`no setuptools module in python`，表示您需要安装python setuptools。通过以下方式解决：

-   CentOS/RedHat：`yum -y install python-pip`
-   Ubuntu/Debian：`apt-get -y install python-pip`
-   OpenSUSE/SUSE：`zypper -n install python-pip`

**报错：No module named six**

使用pip安装six库 `pip install six`可以解决以下报错。

```
File "/root/cloud-init/cloudinit/log.py", line 19, in <module>
      import six
  ImportError: No module named six  )
```

**报错：No module named oauthlib.oauth1**

使用pip安装oauthlib库`pip install oauthlib`可以解决以下报错。

```
File "/root/cloud-init/cloudinit/url_helper.py", line 20, in <module>
      import oauthlib.oauth1 as oauth1
  ImportError: No module named oauthlib.oauth1  )
```

**报错时没有明确缺少的依赖库**

如果安装报错时，没有明确提示缺少哪些依赖库时，您可以根据cloud-init的requirements.txt文件里显示的库，安装所有依赖库：

```
pip install -r requirements.txt
```

## 参考链接 {#section_qsb_npm_xdb .section}

[cloud-init官网 - 阿里云数据源说明文档](http://cloudinit.readthedocs.io/en/latest/topics/datasources/aliyun.html)

