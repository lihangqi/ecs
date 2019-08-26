# f1实例OpenCL开发最佳实践 {#concept_61410_zh .concept}

本文介绍如何在f1实例上使用OpenCL（Open Computing Language）制作镜像文件，并烧写到FPGA芯片中。

**说明：** 

-   本文所述所有操作都必须由同一个账号在同一地域里执行。
-   强烈建议您使用RAM用户操作FaaS实例。为了防止意外操作，您需要让RAM用户仅执行必要的操作。在操作FPGA镜像及下载时，因为您需要从指定的OSS Bucket下载原始DCP工程，所以您必须为FaaS管理账号创建一个角色，并授予临时权限，让FaaS管理账号访问指定的OSS Bucket。如果需要对IP加密，必须授予RAM用户KMS相关权限。如果需要做权限检查，必须授予查看用户资源的权限。

## 前提条件 {#section_b44_gr3_dfb .section}

-   创建f1实例，确认实例能访问公网，并且实例所在安全组中已经添加规则放行SSH（22）端口的访问。

    **说明：** f1实例只能使用镜像市场的FaaS F1基础镜像。详细信息，请参见 [创建f1实例](../../../../intl.zh-CN/用户指南/实例/创建实例/创建f1实例.md)。

-   您已经在 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home) f1实例的详情页上获取实例ID。
-   您必须先开通OSS服务，并 [创建一个OSS Bucket](../../../../intl.zh-CN/快速入门/创建存储空间.md) 用于上传您的文件。Bucket与f1实例必须属于同一个账号、同一个地域。
-   如果需要加密文件，开通密钥管理服务（KMS）。
-   使用RAM用户操作FPGA，必须完成以下操作：
    -    [创建RAM用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md) 并 [授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md)。
    -    [创建RAM角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md) 并 [授权](../../../../intl.zh-CN/用户指南/授权管理/授权.md)。
    -   获取AccessKey ID和AccessKey Secret。

## 操作步骤 { .section}

按以下步骤在f1实例上使用OpenCL Example制作镜像文件，并烧写到FPGA芯片中。

## 第 1 步. 远程连接实例 { .section}

 [远程连接Linux实例](../../../../intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md)。

## 第 2 步. 安装基础环境 { .section}

运行以下脚本安装基础环境。

```language-shell
source /opt/dcp1_1/script/f1_env_set.sh

```

## 第 3 步. 下载官方的OpenCL Example { .section}

按以下步骤下载官方的OpenCL Example。

1.  创建并切换到/opt/tmp目录。

    ```language-shell
    mkdir -p /opt/tmp
    cd /opt/tmp
    
    ```

    此时，您在/opt/tmp目录下。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/154149218411994_zh-CN.png)

2.  依次执行以下命令下载并解压Example文件。

    ```language-shell
    wget https://www.altera.com/content/dam/altera-www/global/en_US/others/support/examples/download/exm_opencl_matrix_mult_x64_linux.tgz
    tar -zxvf exm_opencl_matrix_mult_x64_linux.tgz
    
    ```

    解压后的目录如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/154149218411995_zh-CN.png)

3.  进入matrix\_mult目录下，执行编译命令。

    ```language-shell
    cd matrix_mult
    aoc -v -g --report ./device/matrix_mult.cl
    
    ```

    编译过程可能会持续数个小时，您可以再开一个会话，使用 `top` 命令监控系统占用，确定编译状态。


## 第 4 步. 上传配置文件 { .section}

按以下步骤上传配置文件。

1.  运行以下命令初始化faascmd。

    ```language-shell
    # 如果需要，要添加环境变量及运行权限
    export PATH=$PATH:/opt/dcp1_1/script/
    chmod +x /opt/dcp1_1/script/faascmd
    # 将hereIsYourSecretId换为您的AccessKey ID，hereIsYourSecretKey替换为您的AccessKey Secret
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey
    # 将hereIsYourBucket换为华东1OSS的Bucket名称
    faascmd auth --bucket=hereIsYourBucket
    
    ```

2.  进入matrix\_mult/output\_files，上传配置文件。

    ```language-shell
    cd matrix_mult/output_files # 此时您应该在/opt/tmp/matrix_mult/matrix_mult/output_files
    faascmd upload_object --object=afu_fit.gbs --file=afu_fit.gbs
    
    ```

3.  使用gbs制作FPGA镜像。

    ```language-shell
    # 将hereIsYourImageName换为您的镜象名，将hereIsYourImageTag替换为您的镜像标签
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=hereIsYourImageName --tags=hereIsYourImageTag --encrypted=false --shell=V1.1  
    
    ```

4.  查看镜像是否制作成功：运行命令`faascmd list_images`。 返回结果里，如果显示 `"State":"success"`，表示镜像制作成功。请记录返回结果里显示的**FpgaImageUUID**，稍后会用到。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/154149218511996_zh-CN.png)


## 第 5 步. 下载镜像到f1实例 { .section}

按以下步骤将镜像下载到f1实例。

1.  运行命令获取FPGA ID。

    ```language-shell
    # 将hereIsYourInstanceId替换为您的FPGA实例ID
    faascmd list_instances --instanceId=hereIsYourInstanceId
    
    ```

    以下为返回结果。请记录FpgaUUID。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/154149218511997_zh-CN.png)

2.  运行命令下载镜像到f1实例。

    ```language-shell
    # 将hereIsYourInstanceID替换为刚刚保存的实例ID；将hereIsFpgaUUID替换为上一条命令中记下的FpgaUUID；将hereIsImageUUID替换为上一步记下的FpgaImageUUID
    faascmd download_image  --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID --fpgatype=intel --imageuuid=hereIsImageUUID --imagetype=afu --shell=V0.11
    
    ```

3.  运行命令检查是否下载成功。

    ```language-shell
    # 将hereIsYourInstanceID替换为刚刚保存的实例ID；将hereIsFpgaUUID替换为上一条命令中记下的FpgaUUID；
    faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceID
    
    ```

    如果返回结果里显示\`"TaskStatus":"operating"\`，说明下载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/154149218511998_zh-CN.png)


## 第 6 步. 将FPGA镜像烧录到FPGA芯片 { .section}

按以下步骤将FPGA镜像烧录到FPGA芯片。

1.  打开第2步环境的窗口。如果已关闭，重新执行第2步操作。
2.  运行命令配置OpenCL的运行环境。

    ```language-shell
    sh /opt/dcp1_1/opencl/opencl_bsp/linux64/libexec/setup_permissions.sh
    
    ```

3.  返回上级目录。

    ```language-shell
    cd ../.. # 此时您在/opt/tmp/matrix_mult
    
    ```

4.  执行编译命令。

    ```language-shell
    make
    # 输出环境配置
    export CL_CONTEXT_COMPILER_MODE_ALTERA=3
    cp matrix_mult.aocx ./bin/matrix_mult.aocx
    cd bin
    host matrix_mult.aocx
    
    ```

    当您看到如下输出时，说明配置完成。请注意，最后一行必须为`Verification: PASS`。

    ```language-shell
    [root@iZbpXXXXXZ bin]# ./host matrix_mult.aocx
    Matrix sizes:
      A: 2048 x 1024
      B: 1024 x 1024
      C: 2048 x 1024
    Initializing OpenCL
    Platform: Intel(R) FPGA SDK for OpenCL(TM)
    Using 1 device(s)
      skx_fpga_dcp_ddr : SKX DCP FPGA OpenCL BSP (acl0)
    Using AOCX: matrix_mult.aocx
    Generating input matrices
    Launching for device 0 (global size: 1024, 2048)
    Time: 40.415 ms
    Kernel time (device 0): 40.355 ms
    Throughput: 106.27 GFLOPS
    Computing reference output
    Verifying
    Verification: PASS
    
    ```


