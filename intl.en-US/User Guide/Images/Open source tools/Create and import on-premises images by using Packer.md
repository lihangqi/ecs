# Create and import on-premises images by using Packer {#concept_l1r_hws_xdb .concept}

Packer is a convenient open-source tool to create on-premises image files. It runs on the most major operating systems.

By using Packer, you can create identical on-premises images for multiple platforms from a single source configuration. This topic details steps to create an on-premises image for CentOS 6.9 on an Ubuntu 16.04 server and to upload it to Alibaba Cloud. For actual scenarios, you can customize your Packer templates as required.

## Prerequisites {#section_fss_xws_xdb .section}

-   You must have an [AccessKey](../../../../../intl.en-US/General Reference/Create an AccessKey.md#) for the configuration file.

    **Note:** Do not use the AccessKey of your Alibaba Cloud account. Instead, [create a RAM user](../../../../../intl.en-US/Quick Start/Create a RAM user.md#) and use the RAM account to create the necessary [AccessKey](../../../../../intl.en-US/General Reference/Create an AccessKey.md#) to maintain account security.

-   You must [have purchased OSS](../../../../../intl.en-US/Quick Start/Sign up for OSS.md#).

## Example of creating and importing an on-premises image {#Sample .section}

1.  Run `egrep "(svm|vmx)" /proc/cpuinfo` to check whether your on-premises server or virtual machine supports KVM. If the following output returns, KVM is supported.

    ```
    pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch epb intel_pt tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp
    flags        : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
    ```

2.  Run the following commands to install the KVM:

    ```
    sudo apt-get install qemu-kvm qemu virt-manager virt-viewer libvirt-bin bridge-utils # Install KVM and related dependencies.
    sudo virt-manager # Enable virt-manager.
    ```

    If a GUI runs in the VM console window, you have successfully installed the KVM.

3.  Install Packer.

    To install Packer, see [use Packer to create a custom image](intl.en-US/User Guide/Images/Open source tools/Use Packer to create a custom image.md#).

4.  Run the following commands to define a Packer template.

    **Note:** The on-premises image created in the following configuration is for the CentOS 6.9 operating system only. To create images for other operating systems, [customize](#) the configuration file centos.json as required.

    ```
    cd /user/local # Switch the directory.
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/centos.json # Download file centos.json that is released by Alibaba Cloud.
    wget https://raw.githubusercontent.com/alibaba/packer-provider/master/examples/alicloud/local/http/centos-6.9/ks.cfg # Download file ks.cfg that is released by Alibaba Cloud.
    mkdir -p http/centos-6.9 # Create a directory.
    mv ks.cfg http/centos-6.9/ # Move file ks.cfg to the http/centos-6.9 directory.
    ```

5.  Run the following commands to create an on-premises image.

    ```
    export ALICLOUD_ACCESS_KEY= SpecifyYourAccessKeyIDHere # Import your AccessKeyID,
    export ALICLOUD_SECRET_KEY= SpecifyYourAccessKeySecretHere # Import your AccessKeySecret.
    packer build centos.json # Create an on-premises image.
    ```

    An example result is as follows.

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

6.  Wait for a few minutes, log on to the [ECS console](https://ecs.console.aliyun.com/#/image/region/cn-beijing/imageList) and check your custom image in the image list that is in the corresponding region. In this sample, the region is China North 2 \(cn-beijing\).

## Customize a Packer template {#Custom .section}

In this example, the following JSON file is customized based on the template used to create an image for the CentOS 6.9.

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

**Parameters in a Packer builder**

QEMU builder is used in the preceding [example](#) to create a virtual machine image. Required parameters for the builder are as follows.

|Parameter|Type |Description |
|:--------|:----|:-----------|
|iso\_checksum|String|The checksum for the OS ISO file. Packer verifies this parameter before starting a virtual machine with the ISO attached. Make sure you specify at least one of the iso\_checksum or iso\_checksum\_url parameters. If you have specified the iso\_checksum parameter, the iso\_checksum\_url parameter is automatically ignored.|
|iso\_checksum\_type|String|The type of the checksum specified in iso\_checksum. Optional values:-   none: If you specify none for iso\_checksum\_type, the checksuming is ignored. This value is not recommended.
-   md5
-   sha1
-   sha256
-   sha512

|
|iso\_checksum\_url|String |A URL that points to a GNU or BSD style checksum file that contains the ISO file checksum of an operating system. It may come in either the GNU or BSD pattern. Make sure you specify either the iso\_checksum or the iso\_checksum\_url parameter. If you specify the iso\_checksum parameter, the iso\_checksum\_url parameter is automatically ignored.|
|iso\_url|String |A URL that points to the ISO file, and contains the installation image. This URL may be an HTTP URL or a file path:-   If it is an HTTP URL, Packer downloads the file from the HTTP link and caches the file for later.
-   If it is a file path to the IMG or QCOW2 file, QEMU directly starts the file. If you have the file path specified, set parameter disk\_image to true.

|
|headless|boolean|By default, Packer starts the virtual machine GUI to build a QEMU virtual machine. If you set headless to True, a virtual machine without any console is started.|

For more information, see Packer [QEMU Builder](https://www.packer.io/docs/builders/qemu.html).

**Parameters in a Packer provisioner**

The provisioner in the preceding [example](#) contains a Post-Processor module that enables automated upload of on-premises images to Alibaba Cloud. Required parameters for the provisioner are as follows:

|Parameter|Type|Description|
|:--------|:---|:----------|
|access\_key|String|Your AccessKeyID. The AccessKey has a high privilege. We recommend that you first [create a RAM user](../../../../../intl.en-US/Quick Start/Create a RAM user.md#) and use the RAM account to create an AccessKey to maintain security of your Alibaba Cloud account.|
|secret\_key|String |Your AccessKeySecret. The AccessKey has a high privilege. We recommend that you first [create a RAM user](../../../../../intl.en-US/Quick Start/Create a RAM user.md#) and use the RAM account to create an AccessKey to maintain security of your Alibaba Cloud account.|
|region|String |Select the region where you want to upload your on-premises image. In this example, the region is cn-beijing. For more information, see [regions and zones](../../../../../intl.en-US/General Reference/Regions and zones.md#).|
|image\_name|String |The name of your on-premises image. The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|oss\_bucket\_name|String |The OSS bucket name. If you specify a bucket name that does not exist, Packer creates a bucket automatically with the specified oss bucket name when uploading the image.|
|image\_os\_type|String|Image type. Optional values:-   linux
-   windows

|
|image\_platform|String |Distribution of the image. For example, CentOS.|
|image\_architecture|String|The instruction set architecture of the image. Optional values:-   i386
-   x86\_64

|
|format|String|Image format. Optional values:-   RAW
-   VHD

|

For more information, see Packer [Alicloud Post-Processor](https://www.packer.io/docs/post-processors/alicloud-import.html).

## Next step {#section_thb_v1t_xdb .section}

You can use the created image to create an ECS instance. For more information, see [create an instance from a custom image](intl.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

## References {#section_g23_w1t_xdb .section}

-   For more information about how to use Packer, see [Packer](https://www.packer.io/docs/index.html) documentation.
-   For more information about release information, visit the Packer repository on GitHub [packer](https://github.com/mitchellh/packer).
-   For more information about Alibaba Cloud open source tools, visit the Alibaba Cloud repository on GitHub [opstools](https://github.com/alibaba/opstools).
-   For more information about Alibaba Cloud and Packer project, visit the Alibaba Cloud & Packer repositories on GitHub [packer-provider](https://github.com/alibaba/packer-provider).
-   For more information about configuration file ks.cfg, see [Anaconda Kickstart](https://fedoraproject.org/wiki/Anaconda/Kickstart/zh-cn) .

