# 时间设置：设置Windows实例NTP服务 {#TimeCalibrationWindows .concept}

网络时间协议（Network Time Protocol，NTP）是用来同步网络中各个计算机的时间的协议。一些对时间极度敏感的应用（例如，通信行业的应用）, 如果不同机器时间不一致，就可能导致读取到不同的值。您可以使用NTP服务同步网络中所有服务器的时钟。目前，所有地域的阿里云ECS实例的默认时区为CST（China Standard Time），您可以根据自己的业务需求并参照本文为ECS实例设置或者修改时区。

本文以Windows Server 2008 R2企业版64位为例，说明如何使用NTP服务同步Windows实例的时间。

Windows Server操作系统默认开启Windows Time服务。为了保证NTP服务配置成功后能正常同步时间，实例中必须开启NTP服务。按以下步骤检查并开启NTP服务：

1.   [远程连接Windows实例](../../../../intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。选择 **开始** \> **所有程序** \> **附件** \> **运行**，打开 运行 对话框，并运行命令 `services.msc`。
2.  在 服务 窗口，找到并双击 **Windows Time** 服务。
3.  在 Windows Time的属性\(本地计算机\) 对话框中，执行以下操作：

    1.  将 **启动类型** 设置为 **自动**。
    2.  确认 **服务状态** 为 **已启动**。如果不是，单击 **启动**。
    完成设置后，单击 **应用**，并单击 **确定**。

    ![开启Windows Time服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9806/154096395313081_zh-CN.png)


## 修改默认NTP服务器地址 { .section}

Windows Server操作系统默认都配置微软默认的NTP服务器（time.windows.com），但是因为网络的原因可能经常同步出错。使用阿里云ECS实例时，您可以将默认的NTP服务器更换成阿里云提供的内网NTP服务器。具体信息，请参考 [时间配置：NTP服务器与其他基础服务](intl.zh-CN/最佳实践/实例配置/时间配置：NTP服务器与其他基础服务.md#)。按以下步骤修改默认的NTP服务器地址：

1.   [远程连接Windows实例](../../../../intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。
2.  在任务栏的通知区域，单击日期和时间，并单击 **更改日期和时间设置**。
3.  在 日期和时间 对话框里，单击 **Internet 时间** 选项卡，并单击 **更改设置**。
4.  在 Internet 时间设置 对话框里，选择 **与Internet时间服务器同步**，填写一个阿里云内网NTP服务器地址（详细列表请参考 [时间配置：NTP服务器与其他基础服务](intl.zh-CN/最佳实践/实例配置/时间配置：NTP服务器与其他基础服务.md#)），并单击 **立即更新**。

界面会提示是否同步成功。

## 修改NTP同步的间隔 { .section}

NTP同步的间隔默认是5分钟。按以下步骤修改NTP同步时间间隔：

1.  [远程连接Windows实例](../../../../intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。
2.  选择 **开始** \> **所有程序** \> **附件** \> **运行**，打开 运行 对话框，并运行命令 `regedit`。
3.  在 注册表编辑器 的左侧目录树中，找到 HKEY\_LOCAL\_MACHINE/SYSTEM/CurrentControlSet/services/W32Time/TimeProviders/NtpClient，并双击SpecialPollInterval键值。
4.  在 编辑 DWORD \(32 位）值 对话框中，在 **基数** 栏里选择 **十进制**，并按需要填写 **数值数据**。填入的数值即是您需要的同步时间间隔。单位为秒。

