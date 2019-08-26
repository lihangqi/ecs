# 使用Packer创建并导入本地镜像 {#concept_l1r_hws_xdb .concept}

Packer是一款轻量级的镜像定义工具，能够运行在主流操作系统（如Windows、Linux和MacOS）上。本文示范了如何为CentOS 6.9制作本地镜像并上传至阿里云平台。您可根据需要自定义Packer模板为其他操作系统制作镜像。

## 环境配置 {#section_pmo_usc_vu4 .section}

本文示例步骤使用了如下版本软件。操作时，请以您的实际软件版本为准。

-   服务器操作系统：Ubuntu 16.04
-   待制作镜像的操作系统：CentOS 6.9

## 前提条件 {#section_fss_xws_xdb .section}

-   已创建AccessKey。详细步骤，请参见[创建AccessKey](../../../../cn.zh-CN/通用参考/创建AccessKey.md#)。

    **说明：** 由于AccessKey权限过大，为防止数据泄露，建议您先创建RAM用户，再使用RAM用户创建AccessKey。

-   已开通OSS服务。详细步骤，请参见[开通OSS服务](../../../../cn.zh-CN/快速入门/开通OSS服务.md#)。

## 使用示例 {#Sample .section}

1.  运行`egrep "(svm|vmx)" /proc/cpuinfo`命令，查看您的源服务器或虚拟机是否支持KVM。

    返回如下信息时，表示支持KVM。

    ``` {#codeblock_6c9_qga_u2i}
    pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch epb intel_pt tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp
    flags        : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
    ```

2.  若您的源服务器或者虚拟机支持KVM，依次运行以下命令安装KVM。

    ``` {#codeblock_hwa_m0u_j5w}
    sudo apt-get install qemu-kvm qemu virt-manager virt-viewer  libvirt-bin bridge-utils  #安装KVM及相关控件
    ```

    ``` {#codeblock_u59_3h9_ks8}
    sudo virt-manager  #开启virt-manager
    ```

    如果可以通过GUI创建虚拟机，表示您已经成功安装KVM。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9708/15637893054642_zh-CN.png)

3.  安装Packer。

    详细步骤，请参见[安装Packer](cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用Packer创建自定义镜像.md#section_j5g_gdm_xdb)。

4.  依次运行以下命令定义Packer模板。

    **说明：** 以下示例命令基于CentOS 6.9系统。如果您需要为其他操作系统制作镜像，请根据需要自定义Packer模板配置文件centos.json，详情请参见[自定义Packer模板](#)。

    ``` {#codeblock_ojj_zcp_xg7}
    cd /usr/local  #切换所在目录
    ```

    ``` {#codeblock_kjk_wcz_pzr}
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/centos.json  #下载阿里云官方发行的centos.json配置文件
    ```

    ``` {#codeblock_p13_osd_8ft}
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/http/centos-6.9/ks.cfg  #下载阿里云官方发行的ks.cfg配置文件
    ```

    ``` {#codeblock_5rk_0j4_n03}
    mkdir -p http/centos-6.9  #创建目录
    ```

    ``` {#codeblock_6uc_gvm_c77}
    mv ks.cfg http/centos-6.9/  #移动文件ks.cfg到目录http/centos-6.9中
    ```

5.  依次运行以下命令创建并导入本地镜像。

    ``` {#codeblock_6mu_mmv_jq5}
    export ALICLOUD_ACCESS_KEY=<您的AccessKeyID>      #导入您的AccessKeyID
    ```

    ``` {#codeblock_n5c_akd_onh}
    export ALICLOUD_SECRET_KEY=<您的AccessKeySecret>  #导入您的AccessKeySecret
    ```

    ``` {#codeblock_p2c_rs0_s84}
    packer build centos.json                          #创建本地镜像并导入到阿里云平台
    ```

    运行的示例结果如下：

    ``` {#codeblock_zod_qad_v63}
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

6.  等待一段时间后，在对应地域的[ECS控制台镜像详情页](https://ecs.console.aliyun.com/#/image/region/cn-beijing/imageList)查看上传结果，如示例中的华北二。

## 自定义 Packer 模板 {#Custom .section}

基于CentOS 6.9系统创建本地镜像的示例，请参见[使用示例](#)。如果您需要为其他操作系统创建本地镜像，可参见CentOS 6.9的JSON文件（如下所示），自定义Packer模板。

``` {#codeblock_h8z_xag_plt}
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
        "iso_checksum": "af4axxxxxxxxxxxxxxxxx192a2",
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

[使用示例](#)中使用的生成器为QEMU Builder，该生成器用于创建虚拟机镜像。Packer生成器的必需参数说明，如下表所示。其余可选参数，请参见Packer[QEMU Builder](https://www.packer.io/docs/builders/qemu.html)页面。

|必需参数|类型|描述|
|:---|:-|:-|
|iso\_checksum|string|操作系统的ISO文件的校验和。Packer在启动挂载了ISO的虚拟机之前检查该参数。至少指定iso\_checksum或者iso\_checksum\_url参数；当您指定了参数iso\_checksum时，参数iso\_checksum\_url的值被自动忽略。|
|iso\_checksum\_type|string|已指定的操作系统的ISO文件的校验和类型。取值范围： -   none：忽略校验和过程。不推荐指定该值
-   md5
-   sha1
-   sha256
-   sha512

 |
|iso\_checksum\_url|string|一个包含了操作系统ISO文件校验和的检验和文件的链接（URL），样式为GNU或者 BSD。您需要至少指定iso\_checksum或者iso\_checksum\_url参数；当您指定了参数iso\_checksum时，参数iso\_checksum\_url的值被自动忽略。|
|iso\_url|string|一个指向ISO并包含安装镜像的URL。这个URL可以是一个HTTP链接,也可以是一个文件路径: -   如果是HTTP链接，Packer从HTTP链接下载文件并缓存运行。
-   如果是IMG或者QCOW2文件链接，QEMU直接在文件基础上启动。当您指定了文件路径时，请将参数disk\_image置为true。

 |
|headless|boolean|Packer默认通过启动图形化虚拟机界面构建QEMU虚拟机。当您将headless置为True时，将启动一个没有控制台的虚拟机。|

[使用示例](#)中使用的配置器中包含了Post-Processor模块，该模块实现自动化上传本地镜像到ECS云平台。Post-Processor模块的必需参数如下所示。其余可选参数，请参见Packer[Alicloud Post-Processor](https://www.packer.io/docs/post-processors/alicloud-import.html)页面。

|必需参数|类型|描述|
|:---|:-|:-|
|access\_key|string|您的AccessKeyID。|
|secret\_key|string|您的AccessKeySecret。|
|region|string|本地镜像上传的阿里云地域ID，如本示例中的`cn-beijing`。更多地域信息，请参见[地域和可用区](../../../../cn.zh-CN/通用参考/地域和可用区.md#)。|
|image\_name|string|您的本地镜像的名称。 -   由 \[2, 128\] 位英文或中文字符组成。
-   必须以大小写字母或中文字符开始。
-   可以包含数字、下划线（\_）或者连字符（-）。
-   不能以http://或https://开头。

 |
|oss\_bucket\_name|string|您的OSS Bucket名称。若您指定了一个不存在的Bucket名称，Packer上传镜像时自动创建一个同名Bucket。|
|image\_os\_type|string|镜像类型，取值范围： -   linux
-   windows

 |
|image\_platform|string|镜像发行版本。例如，本示例中的CentOS。|
|image\_architecture|string|镜像发行版本的架构平台，取值范围： -   i386
-   x86\_64

 |
|format|string|镜像的格式，取值范围： -   RAW
-   VHD

 |

## 下一步 {#section_thb_v1t_xdb .section}

您可以使用上传至阿里云平台的自定义镜像创建ECS实例，请参见[使用自定义镜像创建实例](cn.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。

## 参考链接 {#section_g23_w1t_xdb .section}

-   了解Packer使用详情，请参见[Packer 官方文档](https://www.packer.io/docs/index.html) 。
-   获取Packer的更多信息，可访问GitHub Packer仓库[packer](https://github.com/mitchellh/packer)。
-   获取opstools的更多信息，可访问GitHub Alibaba仓库[opstools](https://github.com/alibaba/opstools)。
-   获取packer-provider的更多信息，可访问GitHub Alibaba&Packer仓库[packer-provider](https://github.com/alibaba/packer-provider)。
-   了解配置文件ks.cfg的更多信息，请参见[Anaconda Kickstart](https://fedoraproject.org/wiki/Anaconda/Kickstart/zh-cn)。

