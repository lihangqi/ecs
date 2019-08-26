# 更新虚拟驱动\_Windows {#concept_v4p_2xs_dhb .concept}

阿里云支持对云盘在线扩容，即无需重启实例便可以完成扩容云盘。如果您的实例创建时间早于2019.03.30日且有在线扩容需求，请根据本文描述检查是否需要更新RedHat VirtIO SICI驱动。

## 使用说明 {#section_vhd_23y_dhb .section}

-   驱动仅支持Windows Server 2008及更高版本操作系统。
-   如果Windows实例的数据盘数量较多，可能需要1-2分钟完成驱动的更新。

## 下载驱动程序 {#section_vsy_j3y_dhb .section}

下载并解压[instdrv系列驱动包](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/25367/APP_zh/1553675201254/instdrv.zip)，实例的操作系统与解压后文件夹目录的对应关系如下表所示。

|驱动文件（夹）名称|文件（夹）描述|
|:--------|:------|
|win7|Windows 7|
|Wlh|Windows 2008|
|Win8|Windows 2012|
|win10|Windows 2016/1709/10|
|amd64|64位|
|x86|32位|
|instdrv.exe|检查实例是否支持在线扩容的程序|

## 检查驱动版本 {#section_mhl_nhy_dhb .section}

**方式一：使用instdrv.exe检查驱动版本** 

1.  [远程连接Windows实例](../../../../../intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)
2.  打开CMD命令行窗口。
3.  进入instdrv.exe所在的路径，如`cd C:\\User|lizr\\Desktop\\instdrv\\`。
4.  （可选）运行instdrv.exe查看工具使用说明，运行`instdrv.exe -v`可以查看工具版本号。
5.  运行`instdrv.exe -c`，根据返回信息判断操作系统是否支持在线扩容。若支持，您可以直接[在线扩容云盘](intl.zh-CN/隐藏/ECS Conref仓库/在线扩容云盘.md#)。否则您需要[更新RedHat VirtIO SICI驱动](#)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155529734241813_zh-CN.png)


**方式二：手动检查驱动版本** 

1.  远程连接Windows实例。
2.  进入系统目录C:\\Windows\\System32\\drivers。
3.  右键单击viostor.sys文件，选择**属性**，查看 **详细信息** \> **文件版本号** 。如果Windows Server的Red Hat Vir文件版本大于等于58011，您可以直接[在线扩容云盘](intl.zh-CN/隐藏/ECS Conref仓库/在线扩容云盘.md#)。文件版本小于58011时，请[更新RedHat VirtIO SICI驱动](#)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155529734341818_zh-CN.png)


## 更新RedHat VirtIO SICI驱动 {#section_pvf_cr1_qgb .section}

**方式一：使用pnputil添加驱动** 

1.  打开CMD命令行窗口。
2.  进入viostor.inf所在的路径，如`cd C:\\Users\\Administrator\\Desktop\\amd`。
3.  运行`pnputil –i –a <directory\>`添加驱动包，请确保您已经将目标.inf文件解压到指定的目录（<directory\>）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155529734341303_zh-CN.png)

4.  在控制台重启实例，或者使用API（[RebootInstance](../../../../../intl.zh-CN/API参考/实例/RebootInstance.md#)）重启实例，使得驱动更新生效。

**方式二：手动添加驱动** 

1.  打开设备管理器。
2.  右键单击**存储控制器**下的**Red Hat Vir**，并选择**更新驱动程序软件**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155529734341810_zh-CN.png)

3.  选择**浏览计算机以查找驱动程序软件**。
4.  选择**从计算机的设备驱动程序列表中选择**。
5.  单击**从磁盘安装**。
6.  选择对应文件夹下的驱动文件viostor，并按向导提示更新驱动。
7.  在控制台重启实例，或者使用API（[RebootInstance](../../../../../intl.zh-CN/API参考/实例/RebootInstance.md#)）重启实例，使得驱动更新生效。

## 下一步 {#section_kj1_ssy_dhb .section}

[在线扩容云盘](intl.zh-CN/隐藏/ECS Conref仓库/在线扩容云盘.md#)

