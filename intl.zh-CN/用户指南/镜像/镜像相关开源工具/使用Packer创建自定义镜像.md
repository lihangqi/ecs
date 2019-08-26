# 使用Packer创建自定义镜像 {#concept_idd_4cm_xdb .concept}

Packer是一款轻量级的镜像定义工具，能够运行在常用的主流操作系统（如Windows、Linux和macOS）上。参阅本文安装并使用Packer，轻松创建自定义镜像。

**说明：** 本文描述仅适用于运行Linux操作系统的服务器。

## 1. 安装Packer {#section_j5g_gdm_xdb .section}

您可以进入 [Packer 官网下载页面](https://www.packer.io/downloads.html)，选择下载与您操作系统对应的版本，参阅以下步骤或者访问 [Packer 官方安装说明](https://www.packer.io/docs/install/index.html) 安装Packer。

1.  连接并登录到Linux服务器。如果您的服务器为ECS Linux实例，可参阅文档 [使用用户名密码验证连接 Linux 实例](intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md#)。
2.  执行命令 `cd /usr/local/bin` 进入 /usr/local/bin 目录。

    **说明：** /usr/local/bin 目录为环境变量目录，您可以将Packer安装到该目录下或其他已添加到环境变量的目录下。

3.  执行命令 `wget https://releases.hashicorp.com/packer/1.1.1/packer_1.1.1_linux_amd64.zip` 获取Packer安装包。您可以访问 [Packer 下载页面](https://www.packer.io/downloads.html) 获取其他版本Packer安装包。
4.  执行命令 `unzip packer_1.1.1_linux_amd64.zip` 解压文件。
5.  执行命令 `packer -v` 验证Packer安装状态。若Linux服务器返回Packer版本号，表示您已正确安装Packer。若Linux服务器提示 `command not found` 表示Packer未正确安装。

## 2. 定义Packer模板 {#section_kwk_bdv_ydb .section}

使用Packer创建自定义镜像时，需要创建一个JSON格式的模板文件。在该模板文件中，您需要指定创建自定义镜像的 [Alicloud Image Builder（生成器）](https://www.packer.io/docs/builders/alicloud-ecs.html) 和 [Provisioners（配置器）](https://www.packer.io/docs/provisioners/index.html)。Packer具有多种配置器，可用于配置自定义镜像的内容生成方式，以下以常用的 [Shell](https://www.packer.io/docs/provisioners/shell.html) 配置器为例，定义Packer模板。

在Linux服务器中创建名为alicloud的json文件并粘贴以下内容。

```
{
     "variables": {
       "access_key": "{{env `ALICLOUD_ACCESS_KEY`}}",
       "secret_key": "{{env `ALICLOUD_SECRET_KEY`}}"
     },
     "builders": [{
       "type":"alicloud-ecs",
       "access_key":"{{user `access_key`}}",
       "secret_key":"{{user `secret_key`}}",
       "region":"cn-beijing",
       "image_name":"packer_basic",
       "source_image":"centos_7_02_64_20G_alibase_20170818.vhd",
       "ssh_username":"root",
       "instance_type":"ecs.n1.tiny",
       "internet_charge_type":"PayByTraffic",
       "io_optimized":"true"
     }],
     "provisioners": [{
       "type": "shell",
       "inline": [
         "sleep 30",
         "yum install redis.x86_64 -y"
       ]
     }]
   }
```

您需要自定义以下参数值。

|参数|描述|
|:-|:-|
|access\_key|您的AccessKeyID。更多详情，参阅 [创建AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。**说明：** 由于AccessKey权限过大，为防止错误操作，建议您 [创建 RAM 用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)，并使用RAM子账号 [创建AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。

|
|secret\_key|您的AccessKeySecret。更多详情，参阅 [创建AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。|
|region|创建自定义镜像时使用临时资源的地域。|
|image\_name|自定义镜像的名称。|
|source\_image|基础镜像的名称，可以从阿里云公共镜像列表获得。|
|instance\_type|创建自定义镜像时生成的临时实例的类型。|
|internet\_charge\_type|创建自定义镜像时临时实例的公网带宽付费类型。|
|provisioners|创建自定义镜像时使用的 [Packer 配置器](https://www.packer.io/docs/provisioners/index.html) 类型。|

## 3. 使用Packer创建自定义镜像 {#section_jwh_ldv_ydb .section}

指定Packer模板文件生成自定义镜像：

1.  导入您的AccessKeyID：运行 `export ALICLOUD_ACCESS_KEY=您的 AccessKeyID` 。
2.  导入您的AccessKeySecret：运行 `export ALICLOUD_SECRET_KEY=您的 AccessKeySecret` 。
3.  执行命令 `packer build alicloud.json` 创建自定义镜像。

示例运行结果如下，以下示例将创建含Redis的自定义镜像：

```
alicloud-ecs output will be in this color.
==> alicloud-ecs: Prevalidating alicloud image name...
alicloud-ecs: Found image ID: centos_7_02_64_20G_alibase_20170818.vhd
==> alicloud-ecs: Start creating temporary keypair: packer_59e44f40-c8d6-0ee3-7fd8-b1ba08ea94b8
==> alicloud-ecs: Start creating alicloud vpc
---------------------------
==> alicloud-ecs: Provisioning with shell script: /var/folders/3q/w38xx_js6cl6k5mwkrqsnw7w0000gn/T/packer-shell257466182
alicloud-ecs: Loaded plugins: fastestmirror
---------------------------
alicloud-ecs: Total                                              1.3 MB/s | 650 kB 00:00
alicloud-ecs: Running transaction check
---------------------------
==> alicloud-ecs: Deleting temporary keypair...
Build 'alicloud-ecs' finished.
==> Builds finished. The artifacts of successful builds are:
--> alicloud-ecs: Alicloud images were created:
cn-beijing: m-2ze12578be1oa4ovs6r9
```

## 下一步 {#section_chp_qdv_ydb .section}

 [使用自定义镜像创建实例](intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#)。

## 参考链接 {#section_ntx_rdv_ydb .section}

-   访问阿里云GitHub Packer仓库 [packer-provider](https://github.com/alibaba/packer-provider) 获取更多信息。
-   参阅 [Packer官方文档](https://www.packer.io/docs/index.html) 了解更多Packer使用详情。

