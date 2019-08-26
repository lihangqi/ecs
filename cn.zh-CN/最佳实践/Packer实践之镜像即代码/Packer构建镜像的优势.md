# Packer构建镜像的优势 {#concept_rtr_gdg_chb .concept}

通过Packer，您只需在JSON配置文件中指明构建镜像所需的基本信息、以及需要安装到镜像中的软件及配置，即可自动化构建ECS镜像。

## 什么是Packer {#section_nsc_4dg_chb .section}

Packer是HashiCorp推出的一款镜像工具，旨在通过简易的方式自动化构建镜像。由于构建镜像的过程以一份JSON配置文件为准，您无需担心多次构建的镜像存在不一致。Packer还能为测试和更新镜像带来使用便利，降低运维和管理镜像的时间成本。更多详情，请访问[Packer官网](https://www.packer.io/)。

## 镜像构建方式对比 {#section_hmz_ykg_chb .section}

目前，阿里云支持以下构建镜像的方式：

|构建方式列举|工具与依赖|优点|缺点|
|:-----|:----|:-|:-|
|[使用快照创建自定义镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)|支持通过ECS控制台或者API创建，前提是您必须已经创建了一份系统盘快照。| -   易上手。
-   可多次利用计算资源。
-   可以根据实时生产环境创建镜像。
-   基于阿里云公共镜像创建，安全可靠。

 | -   随镜像内需预装的软件及其配置扩充变得复杂。
-   难以确保人工操作是否准确无误和前后一致。
-   后期维护成本高。

 |
|[使用实例创建自定义镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)|支持通过ECS控制台或者API创建，前提是您已经创建了一台实例。|
|[使用Packer构建自定义镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用Packer创建自定义镜像.md#)|支持识别Packer请求，通过AccessKey验证用户信息。| -   无需提前创建实例或快照。
-   可多次利用和修改JSON文件。
-   具有操作日志，步骤清晰可见易于回溯。
-   自动释放临时资源。
-   支持自动转换ISO文件并导入阿里云ECS。
-   可基于阿里云公共镜像和本地ISO文件构建，灵活方便。

 |具有少量学习成本。|

## 操作条件 {#section_g31_fbh_chb .section}

本文通过比较“使用实例创建自定义镜像”和“使用Packer构建自定义镜像”的操作流程，突出Packer在DevOps场景中的优势。以下为本次操作的假设场景和一致性条件：

-   目标地域：阿里云华北2（北京）地域，更多详情，请参见[地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。
-   操作系统：CentOS 7.3 64位。本文两种方式均采用公共镜像centos\_7\_03\_64\_20G\_alibase\_20170818.vhd，您可以在[ECS管理控制台](https://ecs.console.aliyun.com)或调用[DescribeImages](../../../../../cn.zh-CN/API参考/镜像/DescribeImages.md#)查询其他操作系统的镜像ID列表。
-   自定义服务：redis。
-   是否保留临时资源：否。

**说明：** 本文操作会创建计费资源，请注意释放和清理。如实例、公网IP、快照等。

## 使用实例创建自定义镜像 {#section_onx_wdg_chb .section}

本示例介绍如何通过ECS管理控制台创建一份自定义镜像。以下为示例操作的流程示意图：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/138826/155298835040861_zh-CN.png)

1.  登录[云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  在左侧导航栏，单击**实例**。
3.  选择地域。
4.  参见[使用向导创建实例](../../../../../cn.zh-CN/实例/实例生命周期/创建实例/使用向导创建实例.md#)完成实例购买。为较少费用消耗和简化操作流程，您可以选择以下配置：
    -   计费方式：按量付费，更多详情，请参见[按量付费](../../../../../cn.zh-CN/产品定价/按量付费.md#)。
    -   实例规格：ecs.t5-lc1m1.small，更多详情，请参见[实例规格族汇总](../../../../../cn.zh-CN/实例/实例规格族/实例规格族汇总.md#)。
    -   公共镜像：CentOS 7.3 64位。
    -   专有网络：默认VPC。
    -   安全组：默认安全组。
    -   公网带宽：如果不需要公网访问，可以选择不开通公网带宽，并通过[管理终端](../../../../../cn.zh-CN/实例/实例生命周期/连接实例/使用管理终端连接Linux实例.md#)远程连接实例。
5.  远程连接已创建的ECS实例。连接方式可参见[连接方式导航](../../../../../cn.zh-CN/实例/实例生命周期/连接实例/连接方式导航.md#)。
6.  运行`yum install redis.x86_64 -y`安装redis服务。
7.  返回ECS控制台，选择华北2（北京）地域。
8.  参见[使用实例创建自定义镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)创建一份镜像。
9.  在**快照和镜像** \> **镜像**页面查看镜像完成状态。
10. （可选）镜像制作成功后，释放临时资源，包括实例等。若您使用的是弹性公网IP，也可以选择释放。

## 使用Packer构建自定义镜像 {#section_jmz_xdg_chb .section}

本示例介绍如何通过Packer构建一份自定义镜像。以下为示例操作的流程示意图：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/138826/155298835040862_zh-CN.png)

**前提条件**

您已经安装了Packer。关于如何安装Packer，请参见[Packer官方文档](https://www.packer.io/intro/getting-started/install.html)或者阿里云文档[使用Packer构建自定义镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用Packer创建自定义镜像.md#)。

**操作步骤**

1.  本地新建一份alicloud.json文件，文件内容如下：

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
        "source_image":"centos_7_03_64_20G_alibase_20170818.vhd",
        "ssh_username":"root",
        "instance_type":"ecs.t5-lc1m1.small",
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

    |参数|示例值|参数解释|
    |:-|---|:---|
    |variables\{"varible1":"value"\}|variables\{"access\_key":"\{\{env \`ALICLOUD\_ACCESS\_KEY\`\}\}"\}|定义了[builders](https://www.packer.io/docs/builders/index.html)中会用到的变量（[variables](https://www.packer.io/docs/templates/user-variables.html)）。将AccessKey（access\_key和secret\_key）信息写入配置文件有信息泄露的风险，设置成变量后可防止意外，变量的值取自运行时的输入值。|
    |builders\{"type":"value"\}|builders\{"type":"alicloud-ecs"\}|Packer定义的镜像生成器（[builders](https://www.packer.io/docs/builders/alicloud-ecs.html)）。阿里云支持alicloud-ecs，又称Alicloud Image Builder，用于在阿里云ECS创建自定义镜像。|
    |provisioners\{"type":"value"\}|provisioners\{"type":"shell"\}|Packer定义的镜像配置器（[provisioners](https://www.packer.io/docs/provisioners/index.html)），用以定义需要在临时实例内执行的操作。本文使用的是[Shell Provisioner](https://www.packer.io/docs/provisioners/shell.html)，表示在连接Linux实例后自动执行一段shell命令（如`yum install redis.x86_64 -y`）安装redis服务。|

    |参数|数据类型|示例值|参数解释|重要度|
    |:-|----|---|:---|---|
    |access\_key|String|LTAInPyXXXXQXXXX|您的AccessKeyID。更多详情，请参见[创建AccessKey](../../../../../cn.zh-CN/通用参考/创建AccessKey.md#)。**说明：** 由于AccessKey权限过大，为防止错误操作，建议您[创建RAM用户](../../../../../cn.zh-CN/快速入门/创建 RAM 用户.md#)，并使用RAM子账号创建AccessKey。

|高|
    |secret\_key|String|CM1ycKrrCekQ0dhXXXXXXXXXl7yavUT|您的AccessKeySecret。|高|
    |region|String|cn-beijing|目标自定义镜像的所属地域。更多详情，请参见[地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。|高|
    |image\_name|String|packer\_basic|目标自定义镜像的名称。不允许与已有镜像重名。|低|
    |source\_image|String|centos\_7\_03\_64\_20G\_alibase\_20170818.vhd|具有相同操作系统的阿里云公共镜像ID。|高|
    |instance\_type|String|ecs.t5-lc1m1.small|创建自定义镜像时使用的临时实例的实例规格。更多详情，请参见[实例规格族汇总](../../../../../cn.zh-CN/实例/实例规格族/实例规格族汇总.md#)。|低|
    |internet\_charge\_type|String|PaybyTraffic|临时实例的公网带宽付费类型。建议设置为按流量付费（PaybyTraffic）。|低|
    |io\_optimized|Boolean|true|临时实例的I/O优化属性。建议设置为I/O优化（true）。|低|

2.  执行以下命令构建一份镜像：

    ```
    packer build alicloud.json
    ```

    **说明：** 构建镜像是相对耗时的任务，请您耐心等待。镜像构建成功后，会出现在相应阿里云地域中，您可以通过ECS控制台或[DescribeImages](../../../../../cn.zh-CN/API参考/镜像/DescribeImages.md#)查看。

    构建镜像时会产生的操作日志。日志给出了构建过程中执行的每一个步骤，包括校验参数、创建临时资源、预安装软件、创建目标资源和释放临时资源等。

    ```
    alicloud-ecs output will be in this color.
    
    ==> alicloud-ecs: Prevalidating image name...
        alicloud-ecs: Found image ID: centos_7_03_64_20G_alibase_20170818.vhd
    ==> alicloud-ecs: Creating temporary keypair: packer_xxx
    ==> alicloud-ecs: Creating vpc
    ==> alicloud-ecs: Creating vswitch...
    ==> alicloud-ecs: Creating security groups...
    ==> alicloud-ecs: Creating instance.
    ==> alicloud-ecs: Allocating eip
    ==> alicloud-ecs: Allocated eip xxx
        alicloud-ecs: Attach keypair packer_xxx to instance: i-xxx
    ==> alicloud-ecs: Starting instance: i-xxx
    ==> alicloud-ecs: Using ssh communicator to connect: ***
    ==> alicloud-ecs: Waiting for SSH to become available...
    ==> alicloud-ecs: Connected to SSH!
    ==> alicloud-ecs: Provisioning with shell script: /var/folders/k_/nv2r4drx3bs08l6tcx06ndb40000gn/T/packer-shell260049331
        alicloud-ecs: Loaded plugins: fastestmirror
        alicloud-ecs: Determining fastest mirrors
        alicloud-ecs: Resolving Dependencies
        alicloud-ecs: --> Running transaction check
        alicloud-ecs: ---> Package redis.x86_64 0:3.2.12-2.el7 will be installed
        alicloud-ecs: --> Processing Dependency: libjemalloc.so.1()(64bit) for package: redis-3.2.12-2.el7.x86_64
        alicloud-ecs: --> Running transaction check
        alicloud-ecs: ---> Package jemalloc.x86_64 0:3.6.0-1.el7 will be installed
        alicloud-ecs: --> Finished Dependency Resolution
        alicloud-ecs:
        alicloud-ecs: Dependencies Resolved
        alicloud-ecs:
        alicloud-ecs: ================================================================================
        alicloud-ecs:  Package           Arch            Version                  Repository     Size
        alicloud-ecs: ================================================================================
        alicloud-ecs: Installing:
        alicloud-ecs:  redis             x86_64          3.2.12-2.el7             epel          544 k
        alicloud-ecs: Installing for dependencies:
        alicloud-ecs:  jemalloc          x86_64          3.6.0-1.el7              epel          105 k
        alicloud-ecs:
        alicloud-ecs: Transaction Summary
        alicloud-ecs: ================================================================================
        alicloud-ecs: Install  1 Package (+1 Dependent package)
        alicloud-ecs:
        alicloud-ecs: Total download size: 648 k
        alicloud-ecs: Installed size: 1.7 M
        alicloud-ecs: Downloading packages:
        alicloud-ecs: --------------------------------------------------------------------------------
        alicloud-ecs: Total                                              2.2 MB/s | 648 kB  00:00
        alicloud-ecs: Running transaction check
        alicloud-ecs: Running transaction test
        alicloud-ecs: Transaction test succeeded
        alicloud-ecs: Running transaction
        alicloud-ecs:   Installing : jemalloc-3.6.0-1.el7.x86_64                                  1/2
        alicloud-ecs:   Installing : redis-3.2.12-2.el7.x86_64                                    2/2
        alicloud-ecs:   Verifying  : redis-3.2.12-2.el7.x86_64                                    1/2
        alicloud-ecs:   Verifying  : jemalloc-3.6.0-1.el7.x86_64                                  2/2
        alicloud-ecs:
        alicloud-ecs: Installed:
        alicloud-ecs:   redis.x86_64 0:3.2.12-2.el7
        alicloud-ecs:
        alicloud-ecs: Dependency Installed:
        alicloud-ecs:   jemalloc.x86_64 0:3.6.0-1.el7
        alicloud-ecs:
        alicloud-ecs: Complete!
    ==> alicloud-ecs: Stopping instance: i-xxx
    ==> alicloud-ecs: Waiting instance stopped: i-xxx
    ==> alicloud-ecs: Creating image: packer_basic
        alicloud-ecs: Detach keypair packer_xxx from instance: i-xxx
    ==> alicloud-ecs: Cleaning up 'EIP'
    ==> alicloud-ecs: Cleaning up 'instance'
    ==> alicloud-ecs: Cleaning up 'security group'
    ==> alicloud-ecs: Cleaning up 'vSwitch'
    ==> alicloud-ecs: Cleaning up 'VPC'
    ==> alicloud-ecs: Deleting temporary keypair...
    Build 'alicloud-ecs' finished.
    
    ==> Builds finished. The artifacts of successful builds are:
    --> alicloud-ecs: Alicloud images were created:
    
    cn-beijing: m-xxx
    ```


## 相关链接 {#section_jkd_ktg_chb .section}

更多参数和样例，请参见：

-   *Packer官方文档*[Alicloud Image Builder](https://www.packer.io/docs/builders/alicloud-ecs.html)和[Examples](https://github.com/hashicorp/packer/tree/master/examples/alicloud)
-   [Packer的DevOps配置](cn.zh-CN/最佳实践/Packer实践之镜像即代码/Packer的DevOps配置.md#)

