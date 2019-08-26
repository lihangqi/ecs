# 设置Windows操作系统首选语言 {#task_eyb_syt_hfb .task}

本文使用公共镜像中的Windows Server 2016英语版操作系统为例，从Windows更新下载语言资源包，为一台ECS实例重新设置首选语言。

云服务器ECS仅提供中文版和英文版的Windows Server公共镜像。如果您需要使用其他语言版本，如阿拉伯语、德语、俄语或日语等，可以根据本文设置ECS实例的首选语言。本文为德语为示范步骤，适用于Windows Server 2012及其以上的版本操作系统。创建使用德语和德语键盘设置的自定义镜像后，您可以使用该自定义镜像根据自身需求创建任意数量的实例。

1.  连接Windows实例。连接方式请参见[连接方式导航](../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
2.  打开PowerShell模块。
3.  运行以下命令临时禁用WSUS（Windows Server Update Services）更新源。 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0
    Restart-Service -Name wuauserv
    ```

4.  找到控制面板，单击**Clock, Language, and Region** \> **Language** \> **Add a language**。
5.  在Add languages对话框中，选择一种语言，例如**Deutsch \(German\)** \> **Deutsch \(Deutschland\)**，单击**Add**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/155869123113242_zh-CN.png)

6.  选择语言，例如**Deutsch \(Deutschland\)**，单击**Move up**更改语言优先级。
7.  单击所选语言右侧的**Options**，在线检查语言更新。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/155869123113243_zh-CN.png)

8.  等待实例检查更新，大约三分钟后更新会提示可供下载，单击**Download and install language pack**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/155869123113244_zh-CN.png)

9.  等待安装完成。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/155869123113245_zh-CN.png)

10. 在ECS控制台[重新启动实例](../cn.zh-CN/实例/管理实例/重启实例.md#)。
11. 再次连接Windows实例。 显示语言会在重启登录后更改为德语。
12. 打开PowerShell ISE模块，运行以下命令重新启用WSUS。 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1
    Restart-Service -Name wuauserv                    
    ```

13. 打开**Windows Update**，检查安全更新，重新安装配置语言设置之前已完成的所有安全更新。

您可以使用相同语言设置创建多台实例：

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com/)。
2.  根据该Windows实例[创建自定义镜像](../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。
3.  [通过自定义镜像创建指定数量的实例](../cn.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。

