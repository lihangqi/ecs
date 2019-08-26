# f2实例OpenCL开发最佳实践 {#concept_62781_zh .concept}

本文介绍如何在f2实例上使用OpenCL（Open Computing Language）制作镜像文件，并烧写到FPGA芯片中。

**说明：** 

-   本文所述所有操作都必须由同一个账号在同一地域里执行。
-   强烈建议您使用RAM用户操作FaaS实例。为了防止意外操作，您需要让RAM用户仅执行必要的操作。您需要为FaaS管理账号创建一个角色，并授予临时权限，让FaaS管理账号能访问指定的OSS Bucket。

## 前提条件 {#section_nvh_dw3_dfb .section}

-   创建f2实例，确保实例能访问公网，并且实例所在安全组中已经添加规则放行SSH（22）端口的访问。

    **说明：** f2实例只能使用镜像市场的FaaS F2基础镜像。详细信息，请参见 [创建f2实例](../../../../intl.zh-CN/用户指南/实例/创建实例/创建f2实例.md)。

-   登录 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)，在f2实例的详情页上，获取实例ID。
-   开通OSS服务，并 [创建一个OSS Bucket](../../../../intl.zh-CN/快速入门/创建存储空间.md)。Bucket与f2实例必须属于同一个账号、同一个地域。
-   使用RAM用户操作FPGA，必须完成以下操作：
    -    [创建RAM用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md) 并 [授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md)。
    -    [创建RAM角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md) 并 [授权](../../../../intl.zh-CN/用户指南/授权管理/授权.md)。
    -   获取AccessKey ID和AccessKey Secret。

## 操作步骤 { .section}

按以下步骤在f2实例上使用OpenCL制作镜像文件，并烧写到FPGA芯片中。

## 步骤 1. 配置环境 { .section}

按以下步骤配置环境：

1.   [远程连接f2实例](../../../../intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md)。
2.  使用 `vim` 修改/root/xbinst\_oem/setup.sh：在第5行前加一个 `#`，注释掉 `unset XILINX_SDX`，再保存退出。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764212093_zh-CN.png)

3.  运行以下命令安装Screen，用于后续的持续链接。

    ```language-shell
    yum install screen -y
    
    ```

4.  运行以下命令进入Screen。

    ```language-shell
    screen -S f2opencl
    
    ```

5.  运行以下命令配置安全烧写环境。

    ```language-shell
    source /root/xbinst_oem/F2_env_setup.sh
    
    ```


## 步骤 2. 编译二进制文件 { .section}

按以下步骤编译二进制文件：

1.  进入命令目录 。

    ```language-shell
    cd /opt/Xilinx/SDx/2017.2/examples/vadd
    
    ```

2.  运行命令 `cat sdaccel.mk | grep "XDEVICE"`，查看 `XDEVICE` 配置是否为 `xilinx:aliyun-ku115-f2:4ddr-xpr:4.2`。如果不是，必须改为这个配置。
3.  使用 `vim` 修改 `common.mk` 文件。

    ```language-shell
    vim ../common/common.mk
    
    ```

    将第 63 行代码（参数可能在 60-62 行，由您的文件确定）

    ```language-shell
    CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} -o ${XCLBIN} ${KERNEL_DEFS} ${KERNEL_INCS}
    
    ```

    修改为

    ```language-shell
    CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} -o ${XCLBIN} ${KERNEL_DEFS} ${KERNEL_INCS} --xp param:compiler.acceleratorBinaryContent=dcp
    
    ```

    **说明：** 您必须向编译服务器提交DCP文件，而不是bit文件，所以必须添加编译参数 `--xp param:compiler.acceleratorBinaryContent=dcp`，使Xilinx® OpenCL™ Compiler（xocc）编译生成一个布局布线后的DCP文件，而不是bit文件。

4.  运行以下命令编译程序。

    ```language-shell
    export XILINX_SDX=/opt/Xilinx/SDx/2017.2
    make -f sdaccel.mk xbin_hw
    
    ```

    如果您看到如下界面，说明二进制文件编译已经开始。编译过程可能会持续数个小时，请您耐心等待。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764212094_zh-CN.png)


## 步骤 3. 检查打包脚本 { .section}

运行以下命令检查打包脚本是否存在。

```language-shell
file /root/xbinst_oem/sdaccel_package.sh

```

**说明：** 如果返回结果中包含 `cannot open (No such file or directory)`，说明不存在该文件，您需要手动下载打包脚本。

```language-shell
wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/sdaccel_package.sh

```

## 步骤 4. 制作镜像 { .section}

按以下步骤制作镜像文件。

1.  运行命令配置OSS环境。

    ```language-shell
    # 将此处的hereIsMySecretId、hereIsMySecretKey、hereIsMyBucket分别替换为您的AccessKeyID、AccessKeySecret和Bucket名称
    faascmd config --id=hereIsMySecretId --key=hereIsMySecretKey 
    faascmd auth --bucket=hereIsMyBucket
    
    ```

2.  运行 `ls`，获取文件名。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764212095_zh-CN.png)

3.  打包二进制文件。

    ```language-shell
    /root/xbinst_oem/sdaccel_package.sh -xclbin=/opt/Xilinx/SDx/2017.2/examples/vadd/bin_vadd_hw.xclbin
    
    ```

    打包完成后，在同一目录下，您会看到一个打包好的文件，如本示例中的 `17_10_28-021904_SDAccel_Kernel.tar.gz`。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312096_zh-CN.png)

4.  运行命令将打包好的文件上传到您指定的OSS Bucket中。

    ```language-shell
    # 将文件名改为打包好的文件名，您需要根据您的 ls 命令修改
    faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
    
    ```

5.  运行如下命令制作镜像。

    ```language-shell
    # bit.tar.gz、hereIsFPGAImageName、hereIsFPGAImageTag分别替换为刚创建的压缩包文件名、镜像名和镜像的tag
    faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=20171121
    
    ```

    返回结果示例如下图所示。如果出现 `"State":"queued"`，说明这个任务已经加入队列，开始制作镜像。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312097_zh-CN.png)

    **说明：** 制作镜像比较耗时。等待一段时间后，运行以下命令，查看镜像状态。

    ```language-shell
    faascmd list_images
    
    ```

    返回结果里，如果出现 `"State":"success"`，说明镜制作成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312098_zh-CN.png)

    记录返回结果中的FPGAImageUUID。


## 步骤 5. 烧写镜像 { .section}

按以下步骤将镜像烧写入FPGA芯片。

1.  运行以下命令获取FpgaUUID。

    ```language-shell
    # 将hereIsYourInstanceId替换为你的FPGA云服务器的实例ID 
    faascmd list_instances --instanceId=hereIsYourInstanceId
    
    ```

    返回结果如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312099_zh-CN.png)

    **说明：** 记录返回结果中的FpgaUUID。

2.  运行以下命令下载镜像。

    ```language-shell
    # 将hereIsYourInstanceID替换为这个f2实例的ID，将hereIsFpgaUUID替换为您记录的FpgaUUID，将hereIsImageUUID替换为您记录的FpgaImageUUID
    faascmd download_image  --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=20171121
    
    ```

    在返回结果里，如果看到 `"State":"committed"`，说明镜像下载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312100_zh-CN.png)

    **说明：** 您也可以运行以下命令查看镜像是否下载成功。

    ```language-shell
    # 将 hereIsYourInstanceID 替换为这个 f2 实例的 ID，将 hereIsFpgaUUID 替换为您记录的 FpgaUUID
    faascmd fpga_status  --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID
    
    ```

    返回结果里，如果看到 `"TaskStatus":"valid"`，而且FpgaImageUUID和下载镜像时的FpgaImageUUID一致，说明镜像下载正常。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/154045764312102_zh-CN.png)


## 步骤 6. 运行Host程序 { .section}

执行以下命令运行Host程序。

```language-shell
make -f sdaccel.mk host
unset XILINX_SDX
./vadd bin_vadd_hw.xclbin

```

如果返回结果中出现 `Test Passed`，说明测试通过。

## 其他操作 { .section}

这里介绍 FPGA 实例部分常用的操作。

|任务|命令|
|:-|:-|
|查看帮助文档| `make -f ./sdaccel.mk help` |
|软件仿真| `make -f ./sdaccel.mk run_cpu_em` |
|硬件仿真| `make -f ./sdaccel.mk run_hw_em` |
|只编译 host 代码| `make -f ./sdaccel.mk host` |
|编译生成可以下载的文件| `make -f sdaccel.mk xbin_hw` |
|清理工作目录| `make -f sdaccel.mk clean` |
|强力清除工作目录| `make -f sdaccel.mk cleanall` |

**说明：** 

-   sdx2017.2在仿真时，device需要用xilinx\_aliyun-ku115-f2\_4ddr-xpr\_4\_2。
-   仿真时只需要按照Xilinx标准流程操作，不需要配置F2\_env\_setup环境。

