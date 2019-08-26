# 使用faascmd {#concept_vrl_rn1_tfb .concept}

您可以通过本主题了解faascmd命令的用法。

## 前提条件 {#section_v5y_n51_tfb .section}

使用faascmd工具之前，您需要先 [配置faascmd](intl.zh-CN/最佳实践/FaaS 实例最佳实践/faascmd工具/配置faascmd.md#) 。

## 语法说明 {#section_k5j_b2v_vfb .section}

-   faascmd工具提供的所有命令和参数都严格区分大小写。

-   faascmd命令中各参数“=”前后不能有多余空格。


## 授权 {#section_wgv_4f5_tfb .section}

`faascmd auth` 命令用于授权faas admin访问用户的OSS bucket。

**前提条件**

1.  为FaaS新建一个OSSbucket，用于上传原始编译的DCP文件。

2.  在该FaaSOSSbucket中，新建一个名为compiling\_logs的文件夹。


**命令格式**

```
faascmd auth --bucket=<yourFaasOSSBucketName>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726031129_zh-CN.png)

**说明：** 如果同一主账户下有多个子账户，建议子账户间共享一个OSS bucket，以避免重复修改或覆盖授权策略。

## 查看授权策略 {#section_xbt_srr_5fb .section}

`faascmd list_policy` 命令用来查看指定的OSS bucket是否已添加到相应的授权策略（faasPolicy）里。

**命令格式**

```
faascmd list_policy
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726031130_zh-CN.png)

**说明：** 请关注您的OSS Bucket和OSS Bucket/compiling\_logs是否出现在列出的策略信息中。

## 删除授权策略 {#section_pnl_xrr_5fb .section}

`faascmd delete_policy` 命令用于删除授权策略（faasPolicy）。

**命令格式**

```
faascmd delete_policy
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131131_zh-CN.png)

**说明：** 如果同一主账户下有多个子账户，建议您去RAM控制台操作，以避免误删授权策略。

## 查看OSS Bucket下所有的objects {#section_t1s_1sr_5fb .section}

`faascmd list_objects` 命令用于查看用户OSS Bucket下所有的objects。

**命令格式**

```
faascmd list_objects
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131132_zh-CN.png)

**说明：** 您可以配合grep命令筛选出您想要的文件。例如: `faascmd list_objects | grep "xxx"` 。

## 上传原始编译文件 {#section_k45_dsr_5fb .section}

`faascmd upload_object` 命令用于将本地编译的原始文件上传到用户指定的OSS bucket中。

**命令格式**

```
faascmd upload_object --object=<newFileNameinOSSBucket> --file= <your_file_path>/fileNameYouWantToUpload  

```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131112_zh-CN.png)

**说明：** 

-   如果需上传的文件在当前目录下，则无需提供路径。

-   intel fpga的本地编译原始文件为.gbs格式；xilinx fpga的本地编译原始文件为脚本处理后得到的tar包。


## 下载OSS Bucket中的object {#section_b4q_gsr_5fb .section}

`faascmd get_object` 命令用来下载OSS Bucket中指定的object。

**命令格式**

```
faascmd get_object --obejct=<yourObjectName> --file=<your_local_path>/<yourFileName>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131115_zh-CN.png)

**说明：** 如果您不提供路径，则默认下载到当前文件夹。

## 新建fpga镜像 {#section_rbl_ksr_5fb .section}

`faascmd create_image`命令用来提交制作fpga镜像的请求。请求成功时，返回fpga imageuuid。

**命令格式**

```
faascmd create_image --object=<yourObjectName> 
--fpgatype=<intel/xilinx>  --encrypted=<true/false> 
--kmskey=<key/如果encrypted为true，必须；否则可选> 
--shell=<Shell Version/必选> --name=<name/可选> 
--description=<description/可选> --tags=<tags/可选>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131117_zh-CN.png)

## 查看fpga镜像 {#section_msw_nsr_5fb .section}

`faascmd list_images`命令用于查看用户制作的所有fpga镜像的信息。

**命令格式**

```
faascmd list_images
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131118_zh-CN.png)

**说明：** 每个子账户最多允许保留10个fpga镜像。

## 删除fpga镜像 {#section_pkw_qsr_5fb .section}

`faascmd delete_image`命令用于删除fpga镜像。

**命令格式**

```
faascmd delete_image --imageuuid=<yourImageuuid>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131120_zh-CN.png)

## 下载fpga镜像 {#section_cmr_tsr_5fb .section}

`faascmd download_image`命令用于提交下载fpga镜像的请求。

**命令格式**

```
faascmd download_image  --instanceId=<yourInstanceId> 
--fpgauuid=<yourfpgauuid> --fpgatype=<intel/xilinx> 
--imageuuid=<yourImageuuid> --imagetype=<afu> 
--shell=<yourImageShellVersion>
```

**示例代码**

```
faascmd download_image --instanceId=XXXXX --fpgauuid=XXXX --fpgatype=intel --imageuuid=XXXX
```

## 查看fpga镜像下载状态 {#section_dhj_wsr_5fb .section}

`faascmd fpga_status`命令用于查看当前fpga板卡状态或fpga镜像的下载进度。

**命令格式**

```
faascmd fpga_status --fpgauuid=<fpgauuid> --instanceId=<instanceId>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131126_zh-CN.png)

## 发布fpga镜像 {#section_snv_ysr_5fb .section}

`faascmd publish_image` 命令用来提交发布fpga镜像的请求。

**命令格式**

```
faascmd publish_image --imageuuid=<yourImageuuid> --imageid=<yourFPGAImageid>
```

**说明：** 

-   imageuuid 是您要发布到云市场的镜像id。您可以通过 `faascmd list_images` 命令查看。
-   imageid 是fpga镜像id。您可以通过ECS控制台的实例详情页查看。

## 查看fpga实例的信息 {#section_vhb_btr_5fb .section}

`faascmd list_instances`命令用于获取fpga实例的基本信息，包括实例id、fpga板卡信息和shell版本。

**命令格式**

```
faascmd list_instances --instanceId=<yourInstanceId>
```

**示例代码**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726131128_zh-CN.png)

