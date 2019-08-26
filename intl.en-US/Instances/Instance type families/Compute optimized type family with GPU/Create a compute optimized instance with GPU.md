# Create a compute optimized instance with GPU {#concept_g5s_g2z_xdb .concept}

This topic describes how to create a compute optimized instance with GPU \(hereinafter referred to as GPU instance\) and configure the GPU driver to be automatically installed at instance creation. GPU instances can be used only after the GPU driver is installed. If you do not configure automatic installation of the GPU driver when you create a GPU instance, you can install it manually after you create the GPU instance.

## Limits {#section_urs_qd1_ydb .section}

If you configure automatic installation of the GPU driver, the following limits apply:

-   Only public images of Linux OSs support automatic installation of the GPU driver.
-   Automatic installation of the GPU driver takes 4 to 10 minutes, depending on the intranet bandwidth and the CPU count of different instance types. During automatic installation, GPU cannot be used, the instance cannot be operated, and other GPU software cannot be installed. Otherwise, the automatic installation fails and the instance becomes unavailable.
-   If you change the operating system after you create a GPU instance, you must make sure that you use the same image or [Images that support automatic installation of the GPU driver](#section_gbb_nxz_xdb). Otherwise, automatic installation of the GPU driver fails.

**Note:** You can [connect to the target instance](reseller.en-US/Instances/Connect to instances/Overview.md#) and check the installation progress and result by using the installation log.

-   If you select **Auto-install GPU Driver**, the installation log is stored in the /root/nvidia\_install.log directory.
-   If you configure the nvidia\_install\_v2.0 installation script in **User Data**, the installation log is stored in the /root/nvidia/nvidia\_install.log directory.

## Procedure {#section_v1b_nxz_xdb .section}

The following procedure describes how to configure a GPU instance. For information on how to configure general instances, see [Create an instance](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).

1.  Go to the [ECS purchase page](https://ecs-buy-intl4service.aliyun.com/#/postpay).
2.  Complete the following Basic Configurations.
    -   **Region**: Select the target region. For information about regions and zones, see [Regions and zones that provide GPU instances](#section_e2n_pnb_ygb). If the regions and zones listed in this table are different from those displayed on the Basic Configurations page, the regions and zones displayed on the page are the actual regions and zones available.
    -   **Instance Type**: Choose **Heterogeneous Computing** \> **Compute Optimized Type with GPU**, and then select an instance type as needed.
    -   **Image**: Some **Public Image** items of Linux OSs support automatic installation of the CUDA Toolkit and the GPU driver. For more information, see [Images that support automatic installation of the GPU driver](#section_gbb_nxz_xdb).

        If you select an image that supports automatic installation of the preceding drivers, select **Auto-install GPU driver**, and select a GPU driver version. If you want to use the GPU instance for a new service system, we recommend that you select the latest GPU driver version.

        If you do not select **Auto-install GPU driver**, or if the selected image does not support automatic installation of the GPU driver, you need to configure the installation script in **User Data**, or [Install the GPU driver](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Install the GPU driver.md#) after you install the GPU instance. For information on how to configure the installation script, see [Script version](#section_xcj_1s5_xgb).

        **Note:** If you call the [RunInstances](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) API action to create a GPU instance, you need to use the UserData parameter to upload the installation script, which must be Base64-encoded.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/156636449739823_en-US.png)

3.  Complete the Networking configurations as follows:
    -   **Network Type**: Select **VPC**.
    -   **Network Billing Method**: Select a bandwidth as needed.

        **Note:** If you select Windows 2008 R2 or an earlier image on the **Basic Configurations** page, the GPU instance cannot be accessed by using the [Management Terminal](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#) after the GPU driver takes effect after installation. To resolve this issue, you must select **Assign Public IP**, or [bind EIP](../../../../reseller.en-US/User Guide/Associate an EIP with a cloud instance/Associate an EIP with an ECS instance.md#) after you create the instance. In this way, you can connect to the instance by using other protocols, such as RDP, PCOIP, and XenDeskop HDX 3D. However, RDP does not support such applications as DirectX or OpenGL. If you require RDP to be the protocol, you must install the VNC service and the VNC client.

4.  Complete the System Configurations as follows:
    -   **Log on Credentials**: Select **Key Pair** or **Password**. If you select **Set Later**, you must associate an SSH key pair or reset your password when you log on to the instance by using the Management Terminal, and then restart the instance to make the settings take effect. If the GPU driver is not installed completely, the restart operation will result in installation failure.
    -   **User Data**:
        -   If you select **Auto-install GPU Driver** in the **Image** area on the Basic Configurations page, the Shell script and the precautionary information regarding the installation of the CUDA Toolkit and the GPU driver are displayed in this area.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/156636449739825_en-US.png)

        -   If you do not select **Auto-install GPU Driver**, you can configure the installation script in the **User Data** area. For an installation script example, see [User Data installation script](#section_bl2_k23_ygb).
5.  Complete the Grouping configurations and confirm your order on the Preview page.

    **Note:** 

    -   If you configure an automatic installation script, the GPU driver is automatically installed after you install the GPU instance. After the GPU driver is installed, the GPU instance is automatically restarted. Then, the GPU driver can operate properly.
    -   The GPU driver operates more reliably in the **Persistence** mode. The installation script automatically enables the **Persistence** mode of the GPU driver and adds this setting to the automatic startup script. This mode is then enabled by default whenever the instance is restarted.

## Regions and zones that provide GPU instances {#section_e2n_pnb_ygb .section}

The following table describes the regions and zones where GPU instance type families are available.

|Instance type|Region and zone|
|-------------|---------------|
|gn4| -   China \(Beijing\) zone A, China \(Shanghai\) zone B
-   China \(Shenzhen\) zone C

 |
|gn5| -   China \(Beijing\) zones C and E, China \(Hohhot\) zone A
-   China \(Hangzhou\) zones G and F, China \(Shanghai\) zones D, B, and E
-   China \(Shenzhen\) zone D
-   China \(Hong Kong\) zones C and B
-   Singapore zones B and A, Australia zone A, Malaysia zone A, Indonesia zone A
-   US \(Silicon Valley\) zones B and A, US \(Virginia\) zones B and A
-   Germany \(Frankfurt\) zone A

 |
|gn5 \(NGC environment\)|The instance type family gn5 does not fully support the NVIDIA GPU CLOUD \(NGC\) environment. For more information, see [Deploy an NGC on gn5 instances](reseller.en-US/Best Practices/GPU instances/Deploy an NGC on gn5 instances.md#).|
|gn5i| -   China \(Beijing\) zones C, E, and A
-   China \(Hangzhou\) zone B, China \(Shanghai\) zones D and B
-   China \(Shenzhen\) zone A

 |
|gn6v|China \(Shanghai\) zone F|

## Images that support automatic installation of the GPU driver {#section_gbb_nxz_xdb .section}

The following table describes the images that support automatic installation of the CUDA Toolkit and the GPU driver.

|Image|Version|
|-----|-------|
|Public image|The following versions are supported: -   CentOS 64-bit \(All available versions are supported.\)
-   Ubuntu 16.04 64-bit
-   SUSE Linux Enterprise Server 12 SP2 64-bit

 |
|Alibaba Cloud Marketplace|Depending on your image requirements, obtain the required image by using either of the following methods: -   Search for **NVIDIA** and select the required image. Currently, only CentOS 7.3 is supported.
-   If you want to use the GPU instance for deep learning, you can select an image that has a pre-installed deep learning frame. To do so, search for **Deep Learning** and select the required image. Currently, only CentOS 7.3 is supported.

 |

## Script version {#section_xcj_1s5_xgb .section}

When the GPU instance is restarted for the first time, the cloud-init tool automatically runs the Shell script to install the CUDA Toolkit and the GPU driver.

-   If you select **Auto-install GPU Driver**, the GPU instance uses nvidia\_install\_v1.0. The following table describes the available CUDA Toolkit versions of GPU driver versions.

    |CUDA|GPU driver|Supported instance type|
    |----|----------|-----------------------|
    |9.1.85|390.46|     -   gn5
    -   gn5i
    -   gn6v
    -   gn4
 |
    |9.0.176|     -   390.46
    -   384.125
    -   384.111
 |     -   gn5
    -   gn5i
    -   gn6v
    -   gn4
 |
    |8.0.61|     -   390.46
    -   384.125
    -   384.111
 |     -   gn5
    -   gn5i
    -   gn4
 |

-   If you configure the installation script in the **User Data** area, we recommend that you use nvidia\_install\_v2.0. For more information, see [User Data installation script](#section_bl2_k23_ygb). The nvidia\_install\_v2.0 script has the following benefits:

    -   It provides the latest CUDA Toolkit, GPU driver, and cuDNN library.
    -   After you log on to the instance, a bar is displayed to indicate the installation progress of the GPU driver. Alternatively, you can see the installation result when installation is completed \(**NVIDIA INSTALL OK** or **NVIDIA INSTALL FAIL**\).
    If you use the nvidia\_install\_v2.0 script, you need to specify the version number of the GPU driver, CUDA Toolkit, and cuDNN library. For example:

    ``` {#codeblock_3g2_o5s_7uz}
    driver_version="410.79"
    cuda_version="9.0.176"
    cudnn_version="7.4.2"
    ```

    The following table describes the supported CUDA Toolkit, GPU driver, and cuDNN library versions.

    |CUDA|GPU driver|cuDNN library|
    |----|----------|-------------|
    |10.0.130|410.79|     -   7.4.2
    -   7.3.1
 |
    |9.2.148|     -   410.79
    -   396.44
 |     -   7.4.2
    -   7.3.1
    -   7.1.4
 |
    |9.0.176|     -   410.79
    -   396.44
    -   390.46
 |     -   7.4.2
    -   7.3.1
    -   7.1.4
    -   7.0.5
 |
    |8.0.61|     -   410.79
    -   396.44
    -   390.46
 |     -   7.1.3
    -   7.0.5
 |


## User Data installation script {#section_bl2_k23_ygb .section}

If you install the GPU driver by using **User Data**, we recommend that you use the nvidia\_install\_v2.0 script as follows:

``` {#codeblock_1i3_c2a_8rc}
#!/bin/sh
driver_version=$1
cuda_version=$2
cudnn_version=$3
NVIDIA_DIR="/root/nvidia"
log=${NVIDIA_DIR}"/nvidia_install.log"
PROCESS_NAME="/var/lib/cloud/instance/scripts/part-001"
DRIVER_PROCESS_NAME=${NVIDIA_DIR}"/NVIDIA-Linux-x86_64"
CUDA_PROCESS_NAME=${NVIDIA_DIR}"/cuda"
CUDNN_PROCESS_NAME=${NVIDIA_DIR}"/cudnn"
DOWNLOAD_PROCESS_NAME="wget"
SUCCESS_STR="NVIDIA INSTALL OK"
DOWNLOAD_SUCCESS_STR="Download OK"
DRIVER_FAIL_STR="Driver INSTALL FAIL"
CUDA_FAIL_STR="CUDA INSTALL FAIL"
CUDNN_FAIL_STR="CUDNN INSTALL FAIL"
DOWNLOAD_FAIL_STR="Download FAIL"
install_notes="The script automatically downloads and installs a NVIDIA GPU driver and CUDA/CUDNN Toolkit.
1. The installation takes 6 to 10 minutes, depending on the intranet bandwidth and the quantity of vCPU cores of the instance. Please do not operate the GPU or install any GPU-related software until the GPU driver is installed successfully.
2. After the GPU is installed successfully, the instance will restarts automatically."
check_install()
{
    b=''
    if [ "$1" = "NVIDIA" ]; then
        ProcessName=$DRIVER_PROCESS_NAME
        t=2
    elif [ "$1" = "cuda" ]; then
        ProcessName=$CUDA_PROCESS_NAME
        t=2.5
    elif [ "$1" = "cudnn" ]; then
        ProcessName=$CUDNN_PROCESS_NAME
        t=0.5
    fi
    i=0
    while true
    do
        pid_num=$(ps -ef | grep $ProcessName |grep -v grep | wc -l)
        if [ $pid_num -eq 0 ]; then
            str=$(printf "%-100s" "#")
            b=$(echo "$str" | sed 's/ /#/g')
            printf "| %-100s | %d%% \r\n" "$b" "100";
            break
        fi
        i=$(($i+1))
        str=$(printf "%-${i}s" "#")
        b=$(echo "$str" | sed 's/ /#/g')
        printf "| %-100s | %d%% \r" "$b" "$i";
        sleep $t
    done
    echo
    return 0
}
check_download()
{
    name=$1
    i=0
    b=''
    filesize=0
    percent=0
    sleep 0.5
    while true
    do
        pid_num=$(ps -ef | grep wget |grep $name |grep -v grep | wc -l)
        if [ $pid_num -eq 0 ]; then
            filesize=$(du -sk /root/nvidia/${name}* | awk '{print $1}')
            str=$(printf "%-100s" "#")
            b=$(echo "$str" | sed 's/ /#/g')
            printf "%-8s| %-100s | %d%% \r\n" "${filesize}K" "$b" "100";
            break
        fi
        line=$(tail -2 /root/nvidia/nvidia_install.log)
        filesize=$(echo $line | awk -F ' ' '{print $1}')
        percent=$(echo $line | awk -F '%' '{print $1}' | awk -F ' ' '{print $NF}')
        if [ "$percent" -ge 0 ] 2>/dev/null ;then
           str=$(printf "%-${percent}s" "#")
           b=$(echo "$str" | sed 's/ /#/g')
           printf "%-8s| %-100s | %d%% \r" "${filesize}" "$b" "$percent";
        else
            continue
        fi
        sleep 0.5
    done
    return 0
}
check_install_log()
{
    if [ ! -f "$log" ];then
        echo "NVIDIA install log $log not exist! Install may fail!"
        echo
        exit 1
    fi
    if [ "$1" = "NVIDIA" ]; then
        succstr=$SUCCESS_STR
        str2=$(cat $log |grep "INSTALL_ERROR")
        echo
        if [ -n "$succstr" ] && [ -z "$str2" ]; then
            echo "$succstr !!"
            echo
            return 0
        else
            echo "NVIDIA install may have some INSTALL_ERROR, please check log $log !"
            return 1
        fi
    fi
    if [ "$1" = "DRIVER" ]; then
        failstr=$DRIVER_FAIL_STR
    elif [ "$1" = "CUDA" ]; then
        failstr=$CUDA_FAIL_STR
    elif [ "$1" = "CUDNN" ]; then
        failstr=$CUDNN_FAIL_STR
    fi
    str1=$(cat $log |grep "$failstr")
    if [ -n "$str1" ] ;then
        echo
        echo "NVIDIA $failstr ! please check install log $log !"
        return 1
    fi
}
check_install_process()
{
    echo "CHECKING NVIDIA INSTALL, PLEASE WAIT ......"
    echo "$install_notes"
    echo
    while true
    do
        pid_num=$(ps -ef | grep $PROCESS_NAME |grep -v grep | grep -v check | wc -l)
        if [ $pid_num -eq 0 ];then
            check_install_log "NVIDIA"
            return 0
        else
            pid_num=$(ps -ef | grep $DOWNLOAD_PROCESS_NAME |grep driver |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo "Driver-${1} downloading, need 10 seconds. Remaining installation time 360 - 600 seconds!"
                check_download "NVIDIA" 
            fi
            pid_num=$(ps -ef | grep $DOWNLOAD_PROCESS_NAME |grep cuda |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo "CUDA-${2} downloading, need 150 or more seconds. Remaining installation time 350 - 590 seconds!"
                while true
                do
                    check_download "cuda" 
                    sleep 1
                    pid_num=$(ps -ef | grep $DOWNLOAD_PROCESS_NAME |grep cuda |grep -v grep | wc -l)
                    if [ $pid_num -eq 0 ];then
                        break
                    fi
                done
            fi
            pid_num=$(ps -ef | grep $DOWNLOAD_PROCESS_NAME |grep cudnn |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo "cuDNN-${3} downloading, need about 30 seconds. Remaining installation time 200 - 430 seconds!"
                check_download "cudnn"
            fi
            pid_num=$(ps -ef | grep $DRIVER_PROCESS_NAME |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo
                echo "Driver-${1} installing, need 30 - 160 seconds. Remaining installation time 160 - 400 seconds!"
                check_install "NVIDIA"
                check_install_log "DRIVER"
            fi
            pid_num=$(ps -ef | grep $CUDA_PROCESS_NAME |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo "CUDA-${2} installing, need 80 - 200 seconds. Remaining installation time 90 - 220 seconds!"
                check_install "cuda"
                check_install_log "CUDA"
            fi
            pid_num=$(ps -ef | grep $CUDNN_PROCESS_NAME |grep -v grep | wc -l)
            if [ $pid_num -gt 0 ];then
                echo "cuDNN-${3} installing, need 10 seconds. Installation will be successful soon, please wait......"
                check_install "cudnn"
                check_install_log "CUDNN"
            fi
        fi
        sleep 1
    done
}
create_nvidia_repo_centos()
{
    baseurl_centos=$(cat /etc/yum.repos.d/CentOS-Base.repo |grep baseurl | head -1 | awk -F'[/]' '{print $1"//"$3}')
    if [ -z "$baseurl_centos" ]; then
        url="http://mirrors.cloud.aliyuncs.com"
    fi
    cudaurl=$baseurl_centos"/opsx/ecs/linux/rpm/cuda/${version}/\$basearch/"
    driverurl=$baseurl_centos"/opsx/ecs/linux/rpm/driver/${version}/\$basearch/"
    echo "[ecs-cuda]" > /etc/yum.repos.d/nvidia.repo
    echo "name=ecs cuda - \$basearch" >> /etc/yum.repos.d/nvidia.repo
    echo $cudaurl >> /etc/yum.repos.d/nvidia.repo
    echo "enabled=1" >> /etc/yum.repos.d/nvidia.repo
    echo "gpgcheck=0" >> /etc/yum.repos.d/nvidia.repo
    echo "[ecs-driver]" >> /etc/yum.repos.d/nvidia.repo
    echo "name=ecs driver - \$basearch" >> /etc/yum.repos.d/nvidia.repo
    echo $driverurl >> /etc/yum.repos.d/nvidia.repo
    echo "enabled=1" >> /etc/yum.repos.d/nvidia.repo
    echo "gpgcheck=0" >> /etc/yum.repos.d/nvidia.repo
    yum clean all >> $log 2>&1
    yum makecache >> $log 2>&1
}
disable_nouveau_centos()
{
    echo "blacklist nouveau" > /etc/modprobe.d/blacklist-nouveau.conf
    echo "options nouveau modeset=0" >> /etc/modprobe.d/blacklist-nouveau.conf
    echo "***exec \"dracut --force\" to regenerate the kernel initramfs"
    dracut --force
}
disable_nouveau_ubuntu()
{
    echo "blacklist nouveau" > /etc/modprobe.d/blacklist-nouveau.conf 
    echo "options nouveau modeset=0" >> /etc/modprobe.d/blacklist-nouveau.conf
    echo "***exec \"update-initramfs -u\" to regenerate the kernel initramfs"
    update-initramfs -u
}
install_kernel_centos()
{
    kernel_version=$(uname -r)
    kernel_devel_num=$(rpm -qa | grep kernel-devel | grep $kernel_version | wc -l)
    if [ $kernel_devel_num -eq 0 ];then
        echo "******exec \"yum install -y kernel-devel-$kernel_version\""
        yum install -y kernel-devel-$kernel_version
        if [ $? -ne 0 ]; then
            echo "INSTALL_ERROR: install kernel-devel fail!!!"
            return 1
        fi
    fi
    return 0
}
install_kernel_suse()
{
    kernel_version=$(uname -r|awk -F'-' '{print $1"-"$2}')
    kernel_devel_num=$(rpm -qa | grep kernel-default-devel | wc -l)
    if [ $kernel_devel_num -eq 0 ];then
        echo "***exec \"zypper install -y kernel-default-devel=$kernel_version\""
        zypper install -y kernel-default-devel=$kernel_version
        if [ $? -ne 0 ]; then
            echo "error: install kernel-default-devel fail!!!"
            return 1
        fi
    fi
}
install_kernel_ubuntu()
{
    kernel_version=$(uname -r)
    linux_headers_num=$(dpkg --list |grep linux-headers | grep $kernel_version | wc -l)
    if [ $linux_headers_num -eq 0 ];then
        echo "***exec \"apt-get install -y --allow-unauthenticated linux-headers-$kernel_version\""
        apt-get install -y --allow-unauthenticated linux-headers-$kernel_version
        if [ $? -ne 0 ]; then
            echo "error: install linux-headers fail!!!"
            return 1
        fi
    fi
}
download()
{
    download_url="${baseurl}/opsx/ecs/linux/binary/nvidia"
    wget ${download_url}/driver/${driver_file}
    if [ $? -ne 0 ]; then
        echo "INSTALL_ERROR: Download driver fail!!! return: $?"
        return 1
    fi
    cudafilelist=$(curl ${download_url}/cuda/${cuda_version}/ |grep "cuda_${cuda_version}" | awk -F '>' '{print $2}' | awk -F '<' '{print $1}')
    if [ -z "$cudafilelist" ]; then
        echo "INSTALL_ERROR: Download CUDA fail!!! get cuda-${cuda_version} filename fail!!"
        return 1
    fi
    mkdir /root/nvidia/cuda
    cd /root/nvidia/cuda
    echo $cudafilelist
    for cudafile in $cudafilelist
    do
        sleep 1
        wget ${download_url}/cuda/${cuda_version}/$cudafile
        if [ $? -ne 0 ]; then
            echo "INSTALL_ERROR: Download CUDA fail!!! wget $cudafile fail! return: $?"
            return 1
        fi
    done
    chmod +x /root/nvidia/cuda/*
    cd /root/nvidia
    wget ${download_url}/cudnn/${cuda_big_version}/${cudnn_file}
    if [ $? -ne 0 ]; then
        echo "INSTALL_ERROR: Download cuDNN fail!!! return :$?"
        return 1
    fi
    chmod +x /root/nvidia/*
    echo "$DOWNLOAD_SUCCESS_STR !"
    return 0
}
install_driver()
{
    /root/nvidia/$driver_file --silent
    if [ $? -ne 0 ]; then
        echo "INSTALL_ERROR: driver install fail!!!"
        return 1
    fi
    echo "$DRIVER_SUCCESS_STR !"
    return 0
}
install_cuda()
{
    cd /root/nvidia/cuda
    cuda_file=$(ls -S | grep cuda | grep $cuda_version | head -1)
    echo "cuda file: "$cuda_file
    if [ -z "$cuda_file" ]
    then
        echo "INSTALL_ERROR: cuda file is null, cuda install fail!!!"
        return 1
    fi
    /root/nvidia/cuda/$cuda_file --silent --toolkit --samples --samplespath=/root
    if [ $? -ne 0 ]; then
        echo "INSTALL_ERROR: cuda install fail!!!"
        return 1
    fi
    cuda_patchfile=$(ls | grep cuda | grep $cuda_version | grep -v ${cuda_file})
    for cuda_patch in $cuda_patchfile
    do
        echo "install cuda patch file: "$cuda_patch
        /root/nvidia/cuda/$cuda_patch --silent --installdir=/usr/local/cuda --accept-eula
        if [ $? -ne 0 ]; then
            echo "INSTALL_ERROR: cuda patch install fail!!!"
            return 1
        fi
    done
    echo "$CUDA_SUCCESS_STR !"
    return 0
}
install_cudnn()
{
    tar zxvf /root/nvidia/$cudnn_file -C /usr/local
    if [ $? -ne 0 ]; then
        echo "INSTALL_ERROR: CUDNN INSTALL FAIL !!!"
        return 1
    fi
    echo "$CUDNN_SUCCESS_STR !"
    return 0
}
enable_pm()
{
    echo "#!/bin/bash" > /etc/init.d/enable_pm.sh
    echo "nvidia-smi -pm 1" >> /etc/init.d/enable_pm.sh
    echo "exit 0" >> /etc/init.d/enable_pm.sh
    chmod +x /etc/init.d/enable_pm.sh
    str=$(tail -1 $filename |grep "exit")
    if [ -z "$str" ]; then
        echo "/etc/init.d/enable_pm.sh" >> $filename
    else
        sed -i '$i\/etc/init.d/enable_pm.sh' $filename
    fi
    chmod +x $filename
}
issue=$(cat /etc/issue | grep Ubuntu)
if [ -n "$issue" ];then
    os="ubuntu"
    profile_file="/root/.profile"
    filename="/etc/rc.local"

else
    issue=$(cat /etc/issue | grep SUSE)
    if [ -n "$issue" ];then
        os="suse"
        filename="/etc/init.d/after.local"
    else
        os="centos"
        filename="/etc/rc.d/rc.local"
    fi
    profile_file="/root/.bash_profile"
fi
if [ "$1" = "check" ];then
    check_install_process $driver_version $cuda_version $cudnn_version
    sed -i '/part-001 /d' $profile_file
    exit 0
else
    mkdir $NVIDIA_DIR
    echo "begin to install, driver: $driver_version, cuda: $cuda_version, cudnn: $cudnn_version " >> $log 2>&1
    driver_file="NVIDIA-Linux-x86_64-"${driver_version}".run"
    cuda_big_version=$(echo $cuda_version | awk -F'.' '{print $1"."$2}')
    cudnn_file="cudnn-"${cuda_big_version}"-linux-x64-v"${cudnn_version}".tgz"
    echo "sh /var/lib/cloud/instance/scripts/part-001 check" | tee -a $profile_file
fi
echo "os:$os" >> $log 2>&1
if [ "$os" = "ubuntu" ]; then
    disable_nouveau_ubuntu >> $log 2>&1
    if [ -f "/etc/apt/sources.list.d/sources-aliyun-0.list" ]; then
        repo_file="/etc/apt/sources.list.d/sources-aliyun-0.list"
    else
        repo_file="/etc/apt/sources.list"
    fi
    baseurl=$(cat $repo_file |grep "^deb" | head -1 | awk -F'[/]' '{print $1"//"$3}' |awk -F ' ' '{print $2}')
    if [ -z "$baseurl" ]; then
        baseurl="http://mirrors.cloud.aliyuncs.com"
    fi
elif [ "$os" = "suse" ]; then
    baseurl=$(cat /etc/zypp/repos.d/SLES12-SP2-0.repo |grep baseurl | head -1| awk -F'[=/]' '{print $2"//"$4}')
    if [ -z "$baseurl" ]; then
        baseurl="http://mirrors.cloud.aliyuncs.com"
    fi
elif [ "$os" = "centos" ]; then
    baseurl=$(cat /etc/yum.repos.d/CentOS-Base.repo |grep baseurl | head -1 | awk -F'[/]' '{print $1"//"$3}' |awk -F '=' '{print $2}')
    if [ -z "$url" ]; then
        baseurl="http://mirrors.cloud.aliyuncs.com"
    fi
    if [ ! -f "/usr/bin/lsb_release" ]; then
       pkgname=$(yum provides /usr/bin/lsb_release |grep centos|grep x86_64 |head -1 |awk -F: '{print $1}')
       if [ -z "$pkgname" ]; then
           echo "INSTALL_ERROR: /usr/bin/lsb_release pkg not exists!" >> $log 2>&1
           exit 1
       fi
       yum install -y $pkgname >> $log 2>&1
    fi
    if [ ! -f "/usr/bin/gcc" ]; then
        yum install -y gcc
    fi
    disable_nouveau_centos >> $log 2>&1
    str=$(lsb_release -r | awk -F'[:.]' '{print $2}')
    version=$(echo $str | sed 's/ //g')
    create_nvidia_repo_centos
fi
install_kernel_${os} >> $log 2>&1
if [ $? -ne 0 ]; then
    echo "INSTALL_ERROR: kernel-devel install fail!!!" >> $log 2>&1
    exit 1
fi
cd /root/nvidia
begin_download=$(date '+%s')
download >> $log 2>&1
if [ $? -ne 0 ]; then
    exit 1
fi
end_download=$(date '+%s')
time_download=$((end_download-begin_download))
echo "NVIDIA download OK! Using time $time_download s !!" >> $log 2>&1
begin=$(date '+%s')
install_driver >> $log 2>&1
if [ $? -ne 0 ]; then
    exit 1
fi
end=$(date '+%s')
time_install=$((end-begin))
echo "NVIDIA install driver OK! Using time $time_install s !!" >> $log 2>&1
begin=$(date '+%s')
install_cuda >> $log 2>&1
if [ $? -ne 0 ]; then
    exit 1
fi
end=$(date '+%s')
time_install=$((end-begin))
echo "NVIDIA install cuda OK! Using time $time_install s !!"  >> $log 2>&1
begin=$(date '+%s')
install_cudnn >> $log 2>&1
if [ $? -ne 0 ]; then
    exit 1
fi
end=$(date '+%s')
time_install=$((end-begin))
echo "NVIDIA install cudnn OK! Using time $time_install s !!" >> $log 2>&1
enable_pm
echo "reboot......" >> $log 2>&1
sleep 2
reboot
```

## What to do next {#section_o3f_dch_ygb .section}

-   If you do not configure automatic installation of the GPU driver when you create the GPU instance, you must install it manually. For more information, see [Install the GPU driver](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Install the GPU driver.md#).
-   If the selected gn5, gn5i, gn6v, vgn5i, or gn6i type instance need to support OpenGL, you must install the GRID driver. For more information, see [Install the GRID driver on a gn5/gn5i/gn6v instance](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Install a GRID driver in a GPU-equipped ECS instance (Linux).md#).
-   You can uninstall the GPU driver and the CUDA Toolkit. For more information, see [Uninstall the GPU driver](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Uninstall the GPU driver.md#).
-   You can view GPU monitoring data by using the CloudMonitor console or call the API. For more information, see [GPU monitoring](../../../../reseller.en-US/User Guide/Host monitoring/GPU monitoring.md#).

