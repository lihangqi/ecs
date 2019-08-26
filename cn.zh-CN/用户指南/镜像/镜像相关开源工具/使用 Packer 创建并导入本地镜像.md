# 使用 Packer 创建并导入本地镜像 {#concept_l1r_hws_xdb .concept}

Packer是一款轻量级的镜像定义工具，能够运行在常用的主流操作系统（如Windows、Linux和macOS）上。参阅本文安装并使用Packer，轻松创建自定义镜像。

自行创建本地镜像并上传到云平台是一个非常繁复的过程，此处示范了如何在 Ubuntu 16.04 服务器中创建 CentOS 6.9 本地镜像并上传到阿里云云平台，如果您需要制作其他操作系统类型的镜像，请根据需要 自定义Packer模板。

## 前提条件 {#section_fss_xws_xdb .section}

-   您已经 [创建 AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)，用于输出到配置文件 centos.json 里。

    **说明：** 由于 AccessKey 权限过大，为防止数据泄露，建议您 [创建 RAM 用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)，并使用 RAM 用户子账号 [创建 AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。

-   您已经 [开通OSS服务](../../../../intl.zh-CN/快速入门/开通OSS服务.md#)，便于上传镜像文件到云平台。

## 使用示例 {#Sample .section}

1.  运行 `egrep "(svm|vmx)" /proc/cpuinfo` 确保您的源服务器或者虚拟机是否支持 KVM。当返回下列信息时，表示支持 KVM。

    ```
    pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch epb intel_pt tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp
    flags        : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
    ```

2.  若您的源服务器或者虚拟机支持 KVM，运行以下命令安装 KVM。

    ```
    sudo apt-get install qemu-kvm qemu virt-manager virt-viewer  libvirt-bin bridge-utils  #安装 KVM 及相关控件。
    sudo virt-manager  #开启 virt-manager。
    ```

    如果可以通过 GUI 创建虚拟机，表示您已经成功安装 KVM。

3.  安装 Packer。

    您可以参阅 [使用Packer创建自定义镜像](intl.zh-CN/用户指南/镜像/镜像相关开源工具/使用Packer创建自定义镜像.md#) 部分内容安装 Packer。

4.  依次执行以下命令定义 Packer 模板:

    **说明：** 以下示例制作的本地镜像基于 CentOS 6.9 操作系统，如果您需要创建其他类型操作系统的镜像，您可以根据需要 [自定义 Packer 模板](#) 配置文件 centos.json。

    ```
    cd /user/local  #切换所在目录。
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/centos.json  #下载阿里云官方发行的 centos.json 配置文件。
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/http/centos-6.9/ks.cfg  #下载阿里云官方发行的 ks.cfg 配置文件。
    mkdir -p http/centos-6.9  #创建目录。
    mv ks.cfg http/centos-6.9/  #移动文件 ks.cfg 到目录  http/centos-6.9 中。
    ```

5.  依次执行以下命令创建本地镜像。

    ```
    export ALICLOUD_ACCESS_KEY=您的 AccessKeyID  #导入您的 AccessKeyID。
    export ALICLOUD_SECRET_KEY=您的 AccessKeySecret  #导入您的 AccessKeySecret。
    packer build centos.json  #创建本地镜像。
    ```

    示例运行结果如下：

    ```
    qemu output will be in this color.
     ==> qemu: Downloading or copying ISO
         qemu: Downloading or copying: http://mirrors.aliyun.com/centos/6.9/isos/x86_64/CentOS-6.9-x86_64-minimal.iso
     ................................................
     ==> qemu: Running post-processor: alicloud-import
         qemu (alicloud-import): Deleting import source https://oss-cn-beijing.aliyuncs.com/packer/centos_x86_64
     Build 'qemu' finished.
     ==> Builds finished. The artifacts of successful builds are:
     --> qemu: Alicloud images were created:
     cn-beijing: XXXXXXXX
    ```

6.  等待一段时间后，在对应地域的 [ECS 控制台镜像详情页](https://ecs.console.aliyun.com/#/image/region/cn-beijing/imageList) 查看上传结果，如示例中的华北二。

## 后续操作 {#section_lpr_gys_xdb .section}

您可以使用该自定义镜像创建 ECS 实例，具体步骤参阅 [使用自定义镜像创建实例](intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#)。

## 自定义 Packer 模板 {#Custom .section}

以上 [使用示例](#) 制作的本地镜像基于 CentOS 6.9 操作系统，如果您需要创建其他类型操作系统的镜像，您可以根据需要自定义 Packer 模板。

例如，以下 JSON 文件是基于 Packer 模板生成的，用于创建 CentOS 6.9 镜像。

```
{"variables": {
        "box_basename": "centos-6.9",
        "build_timestamp": "{{isotime \"20060102150405\"}}",
        "cpus": "1",
        "disk_size": "4096",
        "git_revision": "__unknown_git_revision__",
        "headless": "",
        "http_proxy": "{{env `http_proxy`}}",
        "https_proxy": "{{env `https_proxy`}}",
        "iso_checksum_type": "md5",
        "iso_checksum": "af4a1640c0c6f348c6c41f1ea9e192a2",
        "iso_name": "CentOS-6.9-x86_64-minimal.iso",
        "ks_path": "centos-6.9/ks.cfg",
        "memory": "512",
        "metadata": "floppy/dummy_metadata.json",
        "mirror": "http://mirrors.aliyun.com/centos",
        "mirror_directory": "6.9/isos/x86_64",
        "name": "centos-6.9",
        "no_proxy": "{{env `no_proxy`}}",
        "template": "centos-6.9-x86_64",
        "version": "2.1.TIMESTAMP"
      },
    "builders":[
        {
          "boot_command": [
            "<tab> text ks=http://{{ .HTTPIP }}:{{ .HTTPPort }}/{{user `ks_path`}}<enter><wait>"
          ],
          "boot_wait": "10s",
          "disk_size": "{{user `disk_size`}}",
          "headless": "{{ user `headless` }}",
          "http_directory": "http",
          "iso_checksum": "{{user `iso_checksum`}}",
          "iso_checksum_type": "{{user `iso_checksum_type`}}",
          "iso_url": "{{user `mirror`}}/{{user `mirror_directory`}}/{{user `iso_name`}}",
          "output_directory": "packer-{{user `template`}}-qemu",
          "shutdown_command": "echo 'vagrant'|sudo -S /sbin/halt -h -p",
          "ssh_password": "vagrant",
          "ssh_port": 22,
          "ssh_username": "root",
          "ssh_wait_timeout": "10000s",
          "type": "qemu",
          "vm_name": "{{ user `template` }}.raw",
          "net_device": "virtio-net",
          "disk_interface": "virtio",
          "format": "raw"
        }
      ],
    "provisioners": [{
          "type": "shell",
          "inline": [
                "sleep 30",
                "yum install cloud-util cloud-init -y"
              ]
        }],
      "post-processors":[
        {
          "type":"alicloud-import",
          "oss_bucket_name": "packer",
          "image_name": "packer_import",
          "image_os_type": "linux",
          "image_platform": "CentOS",
          "image_architecture": "x86_64",
          "image_system_size": "40",
          "region":"cn-beijing"
        }
      ]
}
```

**Packer 生成器参数说明**

[使用示例](#) 中使用的生成器为 QEMU Builder，该生成器用于创建虚拟机镜像。其必需参数如下所示。

|必需参数|类型|描述|
|:---|:-|:-|
|iso\_checksum|string|操作系统的 ISO 文件的校验和。Packer 在启动挂载了 ISO 的虚拟机之前检查该参数。至少指定 iso\_checksum 或者 iso\_checksum\_url 参数；当您指定了参数iso\_checksum时，参数 iso\_checksum\_url 的值被自动忽略。|
|iso\_checksum\_type|string|已指定的操作系统的 ISO 文件的校验和类型。取值范围：-   none：忽略校验和过程。不推荐指定该值
-   md5
-   sha1
-   sha256
-   sha512

|
|iso\_checksum\_url|string|一个包含了操作系统 ISO 文件校验和的检验和文件的链接（URL），样式为 GNU 或者 BSD。您需要至少指定 iso\_checksum 或者 iso\_checksum\_url 参数；当您指定了参数iso\_checksum时，参数 iso\_checksum\_url 的值被自动忽略。|
|iso\_url|string|一个指向 ISO 并包含安装镜像的 URL。这个 URL 可以是一个 HTTP 链接,也可以是一个文件路径:-   如果是 HTTP 链接，Packer 从 HTTP 链接下载文件并缓存运行。
-   如果是 IMG 或者 QCOW2 文件 链接，QEMU直接在文件基础上启动。当您指定了文件路径时，请将参数 disk\_image 置为 true。

|
|headless|boolean|Packer 默认通过启动图形化虚拟机界面构建 QEMU 虚拟机。当您将 headless 置为 True 时，将启动一个没有控制台的虚拟机。|

其余可选参数可参阅 Packer [QEMU Builder](https://www.packer.io/docs/builders/qemu.html) 页面。

**Packer 配置器部分参数说明**

[使用示例](#) 中使用的配置器中包含了 Post-Processor 模块，该模块实现自动化上传本地镜像到 ECS 云平台。Post-Processor 模块的必需参数如下所示。

|必需参数|类型|描述|
|:---|:-|:-|
|access\_key|string|您的 AccessKeyID。由于 AccessKey 权限过大，为防止数据泄露，建议您 [创建 RAM 用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)，并使用 RAM 用户子账号 [创建 AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。|
|secret\_key|string|您的 AccessKeySecret。由于 AccessKey 权限过大，为防止数据泄露，建议您 [创建 RAM 用户](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)，并使用 RAM 用户子账号 [创建 AccessKey](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)。|
|region|string|本地镜像上传的地域，如本示例中的 cn-beijing。请参阅 [地域和可用区](../../../../intl.zh-CN/通用参考/地域和可用区.md#)查看更多地域信息。|
|image\_name|string|您的本地镜像的名称。-   由 \[2, 128\] 位英文或中文字符组成。
-   必须以大小写字母或中文字符开始。
-   可以包含数字、下划线（\_）或者连字符（-）。
-   不能以 http:// or https:// 开头。

|
|oss\_bucket\_name|string|您的 OSS Bucket 名称。若您指定了一个不存在的 Bucket 名称，Packer 上传镜像时自动创建一个同名 Bucket。|
|image\_os\_type|string|镜像类型，取值范围：-   linux
-   windows

|
|image\_platform|string|镜像发行版本，如本示例中的 CentOS。|
|image\_architecture|string|镜像发行版本的架构平台，取值范围：-   i386
-   x86\_64

|
|format|string|镜像的格式，取值范围：-   RAW
-   VHD

|

其余可选参数可参阅 Packer [Alicloud Post-Processor](https://www.packer.io/docs/post-processors/alicloud-import.html) 页面。

## 下一步 {#section_thb_v1t_xdb .section}

您可以使用该镜像创建 ECS 实例，参阅 [使用自定义镜像创建实例](intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#)。

## 参考链接 {#section_g23_w1t_xdb .section}

-   您可以参阅 [Packer 官方文档](https://www.packer.io/docs/index.html) 了解 Packer 使用详情。
-   您可以访问 GitHub Packer 仓库 [packer](https://github.com/mitchellh/packer) 获取更多信息。
-   您可以访问 GitHub Alibaba 仓库 [opstools](https://github.com/alibaba/opstools) 获取更多信息。
-   您可以访问 GitHub Alibaba&Packer 仓库 [packer-provider](https://github.com/alibaba/packer-provider) 获取更多信息。
-   您可以参阅 [Anaconda Kickstart](https://fedoraproject.org/wiki/Anaconda/Kickstart/zh-cn) 了解配置文件 ks.cfg 的更多信息。

