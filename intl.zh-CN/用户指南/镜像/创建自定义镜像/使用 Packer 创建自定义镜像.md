# 使用 Packer 创建自定义镜像 {#concept_idd_4cm_xdb .concept}

[Packer](https://www.packer.io/) 是一个便捷的创建自定义镜像的开源工具，能运行在大多数主流操作系统上。您可以参阅本文安装并使用 Packer，执行一两行命令就能轻松创建自定义镜像。

## 前提条件 {#section_qbp_xcm_xdb .section}

您已经获取了 AccessKey，参阅文档 [创建 AccessKey](https://help.aliyun.com/document_detail/53045.html) 在管理控制台获取 AccessKey。

**说明：** 

由于 AccessKey 权限过大，为防止错误操作，建议您 [创建 RAM 用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)，并使用 RAM 子账号 [创建 AccessKey](https://help.aliyun.com/document_detail/53045.html)。

## 步骤一. 安装 Packer {#section_j5g_gdm_xdb .section}

您可以进入 [Packer 官网下载页面](https://www.packer.io/downloads.html)，选择下载与您操作系统对应的版本，参阅以下步骤或者访问 [Packer 官方安装说明](https://www.packer.io/docs/install/index.html) 安装 Packer。

**在 Linux 服务器上安装 Packer**

配置文件 配置说明 修改该配置文件的风险 /etc/issue\*, /etc/\*-release, /etc/\*\_version 系统发行版信息配置文件 修改 /etc/issue\* 会导致系统发行版无法被正常识别，导致系统创建失败。 /boot/grub/menu.lst, /boot/grub/grub.conf 系统引导启动配置文件 修改 /boot/grub/menu.lst 会导致内核无法正确加载，导致系统无法启动。 /etc/fstab 系统启动挂载分区配置文件 修改该文件会导致异常分区无法被加载，导致系统无法启动。 /etc/shadow 系统密码相关配置文件 修改该文件为只读会导致无法修改密码文件，导致系统创建失败。 /etc/selinux/config 系统安全策略配置文件 修改 /etc/selinux/config 开启SELinux导致系统无法启动。

**在 Windows 服务器上安装 Packer**

以 Windows Server 2012 安装 64 位 Packer 为例：

1.  连接并登录到 Windows 服务器。如果您的服务器为 ECS Windows 实例，可参阅文档 [使用软件连接Windows实例](intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。
2.  打开 [Packer 下载页面](https://www.packer.io/downloads.html) 选择下载 Windows 64 位 Packer。
3.  解压文件到指定目录并安装，您可以指定自己常用的目录。
4.  在环境变量 PATH 中 定义 Packer 所在目录。
    1.  打开 **控制面板**。
    2.  选择 **所有控制面板项** \> **系统** \> **高级系统设置**。
    3.  单击 **环境变量**。
    4.  在系统变量列表中找到 **Path**。
    5.  在 **变量值** 中加入 Packer 的安装目录，如本示例中的 C:\\Packer，目录之间以半角分号（;）隔开。单击 **确定**。
5.  在 CMD 中执行命令 `packer.exe -v` 验证 Packer 安装状态。若 Windows 服务器返回 Packer 版本号，表示您已正确安装 Packer；若 Windows 服务器提示 **command not found** 表示 Packer 未正确安装。

## 步骤二. 定义 Packer 模板 {#section_kwk_bdv_ydb .section}

**说明：** 

使用 Packer 创建自定义镜像时，需要创建一个 JSON 格式的模板文件。在该模板文件中，您需要指定创建自定义镜像的 [Alicloud Image Builder（生成器）](https://www.packer.io/docs/builders/alicloud-ecs.html)和 [Provisioners（配置器）](https://www.packer.io/docs/provisioners/index.html)。Packer 具有多种配置器，可用于配置自定义镜像的内容生成方式，以下以常用的 [Shell](https://www.packer.io/docs/provisioners/shell.html) 配置器为例，定义 Packer 模板。

创建名为 alicloud 的 json 文件并粘贴以下内容。

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

**说明：** 您需要自定义以下参数的值。

|参数|获取位置|
|access\_key|您的 AccessKeyID。更多详情，参阅 [创建 AccessKey](https://help.aliyun.com/document_detail/53045.html)。|
|secret\_key|您的 AccessKeySecret。更多详情，[创建 AccessKey](https://help.aliyun.com/document_detail/53045.html)。|
|region|创建自定义镜像时使用临时资源的地域|
|image\_name|自定义镜像的名称|
|source\_image|基础镜像的名称，可以从阿里云公共镜像列表获得|
|instance\_type|创建自定义镜像时生成的临时实例的类型|
|internet\_charge\_type|创建自定义镜像时临时实例的公网带宽付费类型|
|provisioners|创建自定义镜像时使用的 [Packer 配置器](https://www.packer.io/docs/provisioners/index.html) 类型|

## 步骤三. 使用 Packer 创建自定义镜像 {#section_jwh_ldv_ydb .section}

指定 Packer 模板文件生成自定义镜像：

1.  执行命令 `export ALICLOUD_ACCESS_KEY=您的 AccessKeyID` 导入您的 AccessKeyID。
2.  执行命令 `export ALICLOUD_SECRET_KEY=您的 AccessKeySecret` 导入您的 AccessKeySecret。
3.  执行命令 `packer build alicloud.json` 创建自定义镜像。

示例运行结果如下，以下示例将创建含 Redis 的自定义镜像：

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
alicloud-ecs: Total 1.3 MB/s | 650 kB 00:00
alicloud-ecs: Running transaction check
---------------------------
==> alicloud-ecs: Deleting temporary keypair...
Build 'alicloud-ecs' finished.
==> Builds finished. The artifacts of successful builds are:
--> alicloud-ecs: Alicloud images were created:
cn-beijing: m-2ze12578be1oa4ovs6r9
```

## 后续操作 {#section_chp_qdv_ydb .section}

您可以使用该自定义镜像创建 ECS 实例，具体步骤参阅文档 [使用自定义镜像创建实例](intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#)。

## 参考链接 {#section_ntx_rdv_ydb .section}

-   您可以访问阿里云 GitHub Packer 仓库 [packer-provider](https://github.com/alibaba/packer-provider) 获取更多信息。
-   您可以参阅 [Packer 官方文档](https://www.packer.io/docs/index.html) 了解更多 Packer 使用详情。

