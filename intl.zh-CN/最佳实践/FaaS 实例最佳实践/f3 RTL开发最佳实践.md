# f3 RTL开发最佳实践 {#concept_71547_zh .concept}

本文描述基于f3的RTL（Register Transfer Level）开发流程。

**说明：** 

-   本文所述所有操作必须由同一个账号在同一个地域执行。
-   强烈建议您使用RAM用户操作FPGA实例。为了防止意外操作，您需要让RAM用户仅执行必要的操作。在操作及下载FPGA镜像时，因为您需要从指定的OSS存储空间下载原始DCP工程，所以您需要为FaaS账号创建一个角色，并授予临时权限，让FaaS管理账号可以访问指定的OSS存储空间。如果需要对IP加密，必须授予RAM用户KMS相关的权限。如果需要做权限检查，必须授予查看用户资源的权限。

## 前提条件 {#section_agy_vy3_dfb .section}

-   您已经 [创建f3实例](../../../../intl.zh-CN/用户指南/实例/创建实例/创建f3实例.md)，实例能访问公网，并且实例所在安全组中已经添加规则放行SSH（22）端口的访问。
-   登录 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)，在f3实例的详情页上，获取实例ID。
-   在华东2 [创建一个OSS Bucket](../../../../intl.zh-CN/快速入门/创建存储空间.md)，专门用于FaaS服务。

    **说明：** 这个Bucket会对FaaS管理账号开通读写权限，因此不建议您存储与FaaS无关的内容。

-   如果使用RAM用户操作FPGA，必须完成以下操作：
    -    [创建RAM用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md) 并 [授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md)。
    -    [创建RAM角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md) 并 [授权](../../../../intl.zh-CN/用户指南/授权管理/授权.md)。
    -   获取AccessKey ID和AccessKey Secret。

## 操作步骤 { .section}

1.   [远程连接Linux实例](../../../../intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md)。

    **说明：** 编译工程时需要 2 ~ 3 小时。建议您使用nohup或者VNC连接实例，以免编译时意外退出。

2.  下载 [RTL参考设计](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/f30002/f30002.tar.gz)。
3.  解压文件。
4.  运行以下脚本配置f3环境。

    ```language-bash
    source /root/xbinst_oem/F3_env_setup.sh xdma
    
    ```

    **说明：** 每打开一个terminal窗口都需要运行此命令。

5.  指定OSS存储空间。

    ```language-bash
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey #将hereIsYourSecretId和hereIsYourSecretKey替换为您的RAM用户AK信息
    faascmd auth --bucket=hereIsYourBucket # 将hereIsYourBucket替换为您创建的OSS Bucket名称
    
    ```

6.  运行以下命令编译RTL工程。

    ```language-bash
    cd <您之前解压的路径>/hw/ # 进入解压后的hw路径
    sh compiling.sh
    
    ```

    **说明：** 编译工程需要2 ~ 3小时。

7.  上传网表文件，并下载FPGA镜像。您可以采用脚本化流程或者单步操作流程完成该步骤。
    -   脚本化流程：仅适用于配备单块FPGA卡的f3实例。

        1.  运行以下命令上传并生成镜像文件。

            ```
            sh /root/xbinst_oem/tool/faas_upload_and_create_image.sh <bit.tar.gz需要上传的压缩包文件名>
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712110_zh-CN.png)

        2.  下载镜像文件。

            ```
            
            sh /root/xbinst_oem/tool/faas_download_image.sh  0 # 最后的数字为实例中fpga的序号
            ```

            0为FaaS实例中的第一个FPGA，单芯片实例序号一律为0，对多芯片实例，例如4芯片的序号为0,1,2,3。

            如果需要对多个FPGA下载同一个镜像，可以在末尾添加序号，例如：

            ```
            sh faas_download_image.sh bit.tar.gz 0 1 2
            
            ```

    -   单步操作流程：
        1.  运行以下命令，将压缩包上传到您个人的OSS Bucket，再将存放在您个人OSS Bucket中的gbs上传到FaaS管理单元的OSS Bucket中。

            ```language-bash
            faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
            faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=f30001
            
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712112_zh-CN.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712113_zh-CN.png)

        2.  运行命令查看FPGA镜像是否处于可下载状态。

            ```
            faascmd list_images
            ```

            在返回结果中，如果看到 `"State":"success"`，表示FPGA镜像已经可以下载。找到并记录FpgaImageUUID。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712115_zh-CN.png)

        3.  运行以下命令，在返回结果中，找到并记录FpgaUUID。

            ```
            faascmd list_instances --instanceId=hereIsYourInstanceId # 将hereIsYourInstanceId替换为f3实例ID
            ```

        4.  运行以下命令下载FPGA镜像。

            ```
            
            faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=f30001
            # hereIsYourInstanceId替换为f3的实例ID，hereIsFpgaUUID替换为您获取的FpgaUUID，hereIsImageUUID替换为您获取的FpgaImageUUID
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712116_zh-CN.png)

        5.  运行以下命令查看镜像是否下载成功。

            ```
            faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceId # hereIsFpgaUUID替换为您获取的FpgaUUID，hereIsYourInstanceId替换为f3实例ID。
            ```

            以下为返回结果示例。如果显示的FpgaImageUUID与您获取的FpgaImageUUID一致，并且显示 `"TaskStatus":"valid"`，说明镜像下载成功。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154045394712117_zh-CN.png)


## FAQ { .section}

**上传镜像时出现异常，如何查看异常详情？**

如果您的工程在上传生成镜像的过程中出现异常，例如云上编译服务器编译报错，你可以通过以下两种方式来查看异常详情：

-   查看faas\_compiling.log。使用上传脚本faas\_upload\_and\_create\_image.sh时，如果编译失败会自动下载并打印faas\_compiling.log到terminal中。
-   手动执行命令查看编译log文件：`sh /root/xbinst_oem/tool/faas_checklog.sh <bit.tar.gz之前上传的压缩包文件名>` 

**如何重新加载镜像？**

您可以参考以下步骤重新加载镜像：

1.  在实例中运行以下命令卸载驱动。

    ```
    sudo rmmod xdma
    sudo rmmod xocl
    
    ```

2.  下载镜像。可以使用以下两种方式之一：
    -   使用脚本，最后的数字为实例中FPGA的序号：`sh faas_download_image.sh bit.tar.gz 0` 
    -   使用faascmd：`faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=f30001` 
3.  安装驱动。

    ```
    sudo depmod
    sudo modprobe xdma
    
    ```


