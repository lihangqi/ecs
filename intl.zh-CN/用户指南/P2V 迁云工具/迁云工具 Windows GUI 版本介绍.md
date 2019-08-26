# 迁云工具 Windows GUI 版本介绍 {#reference_ngp_fx1_kfb .reference}

迁云工具从 1.2.9 版本开始支持 Windows GUI 版本，程序文件名为go2aliyun\_gui.exe。如果您使用的是旧版本迁云工具，请重新 [下载](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip) 压缩包以获取更多功能。迁云工具 Windows GUI 界面的设置与命令行界面配置原理一致，并且 Windows GUI 版本与命令行界面运行过程兼容，您可以在使用迁云工具的过程中切换使用方式。

## 界面介绍 {#section_bxm_gx1_kfb .section}

迁云工具 Windows GUI 界面有四块区域组成，包括菜单栏、用户自定义配置（user\_config.json）编辑区、磁盘列表和任务进度与日志区。如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22628/153949499613345_zh-CN.png)

## 图标说明 {#section_vjd_yx1_kfb .section}

-   菜单栏，由 **Config**、**Logs** 和 **Help** 三个功能页组成。

-   用户自定义配置（user\_config.json）编辑区，主要用于配置源服务器的一些必要配置信息，其中包括您的 AccessKey 信息、源服务器的操作系统信息、系统盘大小、源服务器迁移入阿里云的地域 ID、生成 ECS 镜像后的名称以及生成的目标自定义镜像的配置信息等。更多详情，请参阅 *使用迁云工具* [编辑 user\_config.json](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#)。

-   磁盘列表，包括系统盘和数据盘。您可以在该区域通过右键单击添加需要迁云的磁盘，双击进入磁盘信息编辑页面。

-   任务进度与日志区，运行迁云工具后，您可以通过该区域查看任务进度与或者根据界面提示排查故障。

-   菜单栏之一，您可以在这里单击 **Rsync** 设置数据传输的带宽上限值，单位为 KB/s，单击 **Save User Config** 保存当前的页面设置便于批量操作，单击 **Clear Client Data** 一键初始化客户端配置文件，更多详情，请参阅 [使用迁云工具](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#)。

-   菜单栏之一，您可以在这里单击 **Open Log File** 快速打开日志文件，或者单击 **Open Log Dir** 查找日志文件所在路径。

-   菜单栏之一，您可以在这里获取在线文档或者迁云工具版本信息。

-   您可以在这里添加数据盘。迁云工具会自动查询您的服务器里的数据盘盘符列表，显示已使用数据盘空间。数据盘大小设置需要大于源服务器数据盘实际占用大小，例如，源数据盘大小为 500 GiB，实际占用 100 GiB，那么您只要设置成大于 100 GiB 即可。


在 GUI 界面上完成服务器信息配置后，您可以单击 **Start** 开始迁云工作。当任务进度与日志区出现 `Goto Aliyun Finished!` 提示时，前往 [ECS管理控制台](https://ecs.console.aliyun.com/) 镜像详情页查看结果。当出现 `Goto Aliyun Not Finished!` 提示时，通过菜单功能页 **Logs** 检查同日志文件 [排查故障](intl.zh-CN/最佳实践/P2V 迁云实践/问题与报错排查.md#)。修复问题后，重新运行迁云工具即可恢复迁云工作，迁云工具会从上一次执行的进度中继续迁云，无需重新开始。

