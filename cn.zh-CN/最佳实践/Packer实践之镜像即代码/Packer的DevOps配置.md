# Packer的DevOps配置 {#concept_hdn_ygg_chb .concept}

本文提供了在阿里云ECS使用Packer创建自定义镜像的DevOps（开发运维一体化）常用配置，适用于使用Packer创建ECS自定义镜像的场景。

## 镜像标签 {#section_rr4_pj3_chb .section}

-   字段名称：tags\{"key":"value"\}。
-   适用场景：当您的自定义镜像达到一定的数量时，适当的标记镜像有利于镜像管理和检索。例如记录镜像版本号和镜像包含的应用类型等。阿里云Builder提供了tags参数，支持为镜像绑定标签。生成的镜像自动包含阿里云ECS标签，更多有关标签的详情，请参见[标签概述](../../../../../cn.zh-CN/标签与资源/标签/标签概述.md#)。
-   配置作用：[ECS管理控制台](https://ecs.console.aliyun.com)镜像列表页面和API [DescribeImages](../../../../../cn.zh-CN/API参考/镜像/DescribeImages.md#)均支持查询镜像时返回标签以及根据标签过滤镜像。为镜像绑定标签能够和[Terraform](cn.zh-CN/最佳实践/Terraform/什么是Terraform.md#)一起为企业级标准化DevOps流程提供支持。本文推荐[Alibaba Cloud DevOps tutorials](https://alibabacloud-howto.github.io/devops/index)系列教程，其中涉及Terraform和Packer的内容参见[Continuous Delivery](https://alibabacloud-howto.github.io/devops/tutorials/devops_for_small_to_medium_web_applications/part_04_continuous_delivery.html)一节。
-   配置示例：以下配置文件为最终生成的镜像和对应的快照绑定`version=v1.0.0`和`app=web`两个标签。

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
        "io_optimized":"true",
        "tags": {
          "version": "v1.0.0",
          "app": "web"
        }
      }]
    }
    ```


## 只包含系统盘快照 {#section_lbb_wj3_chb .section}

-   字段名称：image\_ignore\_data\_disks，数据类型为Boolean。
-   适用场景：默认情况下Packer直接从ECS实例创建镜像，从实例创建镜像时如果包含数据盘，则镜像会同时包含数据盘快照。创建包含数据盘的实例通常有两种方式：
    -   方式一：通过image\_disk\_mappings设置数据盘相关参数。更多详情，请参见*Packer文档*[Alicloud Image Builder](https://www.packer.io/docs/builders/alicloud-ecs.html)。
    -   方式二：选择默认带有数据盘的实例规格。该类实例规格包含的数据盘大多为本地盘，如ecs.d1ne.2xlarge。本地盘当前并不支持创建快照，所以无法直接通过此类实例创建镜像。
-   配置作用：如果您需要选择默认带有数据盘的实例规格，但实际上数据盘部分并不是必须的，可以在配置文件中加上`"image_ignore_data_disks": "true"`实现只基于系统盘创建镜像。

## 设置快照超时时间 {#section_chd_1k3_chb .section}

-   字段名称：wait\_snapshot\_ready\_timeout，数据类型为Interger，默认值为3600（秒s）。
-   适用场景：创建镜像依赖于快照，快照的创建时间依赖于磁盘大小。当磁盘较大时，创建快照所需时间会相应增加。
-   配置作用：当磁盘太大导致超时错误时，可以通过`wait_snapshot_ready_timeout`调大超时时间。

## 通过私网IP连接实例 {#section_bgk_dk3_chb .section}

-   字段名称：ssh\_private\_ip，数据类型为Boolean。
-   适用场景：默认情况下，Packer创建EIP并绑定实例，再通过EIP对应的公网IP连接实例安装软件或执行命令。如果您能通过私网IP直接连接实例，可以免除公网IP。
-   配置作用：通过设置`"ssh_private_ip": "true"`，Packer不会分配EIP或者公网IP，而是通过私网IP连接实例。

## 设置停止实例选项 {#section_c2f_hk3_chb .section}

-   字段名称：disable\_stop\_instance，数据类型为Boolean。
-   适用场景：默认情况下，Packer执行完provisioners后，会先停止实例再创建镜像。某些特殊场景，如在Windows实例中运行Sysprep，需要实例处于运行中状态。Sysprep的使用场景示例可参见[修改Windows实例SID以搭建域环境](https://help.aliyun.com/knowledge_detail/40846.html)。
-   配置作用：通过设置`"disable_stop_instance": "true"`，Packer不会主动停止实例，而是假设配置（provisioners）中提供的命令会自行停止实例。

## 通过UserData启用WinRM {#section_cqz_3k3_chb .section}

-   字段名称：user\_data\_file。
-   适用场景：出于安全考虑，Windows镜像默认关闭了WinRM（Windows Remote Management）。但连接Windows实例及之后在实例内部执行命令都依赖于WinRM。在实例创建时，您可以通过UserData启用WinRM。
-   配置作用：通过配置`"user_data_file":"examples.ps1"`指定UserData文件路径。
-   配置示例：本示例假定UserData文件在给定的相对路径[`examples/alicloud/basic/winrm_enable_userdata.ps1`](https://github.com/hashicorp/packer/blob/master/examples/alicloud/basic/winrm_enable_userdata.ps1)下。

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
        "image_name":"packer_test",
        "source_image":"win2008r2_64_ent_sp1_zh-cn_40G_alibase_20181220.vhd",
        "instance_type":"ecs.n1.tiny",
        "io_optimized":"true",
        "internet_charge_type":"PayByTraffic",
        "image_force_delete":"true",
        "communicator": "winrm",
        "winrm_port": 5985,
        "winrm_username": "Administrator",
        "winrm_password": "Test1234",
        "user_data_file": "examples/alicloud/basic/winrm_enable_userdata.ps1"
      }],
      "provisioners": [{
        "type": "powershell",
        "inline": ["dir c:\\"]
      }]
    }
    ```

    **说明：** 

    -   示例中与WinRM相关的参数`"communicator": "winrm"`、`"winrm_port": 5985`、`"winrm_username": "Administrator"`和`"winrm_password": "Test1234"`分别表示通过WinRM连接实例、通信端口为5985、连接时使用Administrator账户、密码采用Test1234。
    -   `image_force_delete`表示如果存在同名镜像，则先删除已有镜像。

## 基于本地ISO文件制作镜像 {#section_rt2_nk3_chb .section}

-   字段名称：builders\{"type":"qemu"\}，post-processors\{"type":"alicloud-import"\}。
-   适用场景：如果线下ISO文件环境为其他虚拟化环境，也可以通过Packer完成操作。
-   配置示例：如果线下环境使用的是qemu，可以参见[使用Packer创建并导入本地镜像](../../../../../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用 Packer 创建并导入本地镜像.md#)。文档中包含两个重要的部分：
    1.  您需要使用本地虚拟化环境或软件对应的Builder，如[Qemu Builder](https://www.packer.io/docs/builders/qemu.html)。
    2.  请通过定义[Alicloud Import Post-Processor](https://www.packer.io/docs/post-processors/alicloud-import.html)将生成的本地镜像文件导入阿里云ECS。

如果您采用导入自定义镜像流程，请在本地安装虚拟化环境，将ISO文件制作成阿里云支持的镜像文件格式后再导入，如QCOW2、VHD和RAW。流程请参见[导入镜像必读](../../../../../cn.zh-CN/镜像/自定义镜像/导入镜像/导入镜像必读.md#)。

## 相关链接 {#section_rjn_4y1_dhb .section}

更多参数和样例，请参见Packer官方文档[Alicloud Image Builder](https://www.packer.io/docs/builders/alicloud-ecs.html)和[Examples](https://github.com/hashicorp/packer/tree/master/examples/alicloud)。

