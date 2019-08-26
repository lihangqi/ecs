# ECS 实例常用端口介绍 {#concept_gbt_s21_ydb .concept}

以下为 ECS 实例常用端口列表：

|端口|服务|说明|
|21|FTP|FTP 服务所开放的端口，用于上传、下载文件。|
|22|SSH|SSH 端口，用于通过命令行模式 [使用用户名密码验证连接 Linux 实例](intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接 Linux 实例.md#)。|
|23|Telnet|Telnet 端口，用于 Telnet 远程登录 ECS 实例。|
|25|SMTP|SMTP 服务所开放的端口，用于发送邮件。基于安全考虑，ECS 实例 25 端口默认受限，请提交工单申请解封，请参阅 [TCP 25 端口控制台解封申请](https://www.alibabacloud.com/help/doc-detail/56130.htm)。

|
|80|HTTP|用于 HTTP 服务提供访问功能，例如，IIS、Apache、Nginx 等服务。您可以参阅 [检查 TCP 80 端口是否正常工作](https://www.alibabacloud.com/help/faq-detail/59367.htm) 排查 80 端口故障。

|
|110|POP3|用于 POP3 协议，POP3 是电子邮件收发的协议。|
|143|IMAP|用于 IMAP（Internet Message Access Protocol）协议，IMAP 是用于电子邮件的接收的协议。|
|443|HTTPS|用于 HTTPS 服务提供访问功能。HTTPS 是一种能提供加密和通过安全端口传输的一种协议。|
|1433|SQL Server|SQL Server 的 TCP 端口，用于供 SQL Server 对外提供服务。|
|1434|SQL Server|SQL Server 的 UDP 端口，用于返回 SQL Server 使用了哪个 TCP/IP 端口。|
|1521|Oracle|Oracle 通信端口，ECS 实例上部署了 Oracle SQL 需要放行的端口。|
|3306|MySQL|MySQL 数据库对外提供服务的端口。|
|3389|Windows Server Remote Desktop Services|Windows Server Remote Desktop Services（远程桌面服务）端口，可以通过这个端口 [使用软件连接Windows实例](intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。|
|8080|代理端口|同 80 端口一样，8080 端口常用于 WWW 代理服务，实现网页浏览。如果您使用了 8080 端口，访问网站或使用代理服务器时，需要在 IP 地址后面加上 `:8080`。安装 Apache Tomcat 服务后，默认服务端口为 8080。|
|137、138、139|NetBIOS 协议|-   137、138 为 UDP 端口，通过网上邻居传输文件时使用的端口。
-   139 通过这个端口进入的连接试图获得 NetBIOS/SMB 服务。

NetBIOS 协议常被用于 Windows 文件、打印机共享和 Samba。|

## 无法访问某些端口 {#section_whp_ff1_ydb .section}

现象：ECS 实例监听了对应端口，但这个端口在部分地区无法访问，而其它端口访问正常的情况。

分析：部分运营商判断端口 135、139、444、445、5800、5900 等为高危端口，默认被屏蔽。

解决：建议您修改敏感端口为其它非高危端口承载业务。

## 参考链接 {#section_b1p_qf1_ydb .section}

-   更多关于 Windows 实例服务端口说明，请参阅微软文档 [Windows 服务器系统的服务概述和网络端口要求](https://support.microsoft.com/zh-cn/kb/832017)。
-   如何通过安全组放行服务端口，请参阅 [添加安全组规则](intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。

