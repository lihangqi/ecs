# Introduction to common ECS instance ports {#concept_gbt_s21_ydb .concept}

The following table lists commonly used ECS instance ports.

|Port|Service|Description|
|21|FTP|A port opened by the FTP service is used for uploading and downloading files.|
|22|SSH|An SSH port is used to [connect to a Linux instance by using a password](intl.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#) in command-line mode.|
|23|Telnet|The Telnet port is used for Telnet to log on to the ECS instance.|
|25|SMTP|The port that is open to the SMTP service is used for sending mails.Based on security concerns, ECS instance Port 25 is restricted by default. See [apply to open TCP port 25](https://www.alibabacloud.com/help/doc-detail/56130.htm)to remove the limit.

|
|80|HTTP|Provides access to HTTP services, such as IIS, Apache, and Nginx.We recommend that you [verify if TCP port 80 works properly](https://www.alibabacloud.com/help/faq-detail/59367.htm) .

|
|110|POP3|A port used for the POP3 protocol, which is a protocol for sending and receiving emails.|
|143|IMAP|A port used for IMAP \(Internet Message Access Protocol\), which is a protocol for receiving emails.|
|443|HTTPS|A port used to provide access to the HTTPS service. HTTPS is a protocol that provides encryption and transmission through secure ports.|
|1433|SQL Server|The TCP port of the SQL Server that is used for external service by SQL Server.|
|1434|SQL Server|The SQL Server UDP port that is used to return which TCP/IP port SQL Server uses.|
|1521|Oracle|An Oracle communications port. The port that needs to be released by Oracle SQL is deployed on the ECS instance.|
|3306|MySQL|The port through which the MySQL database provides external service.|
|3389|Windows Server Remote Desktop Services|The Windows Server Remote Desktop Services port can be used to [connect to a Windows instance](intl.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).|
|8080|Proxy port|Similar to 80 port, port 8080 is used by WWW agents to enable web browsing. If you are using port 8080, when you visit a Web site or use a proxy server, you must add `:8080` after the IP Address: 8080. If you install the Apache Tomcat service, the default service port is 8080.|
|137, 138, 139|NetBIOS protocol|-   Ports 137 and 138 are UDP ports that are used to transfer files through the network neighbor.
-   The connection entering through the port 139 attempts to obtain the NetBIOS/smb service.

NetBIOS protocols are often used for Windows files, printer sharing, and samba.|

## Some ports cannot be accessed {#section_whp_ff1_ydb .section}

Issue: An ECS instance attempts to listen for the corresponding port, but the port is not accessible, while other ports can be accessed normally.

Cause: Some operators determine that port numbers 135, 139, 444, 445, 5800, 5900, and related ports, are high-risk ports, which are then blocked by default.

Resolution: We recommend that you change the port to another port number

## Related topic {#section_b1p_qf1_ydb .section}

For more information on how to release a service port through a security group, see [add security group rules](intl.en-US/User Guide/Security groups/Add security group rules.md#).

