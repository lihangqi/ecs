# 配置Windows实例NTP服务 {#TimeCalibrationWindows .concept}

本文介绍如何开启和配置Windows NTP服务，保证实例本地时间精确同步。

## Windows实例NTP服务介绍 {#section_qvw_zxf_qgb .section}

目前，所有地域下ECS实例默认采用CST（China Standard Time）时区，您也可以根据自己的业务需求为ECS实例设置或者修改时区。

本文以Windows Server 2008 R2企业版64位为例，介绍如何使用NTP服务同步Windows实例的本地时间。

## 开启NTP服务 {#section_ozt_sxf_qgb .section}

Windows Server操作系统默认开启Windows Time服务。为了保证NTP服务配置成功后能正常同步时间，实例中必须开启NTP服务。按以下步骤检查并开启NTP服务：

1.   [远程连接Windows实例](../../../../../intl.zh-CN/实例/实例生命周期/连接实例/连接方式导航.md#)。选择 **开始** \> **所有程序** \> **附件** \> **运行**，打开 运行 对话框，并运行命令 `services.msc`。
2.  在 服务 窗口，找到并双击 **Windows Time** 服务。
3.  在 Windows Time的属性\(本地计算机\) 对话框中，执行以下操作：
    1.  将 **启动类型** 设置为 **自动**。
    2.  确认 **服务状态** 为 **已启动**。如果不是，单击 **启动**。

        ![开启Windows Time服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9806/155102411213081_zh-CN.png)

    3.  单击 **应用**，并单击 **确定**。

## 修改默认NTP服务器地址 {#section_b24_55j_ngb .section}

Windows Server操作系统默认配置微软NTP服务器（time.windows.com），但是可能经常同步出错。使用阿里云ECS实例时，您可以将默认NTP服务器更换成阿里云提供的内网NTP服务器。详细的服务器地址，请参考 [使用阿里云NTP服务器](intl.zh-CN/实例/配置实例/配置时间/使用阿里云NTP服务器.md#)。按以下步骤修改默认NTP服务器地址：

1.   [远程连接Windows实例](../../../../../intl.zh-CN/实例/实例生命周期/连接实例/连接方式导航.md#)。
2.  在任务栏的通知区域，单击日期和时间，并单击 **更改日期和时间设置**。
3.  在 日期和时间 对话框里，单击 **Internet 时间** 选项卡，并单击 **更改设置**。
4.  在 Internet 时间设置 对话框里，选择 **与Internet时间服务器同步**，填写一个阿里云内网NTP服务器地址，并单击 **立即更新**。

## 修改NTP服务时间同步间隔 {#section_g24_55j_ngb .section}

NTP服务的时间同步间隔默认是5分钟，您可以根据业务需求自定义同步间隔。按以下步骤修改时间同步间隔：

1.  [远程连接Windows实例](../../../../../intl.zh-CN/实例/实例生命周期/连接实例/连接方式导航.md#)。
2.  选择 **开始** \> **所有程序** \> **附件** \> **运行**，打开 运行 对话框，并运行命令 `regedit`。
3.  在 注册表编辑器 的左侧目录树中，找到 **HKEY\_LOCAL\_MACHINE** \> **SYSTEM** \> **CurrentControlSet** \> **services** \> **W32Time** \> **TimeProviders** \> **NtpClient**，并双击**SpecialPollInterval**键值。
4.  在 编辑 DWORD \(32 位）值 对话框中，在 **基数** 栏里选择 **十进制**，并按需要填写 **数值数据**。填入的数值即是您需要的同步时间间隔（单位为秒）。

