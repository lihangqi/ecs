# 使用f1 RTL {#concept_n5c_vt3_dfb .concept}

本文描述如何使用f1 RTL（Register Transfer Level）。

**说明：** 

-   本文所述所有操作都必须由同一个账号在同一地域里执行。
-   强烈建议您使用RAM用户操作FaaS实例。为了防止意外操作，您需要让RAM用户仅执行必要的操作。在操作FPGA镜像及下载时，因为您需要从指定的OSS Bucket下载原始DCP工程，所以您必须为FaaS管理账号创建一个角色，并授予临时权限，让FaaS管理账号访问指定的OSS Bucket。如果需要对IP加密，必须授予RAM用户KMS相关权限。如果需要做权限检查，必须授予查看用户资源的权限。

## 前提条件 {#section_il5_153_dfb .section}

-   创建f1实例，确保实例能访问公网，并且实例所在安全组中已经添加规则放行SSH（22）端口的访问。

    **说明：** f1实例只能使用镜像市场的FaaS F1基础镜像。详细信息，请参见 [创建f1实例](../../../../intl.zh-CN/用户指南/实例/创建实例/创建f1实例.md)。

-   您已经在 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home) f1实例的详情页上获取实例ID。
-   您必须先开通OSS服务，并 [创建一个OSS Bucket](../../../../intl.zh-CN/快速入门/创建存储空间.md) 用于上传您的文件。Bucket与f1实例必须属于同一个账号、同一个地域。
-   如果需要加密服务，您还需要 [开通密钥管理服务（KMS）](../../../../intl.zh-CN/快速入门/使用步骤.md#)。
-   使用RAM用户操作FPGA，必须完成以下操作：
    -    [创建RAM用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md) 并 [授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md)。
    -    [创建RAM角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md) 并 [授权](../../../../intl.zh-CN/用户指南/授权管理/授权.md)。
    -   获取AccessKey ID和AccessKey Secret。

## 操作步骤 {#section_i5l_453_dfb .section}

按以下步骤使用f1 RTL。

## 第 1 步. 远程连接f1实例 {#section_ccx_f53_dfb .section}

[远程连接Linux实例](../../../../intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md)。

## 第 2 步. 配置基础环境 {#section_dcx_f53_dfb .section}

运行以下脚本配置基础环境。

```
source /opt/dcp1_1/script/f1_env_set.sh
```

## 第 3 步. 编译工程 {#section_fcx_f53_dfb .section}

运行以下命令：

```
cd /opt/dcp1_1/hw/samples/dma_afu
afu_synth_setup --source hw/rtl/filelist.txt build_synth
cd build_synth/
run.sh
```

**说明：** 编译时间较长，请耐心等待。

## 第 4 步. 制作镜像 {#section_hcx_f53_dfb .section}

按以下步骤制作镜像：

1.  运行命令初始化 `faascmd`。

    ```
    #如果需要，添加环境变量及运行权限
    export PATH=$PATH:/opt/dcp1_1/script/
    chmod +x /opt/dcp1_1/script/faascmd
    # 将hereIsYourSecretId替换为您的AccessKey ID，hereIsYourSecretKey替换为您的AccessKey Secret
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey
    # 将hereIsYourBucket换为华东1地域里OSS Bucket名称
    faascmd auth --bucket=hereIsYourBucket
    ```

2.  确认在/opt/dcp1\_1/hw/samples/dma\_afu目录下，运行以下命令上传gbs文件。

    ```
    faascmd upload_object --object=dma_afu.gbs --file=dma_afu.gbs
    ```

3.  运行以下命令制作镜像。

    ```
    # 将hereIsYourImageName替换为您的镜像名称
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=hereIsYourImageName --tags=hereIsYourImageTag --encrypted=false --shell=V1.1
    ```


## 第 5 步. 下载镜像 {#section_ocx_f53_dfb .section}

按以下步骤下载镜像到f1实例：

1.  查看镜像是否制作成功：运行命令 `faascmd list_images`。

    返回结果里，如果出现`"State":"success"`，表示镜像制作成功。请记录返回结果里显示的**FpgaImageUUID**，稍后会用到。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/154149206412086_zh-CN.png)

2.  运行命令获取FPGA ID。

    ```
    # 将hereIsYourInstanceId替换为您的f1实例ID
    faascmd list_instances --instanceId=hereIsYourInstanceId
    ```

    以下为返回结果。请记录FpgaUUID。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/154149206412087_zh-CN.png)

3.  运行命令下载FPGA镜像到f1实例。

    ```
    # 将hereIsYourInstanceID替换为刚刚保存的实例ID；将hereIsFpgaUUID替换为上一条命令中记下的FpgaUUID；将hereIsImageUUID替换为上一步记下FpgaImageUUID
    faascmd download_image --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID --fpgatype=intel --imageuuid=hereIsImageUUID --imagetype=afu --shell=V0.11
    ```

4.  运行命令检查是否下载成功。

    ```
    # 将hereIsYourInstanceID替换为刚刚保存的实例ID；将hereIsFpgaUUID替换为上一条命令中记下的FpgaUUID；
    faascmd fpga_status --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID
    ```

    如果返回结果里出现`"TaskStatus":"operating"`时，且FpgaImageUUID和下载镜像时的FpgaImageUUID一致，说明下载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/154149206412088_zh-CN.png)


## 第 6 步. 测试 {#section_xcx_f53_dfb .section}

依次运行以下命令。

```
cd /opt/dcp1_1/hw/samples/dma_afu/sw
make
sudo LD_LIBRARY_PATH=/opt/dcp1_1/hw/samples/dma_afu/sw:$LD_LIBRARY_PATH ./fpga_dma_test 0
```

如果您看到如图所示的输出结果，说明测试完成。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/154149206412089_zh-CN.png)

**说明：** 如果没有开启Huge pages，运行以下命令启用Huge pages。

```
sudo bash -c "echo 20 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages"
```

