# CLI参数 {#CliParams .reference}

迁云工具从1.2.8版本开始支持命令行（Command line interface，CLI）参数，在迁云工具所在路径中运行`--help`可以查看参数列表。CLI参数具有无需打开各种JSON文件就能配置迁云工具、调整自定义使用习惯和一键清除client\_data等优点。如果您使用的是旧版本迁云工具，请重新 [下载压缩包](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip) 以获取更多功能。CLI参数需要您对迁云工具的使用方式有所了解，更多详情，请参阅 [使用迁云工具](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#)。

## Windows版本参数列表 {#section_tnt_qy1_kfb .section}

以下为Windows版迁云工具完整的CLI参数列表。

```
usage: go2aliyun_client.exe [options]
options:
  --help                        show usage.
  --version                     show version.
  --nocheckversion              no check for new version.
  --noenterkey                  no enter key to exit.
  --progressfile                set progress file path.
  --cleardata                   clear client data and server ecs.
  --accesssid=<accesss_id>      set access id.
  --secretkey=<secret_key>      set secret key.
  --regionid=<region_id>        set region id.
  --imagename=<image_name>      set image name.
  --systemdisksize=<sdsize>     set system disk size.
  --platform=<platform>         set platform.
  --architecture=<arch>         set architecture.
  --datadisks=<data_disks>      set data disks.
    data_disks=data_disk_index|data_disk_size|src_path;
    e.g. --data_disks=1|100|D:;2|150|E:
  --bandwidthlimit=<limit>      set bandwidth limit.
  --netmode=<net_mode>          set net mode.
  --vpcid=<vpc_id>              set vpc id.
  --vswitchid=<vswitch_id>      set vswitch id.
  --zoneid=<zone_id>            set zone id.
  --securegroupid=<sgid>        set secure group id.
```

## Linux版本参数列表 {#section_j4t_qy1_kfb .section}

以下为Linux版迁云工具完整的CLI参数列表。

```
usage: ./go2aliyun_client [options]
options:
  --help                       show usage.
  --version                    show version.
  --nocheckversion             no check for new version.
  --noenterkey                 no enter key to exit.
  --progressfile               set progress file path. 
  --cleardata                  clear client data and server ecs.
  --accesssid=<accesss_id>     set access id.
  --secretkey=<secret_key>     set secret key.
  --regionid=<region_id>       set region id.
  --imagename=<image_name>     set image name.
  --systemdisksize=<sdsize>    set system disk size.
  --platform=<platform>        set platform.
  --architecture=<arch>        set architecture.
  --datadisks=<data_disks>     set data disks.
    data_disks=data_disk_index|data_disk_size|src_path;
    e.g. --data_disks=1|100|/mnt/disk1;2|150|/mnt/disk2
  --bandwidthlimit=<limit>     set bandwidth limit.
  --netmode=<net_mode>         set net mode.
  --vpcid=<vpc_id>             set vpc id.
  --vswitchid=<vswitch_id>     set vswitch id.
  --zoneid=<zone_id>           set zone id.
  --securegroupid=<sgid>       set secure  group id.
```

## 常规参数 {#section_z4t_qy1_kfb .section}

以下为Windows和Linux迁云工具的通用参数。常规参数不会影响迁云工具配置，对迁云工作无影响，常用于调整迁云工具的使用习惯和交互界面。

|参数|说明|
|--|--|
|nocheckversion|停止提示版本更新。|
|noenterkey|迁云结束前不提示输入按键，而是直接退出，减少交互。|
|progressfile|设置迁移进度输出文件，文件内容有两行，格式如下：-   第一行是进度标识，4个标识主要分为准备数据传输阶段`PrepareForRsync`、数据传输阶段`DoRsync`、创建镜像阶段`CreateImage`、完成迁云`Finished`。
-   第二行是进度值表示每一阶段的进度。取值为Integer，范围为\[0, 100\]。

|
|cleardata|清理client\_data数据文件，并释放 **运行中**（`Running`）的中转实例。|

**警告：** 当您的迁云工作还未完成前，请慎重使用`cleardata`参数。否则会导致迁云中断，已迁移的进度会被作废。

## user\_config参数 {#section_fpt_qy1_kfb .section}

以下为配置user\_config的相关CLI参数，更多有关user\_config的信息，请参阅 [使用迁云工具](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#)。

**说明：** 使用CLI参数指定了user\_config的配置后，迁云工具会以CLI参数为准，而忽略配置文件。

```
--accesssid=<accesss_id>     # 设置user_config中的AccessKey ID
--secretkey=<secret_key>     # 设置user_config中的AccessKey Secret
--regionid=<region_id>       # 设置user_config中的地域配置
--imagename=<image_name>     # 设置user_config中的自定义镜像名称
--systemdisksize=<sdsize>    # 设置user_config中的系统盘容量
--platform=<platform>        # 设置user_config中的镜像发行平台
--architecture=<arch>        # 设置user_config中的镜像系统架构
--datadisks=<data_disks>     # 设置user_config中的数据盘列表，由|和;分隔不同数据盘取值，例如data_disk_index|data_disk_size|src_path;
--bandwidthlimit=<limit>     # 设置user_config中的公网出带宽上限
```

## client\_data参数 {#section_opt_qy1_kfb .section}

以下为指定VPC内网迁移相关参数。更多详情，请参阅 [VPC内网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/VPC内网迁云.md#)。

```
--netmode=<net_mode>        # 设置client_data中的迁云方式，取值可以是0、1和2
--vpcid=<vpc_id>            # 设置client_data中配置了高速通道或者VPN网关的VPC
--vswitchid=<vswitch_id>    # 设置client_data中VPC下的虚拟交换机
--securegroupid=<sgid>      # 设置client_data中VPC下的安全组
```

