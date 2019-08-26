# Install cloud-init for Linux images {#concept_e3k_vnm_xdb .concept}

When you use a custom Linux image, we recommend that you install cloud-init in your servers to guarantee successful initialization of the instances running that image.

## What is cloud-init? {#section_ats_vz4_kgb .section}

cloud-init is an open source software used by cloud-based platforms to configure system initialization of Linux instances. It is supported by major platforms such as Alibaba Cloud, AWS, Azure, and OpenStack. For more information, see [cloud-init documentation](http://cloudinit.readthedocs.io/).

Alibaba Cloud cloud-init initializes the configurations of instances during their startup, including the network, NTP, software source, host name, and SSH key pair. It also executes the [user data](reseller.en-US/Instances/Configure instances/User-defined data/User data.md#) script.

## Scenarios {#section_rdw_dbp_kgb .section}

Cloud-init is installed by default for all public images of Alibaba Cloud. If you use custom images in the following scenarios, we recommend that you install Alibaba Cloud cloud-init for your Linux servers so as to ensure the system configurations of created instances can be automatically initialized:

-   Linux servers that will be migrated to Alibaba Cloud, but have not installed cloud-init.
-   Linux servers that have installed cloud-init whose version is earlier than 0.7.9.
-   Alibaba Cloud ECS instances that have not installed cloud-init.

## Check the cloud-init version {#section_ud5_5cp_kgb .section}

Different cloud platforms may use different versions of cloud-init. Please select the appropriate version and configure the appropriate datasource. Alibaba Cloud uses cloud-init 0.7.6a and the data source is `Aliyun`.

After cloud-init is installed, its option of self-start upon instance startup is enabled by default. If the selected cloud-init version or data source is not suitable, cloud-init may run abnormally and the instance may start slowly \(or fail to start\) the next time you restart your instance. As a result, we recommend that you back up your data before you install it. Exercise caution when you install it if you are not fully ready to migrate your servers onto Alibaba Cloud.

-   Check if cloud-init is installed:`which cloud-init`

**Note:** No output indicates that it is not installed and you need to install the Alibaba Cloud cloud-init.

-   Check the cloud-init version: `cloud-init --version`

**Note:** If the version is earlier than the community version 0.7.9 \(except 0.7.6a\), you need to install the Alibaba Cloud cloud-init.


## \(Recommended\) Install the Alibaba Cloud cloud-init {#section_u4y_ytp_kgb .section}

1.  Check and install the python-pip dependency.
2.  [Download the Alibaba Cloud cloud-init](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/tools/ali-cloud-init-latest.tgz) and decompress it to the current directory:

    ```
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ali-cloud-init-latest.tgz
    ```

3.  Enter the tools directory of cloud-init, and then run the cloud-init installation script deploy.sh:

    ```
    bash ./deploy.sh <issue> <major_version>
    ```

    -   The parameters are described as follows:

        -   issue: The operating system platform. The value range is: centos | redhat |rhel | debian | ubuntu | opensuse | sles. The parameter values are case sensitive. sles represents SUSE/SLES.
        -   major\_version: The major version of an operating system platform. For example, the major version of CentOS 6.5 is 6.
    -   The following are command examples:

        -   Install cloud-init in CentOS 6.5:

            ```
            bash ./deploy.sh centos 6
            ```

        -   Install cloud-init in Ubuntu 14.04:

            ```
            bash ./deploy.sh ubuntu 14
            ```

4.  Confirm that the installation is successful. If `"description": "success"` is returned, the installation is successful.

    ![cloud-init successfully installed](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9704/155108533037025_en-US.png)


## Install the Alibaba Cloud cloud-init in different platforms { .section}

Installation commands for different platforms are shown as follows:

-   CentOS 6/7

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      yum -y install python-pip
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$( cat /etc/redhat-release | awk '{printf $3}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh centos "$issue_major"
    ```

-   RHEL 6/7

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      yum -y install python-pip
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$(cat /etc/os-release | grepVERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh rhel "$issue_major"
    ```

-   Ubuntu 14/16/18

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      apt-get install python-pip -y
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh ubuntu "$issue_major"
    ```

-   Debian 8/9

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools' >& /dev/null; then
      apt-get -y install python-pip
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud /etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$(cat /etc/os-release | grep VERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh debian "$issue_major"
    ```

-   SUSE 11/12

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools'>& /dev/null; then
      zypper -n install python-pip
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud/etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$(cat /etc/os-release | grepVERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh sles "$issue_major"
    ```

-   OpenSUSE 13/42

    ```
    # Check and install python-pip
    if ! python -c 'import setuptools'>& /dev/null; then
      zypper -n install python-pip
    fi
    # Back up the legacy cloud-init configuration
    test -d /etc/cloud && mv /etc/cloud/etc/cloud-old
    # Download and decompress the Alibaba Cloud cloud-init
    wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/cloudinit/ali-cloud-init-latest.tgz
    tar -zxvf ./ali-cloud-init-latest.tgz
    # Install cloud-init
    issue_major=$(cat /etc/os-release | grepVERSION_ID | awk -F'"' '{printf $2}' | awk -F'.' '{printf $1}')
    bash ./cloud-init-*/tools/deploy.sh opensuse"$issue_major"
    ```


## \(Optional\) Install the community cloud-init {#section_bw3_b4m_xdb .section}

**Prerequisites**

Before installing cloud-init, you must install the git, python 2.7, and python-pip dependencies. The installation commands are as follows:

-   CentOS/RedHat:

    ```
    yum -y install git python python-pip
    ```

-   Ubuntu/Debian:

    ```
    apt-get -y install git python python-pip
    ```

-   OpenSUSE/SUSE:

    ```
    zypper -n install git python python-pip
    ```


**Procedure**

1.  Log on to the source server.
2.  Download the cloud-init package through git and enter the cloud-init directory:

    ```
    git clone https://git.launchpad.net/cloud-init
    cd ./cloud-init
    ```

3.  Install all the dependencies:

    ```
    pip install -r ./requirements.txt
    ```

4.  Install cloud-init:

    ```
    python setup.py install
    ```

5.  Run `vi /etc/cloud/cloud.cfg` to modify the configuration file cloud.cfg.

    ![cloud-initcloud.cfg](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9704/15510853304621_en-US.png)

    Modify the configurations of `cloud_init_modules:` as follows:

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


## What to do next {#section_p35_32q_kgb .section}

-   For Linux servers that are ready for migration to the cloud, you can [migrate them to Alibaba Cloud by using the Cloud Migration tool](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) or [import custom images](reseller.en-US/Images/Image release notes/Import images/Import custom images.md#).
-   For ECS instances with custom Linux images that are already running on Alibaba Cloud, you can restart the system for verification. If the system is automatically configured with the host name, software source, and NTP, cloud-init is successfully installed.

## Troubleshooting {#section_xsx_t4m_xdb .section}

**Note:** 

-   The libraries that are missing may vary according to the images. To resolve this issue, you can install them through pip, and then install cloud-init again.
-   If the default package manager \(for example yum\) and the pip manager have installed different versions of libraries, library version conflicts may occur and lead to cloud-init running abnormally. We recommend that you download the dependency libraries according to the reported errors.

**Error: no setuptools module in python**

The error prompt `no setuptools module in python` means you need to install python setuptools. You can fix it in the following ways:

-   CentOS/RedHat: `yum -y install python-pip`
-   Ubuntu/Debian: `apt-get -y install python-pip`
-   OpenSUSE/SUSE: `zypper -n install python-pip`

**Error: No module named six**

Run `pip install six` to resolve the following error.

```
File "/root/cloud-init/cloudinit/log.py", line 19, in <module>
      import six
  ImportError: No module named six  )
```

**Error: No module named oauthlib.oauth1**

Run `pip install oauthlib` to resolve the following error.

```
File "/root/cloud-init/cloudinit/url_helper.py", line 20, in <module>
      import oauthlib.oauth1 as oauth1
  ImportError: No module named oauthlib.oauth1  )
```

**Error messages do not indicate the missing libraries**

If error messages do not indicate the missing libraries during installation, you can install all the dependency libraries displayed in the file requirements.txt of cloud-init.

```
pip install -r requirements.txt
```

## References {#section_qsb_npm_xdb .section}

[cloud-init website - Alibaba Cloud \(AliYun\)](http://cloudinit.readthedocs.io/en/latest/topics/datasources/aliyun.html)

