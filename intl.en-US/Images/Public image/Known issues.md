# Known issues {#concept_e3m_ktl_jgb .concept}

This topic describes the known issues of Alibaba Cloud images on different platforms, the scope of these issues, and the corresponding solution.

## Debian 9.6: Classic network configuration {#section_zyc_kxl_jgb .section}

-   **Issue**: Classic network instances created by using Debian 9 public images fail to be pinged.
-   **Cause**: Classic network instances cannot obtain IP addresses automatically through the Dynamic Host Configuration Protocol \(DHCP\) because Debian 9 disables the systemd-networkd service by default.
-   **Image**: debian\_9\_06\_64\_20G\_alibase\_20181212.vhd
-   **Solution**: Run the following command:

    ```
    systemctl enable systemd-networkd 
    systemctl start systemd-networkd
    ```


## CentOS 6.8: An instance installed with the NFS Client fails to respond {#section_bwm_1hc_dhb .section}

-   **Issue**: An instance that is running CentOS 6.8 and has NFS Client installed fails repeatedly to respond and must be restarted.
-   **Cause**: When you use the NFS service, the NFS Client attempts to end the TCP connection if a glitch occurs due to communication latency. Specifically, if the NFS Server is delayed in sending a response to the NFS Client, the connection initiated by the NFS Client may be stalled in the FIN\_WAIT2 state. Normally, the FIN\_WAIT2 connection expires and closes after one minute and the NFS Client initiates another connection. However, a kernel of version 2.6.32-696 to 2.6.32-696.10 has a defect in TCP connection establishment. As a result, the FIN\_WAIT2 connection will remain indefinitely, which means the NFS Client cannot end the TCP connection and then initiate a new TCP connection.
-   **Image**: centos\_6\_08\_32\_40G\_alibase\_20170710.vhd and centos\_6\_08\_64\_20G\_alibase\_20170824.vhd
-   **Solution**: Run the following command to upgrade the kernel to v2.6.32-696.11 or a later version.

    ```
    yum update
    ```

    **Note:** Before you perform any operations on the instance, you must [create a snapshot](../../../../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up your data.


## CentOS 7: The hostname changes from uppercase to lowercase letters after the instance is restarted {#section_qcx_jvc_dhb .section}

-   **Issue**: After an ECS instance is restarted for the first time, the hostname of some CentOS 7 instances is changed from uppercase letters to lowercase letters. The following table shows some examples.

    |Hostname|Hostname after the instance is restarted for the first time|Does the hostname remain in lowercase after the restart?|
    |:-------|:----------------------------------------------------------|:-------------------------------------------------------|
    |iZm5e1qe\*\*\*\*\*sxx1ps5zX|izm5e1qe\*\*\*\*\*sxx1ps5zx|Yes|
    |ZZHost|zzhost|Yes|
    |NetworkNode|networknode|Yes|

-   **Image**: The following CentOS public images \(and custom images created based on them\) are affected:
    -   centos\_7\_2\_64\_40G\_base\_20170222.vhd
    -   centos\_7\_3\_64\_40G\_base\_20170322.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170503.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170523.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170625.vhd
    -   centos\_7\_03\_64\_40G\_alibase\_20170710.vhd
    -   centos\_7\_02\_64\_20G\_alibase\_20170818.vhd
    -   centos\_7\_03\_64\_20G\_alibase\_20170818.vhd
    -   centos\_7\_04\_64\_20G\_alibase\_201701015.vhd
-   **Hostname**: If your applications are sensitive to the letter casing of hostnames, restarting such instances may affect the availability of corresponding services. The following table describes whether the hostname is changed after an instance is restarted.

    |Current state of hostname|Will the hostname change after an instance restart?|When will the change take effect?|
    |:------------------------|:--------------------------------------------------|:--------------------------------|
    |The hostname contains uppercase letters at the time of instance creation \(either in the ECS console or through APIs\).|Yes|When the instance is restarted for the first time.|
    |The hostname contains no uppercase letters at the time of instance creation \(either in the ECS console or through APIs\).|No|N/A|
    |The hostname contains uppercase letters because the hostname is modified after you log on to an instance.|No|N/A|

-   **Solution**: To retain uppercase letters in a hostname after you restart an instance, follow these steps:
    1.  Connect to the target instance.
    2.  View the existing hostname:

        ``` {#codeblock_eqi_06q_ft0}
        [root@izbp193*****3i161uynzzx ~]# hostname
        izbp193*****3i161uynzzx
        ```

    3.  Run the following command:

        ``` {#codeblock_jvk_zp9_ncm}
        hostnamectl set-hostname --static iZbp193*****3i161uynzzX
        ```

    4.  View the updated hostname.

        ``` {#codeblock_k28_zfk_w6z}
        [root@izbp193*****3i161uynzzx ~]# hostname
        iZbp193*****3i161uynzzX
        ```

-   **Additional actions**: If you are using a custom image, we recommend that you update the cloud-init software to the latest version and create a custom image again. Such an action prevents the custom image from being affected by the aforementioned issue. For more information, see [Install cloud-init](reseller.en-US/Images/Custom image/Import images/Install cloud-init for Linux images.md#) and [Create a custom image by using an instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

## Linux: The pip requests time out {#section_yee_nt1_43y .section}

-   **Issue**: The pip requests occasionally time out or fail.
-   **Image**: CentOS, Debian, Ubuntu, SUSE, OpenSUSE, and Aliyun Linux.
-   **Cause**: Alibaba Cloud provides the following three pip source addresses, and the default address is mirrors.aliyun.com. To access this address, instances need to be able to access Internet. If your instance has no public IP address assigned, a pip request timeout will occur.
    -   \(Default\) Internet: mirrors.aliyun.com
    -   VPC intranet: mirrors.cloud.aliyuncs.com
    -   Classic network intranet: mirrors.aliyuncs.com
-   **Solution**: You can solve the problem through one of the following methods:
    -   Method 1

        Assign a public IP address to your instance, that is, attaching an Elastic IP address \(EIP\) to your instance. For more information, see [Bind EIP to an ENI](../../../../reseller.en-US/User Guide/Associate an EIP with an ENI.md#).

        A Subscription instance can also be reassigned a public IP address through changing its configurations. For more information, see [Upgrade configurations of Subscription instances](../../../../reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#).

    -   Method 2

        Once a pip request fails, you can run the script fix\_pypi.sh in your ECS instance and then retry the pip operation. The specific steps are as follows:

        1.  Connect to your ECS instance. For more information, see [Connect to an instance by using the Management Terminal](../../../../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#).
        2.  Run the following command to get the script file:

            ``` {#codeblock_qil_6bn_w52}
            wget http://image-offline.oss-cn-hangzhou.aliyuncs.com/fix/fix_pypi.sh
            ```

        3.  Run the script.
            -   For VPC instances, run the command `bash fix_pypi.sh "mirrors.cloud.aliyuncs.com"`.
            -   For Classic network instances, run the command `bash fix_pypi.sh "mirrors.aliyuncs.com"`.
        4.  Retry the pip operation.
        The content of fix\_pypi.sh is as follows:

        ``` {#codeblock_s9m_90o_2f4}
        #!/bin/bash
        function config_pip() {
            pypi_source=$1
            if [[ ! -f ~/.pydistutils.cfg ]]; then
        cat > ~/.pydistutils.cfg << EOF
        [easy_install]
        index-url=http://$pypi_source/pypi/simple/
        EOF
            else
                sed -i “s#index-url.#index-url=http://$pypi_source/pypi/simple/#“ ~/.pydistutils.cfg
            fi
            if [[ ! -f ~/.pip/pip.conf ]]; then
            mkdir -p ~/.pip
        cat > ~/.pip/pip.conf << EOF
        [global]
        index-url=http://$pypi_source/pypi/simple/
        [install]
        trusted-host=$pypi_source
        EOF
            else
                sed -i “s#index-url.#index-url=http://$pypi_source/pypi/simple/#“ ~/.pip/pip.conf
                sed -i “s#trusted-host.*#trusted-host=$pypi_source#” ~/.pip/pip.conf
            fi
        }
        config_pip $1
        ```


## Aliyun Linux 2: Enabling the CONFIG\_PARAVIRT\_SPINLOCK kernel feature causes performance issues {#section_nnm_3mw_fhb .section}

-   **Issue**: After you enable the `CONFIG_PARAVIRT_SPINLOCK` kernel feature, application performance is significantly impacted if there are a large number of vCPUs in an ECS instance and lock contentions in applications. For example, timed out connections degrade the performance of an Nginx application.
-   **Image**: Aliyun Linux 2
-   **Solution**: We recommend that you do not enable the `CONFIG_PARAVIRT_SPINLOCK` kernel feature for Aliyun Linux 2 \(disabled by default\).

## Aliyun Linux 2: Setting the THP switch to always impacts system stability and causes performance issues {#section_mrx_xnw_fhb .section}

-   **Issue**: After you set the Transparent Hugepage \(THP\) switch in your production environment to always, the system becomes unstable and performance is noticeably degraded.
-   **Image**: Aliyun Linux 2
-   **Solution**: Set the THP switch to `madvise`. In outlier scenarios \(for example, if you run some performance benchmark test suites\), although performance is impacted if this switch is set to `madvise`, we recommend that you do so to prevent the system from being impacted by other contentions.

## Aliyun Linux 2: A delegation conflict occurred in NFS v4.0 {#section_mmx_qrw_fhb .section}

-   **Issue**: A delegation conflict occurred in NFS v4.0. For more information, see [Delegation in NFS Version 4](https://docs.oracle.com/cd/E19253-01/816-4555/rfsrefer-140/index.html).
-   **Image**: Aliyun Linux 2
-   **Solution**: We recommend that you do not enable the Delegation feature when you use NFS v4.0. For information on how to disable this feature at the server side, see [How to Select Different Versions of NFS on a Server](https://docs.oracle.com/cd/E19253-01/816-4555/rfsadmin-965/index.html).

## Aliyun Linux 2: NFS v4.1/4.2 has a defect that may cause logout failure of applications {#section_w35_dyw_fhb .section}

-   **Issue**: In NFS v4.1 or v4.2, if you use Asynchronous I/O \(AIO\) in applications to distribute requests, and close the corresponding file descriptors before all I/Os are returned, a livelock may be triggered and the corresponding process cannot be ended.
-   **Image**: Aliyun Linux 2
-   **Solution**: This problem has been fixed in kernel v4.13.10-10.al7 and higher. To upgrade the kernel version, run the command `sudo yum update kernel -y` 

    **Note:** 

    -   Upgrading the kernel may result in system boot failure. Please exercise caution when performing this action.
    -   Before you upgrade the kernel, make sure you have created a snapshot or custom image to back up data. For more information, see [Create a snapshot](../../../../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) or [Create a custom image by using an instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

## Aliyun Linux 2: System performance is impacted when a high-risk security vulnerability \(such as Spectre or Meltdown\) is fixed {#section_a2j_d4y_ghb .section}

-   **Issue**: In the kernel of Aliyun Linux 2, the repair of high-risk security vulnerabilities \(Meltdown and Spectre\) in processor hardware is enabled by default, which impacts system performance. As a result, performance degradation may be recorded during performance benchmark suite tests.
-   **Image**: Aliyun Linux 2
-   **Solution**: We recommend that in normal circumstances you do not disable the repair function. However, if you need to maximize system performance, you can run the following command to disable the repair function:

    ``` {#codeblock_aqa_pwf_9md}
    # Add nopti nospectre_v2 to the kernel startup parameters.
    sudo sed -i 's/\(GRUB_CMDLINE_LINUX=".*\)"/\1 nopti nospectre_v2"/' /etc/default/grub
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    
    # Restart the system.
    sudo reboot
    ```


