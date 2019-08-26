# CLI参数 {#CliParams .reference}

迁云工具从1.2.8版本开始支持命令行（Command line interface，CLI）参数，运行迁云工具时使用`--help`选项可以查看参数列表。使用CLI参数，您无需打开各种JSON文件即可配置迁云工具、调整自定义使用习惯和一键清除client\_data。如果您使用的是旧版本迁云工具，请重新[下载压缩包](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip)以获取更多功能。CLI参数需要您对迁云工具的使用方式有所了解，更多详情，请参见[使用迁云工具](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)。

## Windows版本选项及参数列表 {#section_tnt_qy1_kfb .section}

Windows版迁云工具的使用方法如下：

``` {#codeblock_zmg_jk2_2uf}
go2aliyun_client.exe [选项]
```

例如，您需要显示迁云工具的版本号，则命令为：

``` {#codeblock_t02_dzh_4eh}
go2aliyun_client.exe --version
```

迁云工具提供的选项及参数说明如下所示。

|选项及参数|说明|
|:----|:-|
|--help|列出迁云工具的使用方法|
|--version|显示迁云工具版本号|
|--nocheckversion|停止提示新版本|
|--noenterkey|迁云结束前不提示输入按键，而是直接退出，减少交互|
|--progressfile|设置迁移进度输出文件。详情请参见[通用参数表](#table_apt_qy1_kfb)|
|--cleardata|清理client\_data数据文件，并释放运行中（Running）的中转实例|
|--accesssid=<accesss\_id\>|设置访问密钥（AccessKey）的AccessKeyId|
|--secretkey=<secret\_key\>|设置访问密钥（AccessKey）的AccessKeySecret|
|--regionid=<region\_id\>|设置迁云的目标地域ID。地域和可用区的详细信息请参见[地域和可用区](../../../../cn.zh-CN/通用参考/地域和可用区.md#)|
|--imagename=<image\_name\>|设置迁云后生成的阿里云ECS镜像名称|
|--systemdisksize=<sdsize\>|设置迁云后目标ECS云服务器的系统盘大小|
|--platform=<platform\>|设置源端服务器的操作系统|
|--architecture=<arch\>|设置源端服务器的架构。 **说明：** 1.5.0及以上版本的迁云工具不再提供该参数

 |
|--datadisks=<data\_disks\>|设置迁云后目标ECS云服务器的数据盘信息 data\_disks=data\_disk\_index|data\_disk\_size|src\_path，示例： data\_disks=1|100|D:;2|150|E:

 |
|--bandwidthlimit=<limit\>|设置迁云时数据传输的带宽|
|--netmode=<net\_mode\>|设置网络模式。详情请参见[net\_mode参数描述](cn.zh-CN/迁移服务/P2V 迁云工具/VPC内网迁云.md#table_hww_qz1_kfb)|
|--vpcid=<vpc\_id\>|已经配置了高速通道服务或者VPN网关的VPC ID|
|--vswitchid=<vswitch\_id\>|指定VPC下的一台虚拟交换机ID|
|--zoneid=<zone\_id\>|设置可用区ID|
|--securegroupid=<sgid\>|设置安全组ID|
|--verbose|显示迁云进度的详细信息|

## Linux版本选项及参数列表 {#section_j4t_qy1_kfb .section}

Linux版迁云工具的使用方法如下：

``` {#codeblock_5kh_gv5_pyg}
# cd <迁云工具所在路径>
# ./go2aliyun_client [选项]
```

例如，迁云工具位于`/root/go2aliyun_client1.5.1.5_linux_x86_64`且您需要清除client\_data，则命令为：

``` {#codeblock_z6b_9r7_fxv}
# cd /root/go2aliyun_client1.5.1.5_linux_x86_64
# ./go2aliyun_client --cleardata
```

迁云工具提供的选项及参数说明如下所示。

|选项及参数|说明|
|:----|:-|
|--help|列出迁云工具的使用方法|
|--version|显示迁云工具版本号|
|--nocheckversion|停止提示新版本|
|--noenterkey|迁云结束前不提示输入按键，而是直接退出，减少交互|
|--progressfile|设置迁移进度输出文件。详情请参见[通用参数表](#table_apt_qy1_kfb)|
|--cleardata|清理client\_data数据文件，并释放运行中（Running）的中转实例|
|--accesssid=<accesss\_id\>|设置访问密钥（AccessKey）的AccessKeyId|
|--secretkey=<secret\_key\>|设置访问密钥（AccessKey）的AccessKeySecret|
|--regionid=<region\_id\>|设置迁云的目标地域ID。地域和可用区的详细信息请参见[地域和可用区](../../../../cn.zh-CN/通用参考/地域和可用区.md#)|
|--imagename=<image\_name\>|设置迁云后生成的阿里云ECS镜像名称|
|--systemdisksize=<sdsize\>|设置迁云后目标ECS云服务器的系统盘大小|
|--platform=<platform\>|设置源端服务器的操作系统|
|--architecture=<arch\>|设置源端服务器的架构。 **说明：** 1.5.0及以上版本的迁云工具不再提供该参数

 |
|--datadisks=<data\_disks\>|设置迁云后目标ECS云服务器的数据盘信息 data\_disks=data\_disk\_index|data\_disk\_size|src\_path， 示例：data\_disks=1|100|/mnt/disk1;2|150|/mnt/disk2

 |
|--bandwidthlimit=<limit\>|设置迁云时数据传输的带宽|
|--netmode=<net\_mode\>|设置网络模式。详情请参见[net\_mode参数描述](cn.zh-CN/迁移服务/P2V 迁云工具/VPC内网迁云.md#table_hww_qz1_kfb)|
|--vpcid=<vpc\_id\>|已经配置了高速通道服务或者VPN网关的VPC ID|
|--vswitchid=<vswitch\_id\>|指定VPC下的一台虚拟交换机ID|
|--zoneid=<zone\_id\>|设置可用区ID|
|--securegroupid=<sgid\>|设置安全组ID|
|--verbose|显示迁云进度的详细信息|

## 通用选项 {#section_z4t_qy1_kfb .section}

以下为Windows和Linux迁云工具的通用选项。常规选项不会影响迁云工具配置，对迁云工作无影响，常用于调整迁云工具的使用习惯和交互界面。

|选项及参数|说明|
|-----|--|
|--nocheckversion|停止提示版本更新。|
|--noenterkey|迁云结束前不提示输入按键，而是直接退出，减少交互。|
|--progressfile|设置迁移进度输出文件，文件内容有两行，格式如下： -   第一行是进度标识，4个标识主要分为准备数据传输阶段`PrepareForRsync`、数据传输阶段`DoRsync`、创建镜像阶段`CreateImage`、完成迁云`Finished`。
-   第二行是进度值表示每一阶段的进度。取值为Integer，范围为\[0, 100\]。

 |
|--cleardata|清理client\_data数据文件，并释放**运行中**（`Running`）的中转实例。|

**警告：** 当您的迁云工作还未完成前，请慎重使用`--cleardata`选项。否则会导致迁云中断，已迁移的进度会被作废。

## user\_config参数 {#section_fpt_qy1_kfb .section}

以下为配置user\_config的相关CLI选项及参数，更多有关user\_config的信息，请参见[使用迁云工具](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)。

**说明：** 使用CLI选项及参数指定了user\_config的配置后，迁云工具会以CLI选项参数为准，而忽略配置文件。

|选项及参数|说明|
|:----|:-|
|--accesssid=<accesss\_id\>|设置user\_config中的AccessKey ID|
|--secretkey=<secret\_key\>|设置user\_config中的AccessKey Secret|
|--regionid=<region\_id\>|设置user\_config中配置的地域ID|
|--imagename=<image\_name\>|设置user\_config中的自定义镜像名称|
|--systemdisksize=<sdsize\>|设置user\_config中的系统盘容量|
|--platform=<platform\>|设置user\_config中的源服务器操作系统|
|--architecture=<arch\>|设置user\_config中的源服务器系统架构。 **说明：** 1.5.0及以上版本的迁云工具不再提供该参数

 |
|--datadisks=<data\_disks\>|设置user\_config中的数据盘列表，由|和;分隔不同数据盘取值，例如data\_disk\_index|data\_disk\_size|src\_path;|
|--bandwidthlimit=<limit\>|设置设置user\_config中迁云时数据传输的带宽|

## client\_data参数 {#section_opt_qy1_kfb .section}

以下为指定VPC内网迁移相关选项及参数。更多详情，请参见[VPC内网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/VPC内网迁云.md#)。

|选项及参数|说明|
|:----|:-|
|--netmode=<net\_mode\>|设置client\_data中的迁云方式，取值可以是0、1和2|
|--vpcid=<vpc\_id\>|设置client\_data中配置了高速通道或者VPN网关的VPC ID|
|--vswitchid=<vswitch\_id\>|设置client\_data中VPC下的虚拟交换机|
|--securegroupid=<sgid\>|设置client\_data中VPC下的安全组|

