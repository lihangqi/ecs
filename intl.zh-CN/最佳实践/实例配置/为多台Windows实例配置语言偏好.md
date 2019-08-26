# 为多台Windows实例配置语言偏好 {#task_eyb_syt_hfb .task}

本文使用公共镜像中的Windows Server 2016英语版操作系统为例，从Windows更新下载德语资源包，为多台实例设置德语语言偏好。创建使用德语和德语键盘设置的自定义镜像后，您可以使用该自定义镜像根据需要创建任意数量的实例。

目前，阿里云ECS仅提供中文版和英文版的 Windows Server 镜像。如果要使用其他语言版本，如阿拉伯语、德语或俄语，可以按照本文设置和部署 ECS 实例。

1.  [连接到 Windows 实例](../intl.zh-CN/用户指南/连接实例/连接实例概述.md#)。 
2.  打开 PowerShell 模块。 
3.  运行以下命令以临时禁用 WSUS。 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0
    Restart-Service -Name wuauserv
    ```

4.  找到控制面板，单击 **Clock, Language, and Region** \> **Language** \> **Add a language**。 
5.  在Add languages对话框中，选择一种语言，例如**Deutsch \(German\)** \> **Deutsch \(Deutschland\)**，然后单击**Add**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756113242_zh-CN.png)

6.  选择语言，例如 **Deutsch \(Deutschland\)**，然后单击**Move up**以更改语言优先级。 
7.  单击所选语言旁边的**Options**以在线检查语言更新。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756113243_zh-CN.png)

8.  实例检查更新需等待大约 3 分钟。更新可供下载后，请单击**Download and install language pack**，然后等待安装完成。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756113244_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756113245_zh-CN.png)

9.  [重新启动实例](../intl.zh-CN/用户指南/实例/重启实例.md#)，显示语言会在下次登录时更改。 
10. 再次 [连接到 Windows 实例](../intl.zh-CN/用户指南/连接实例/连接实例概述.md#)。显示语言现在为德语。 
11. 打开 PowerShell ISE 模块，然后运行以下命令重新打开 WSUS。 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1
    Restart-Service -Name wuauserv
    
    ```

12. 打开**Windows Update**，检查安全更新，并重新安装配置语言设置之前已完成的所有安全更新。 

使用相同语言设置创建多台实例：

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com/)。
2.  根据该Windows实例[创建自定义镜像](../intl.zh-CN/用户指南/镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。
3.  [通过自定义镜像创建指定数量的实例](../intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756113247_zh-CN.png)


