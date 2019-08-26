# Typical applications of commonly used ports {#concept_gbt_s21_ydb .concept}

If you know the commonly used ports of ECS instances, you can add and modify security group rules more accurately. This topic describes commonly used ports of ECS instances and the typical applications of these ports.

## Commonly used ports {#section_vz4_ptr_lgb .section}

|Port|Service|Description|
|:---|:------|:----------|
|21|FTP|A port opened to the FTP service. The port is used to upload and download files.|
|22|SSH|SSH port, which is used to [connect to a Linux instance by using a password](reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Linux instance by using a password.md#) in the command line mode.|
|23|Telnet|Telnet port, which is used to telnet to the ECS instance.|
|25|SMTP|A port opened to the SMTP service. The port is used to send emails.For security purposes, ECS instances are disabled to access port 25. If you want to enable ECS instances to access this port, see [Apply to enable TCP port 25](https://partners-intl.aliyun.com/help/doc-detail/56130.htm).

|
|80|HTTP|This port provides access to HTTP services, such as IIS, Apache, and Nginx.For more information, see [Verify if TCP port 80 works properly](https://partners-intl.aliyun.com/help/faq-detail/59367.htm).

|
|110|POP3|This port is used for the POP3 protocol to send and receive emails.|
|143|IMAP|This port is used for the IMAP protocol to receive emails.|
|443|HTTPS|This port is used to provide access to the HTTPS service. HTTPS is a protocol that provides encryption and transmission through secure ports.|
|1433|SQL Server|The TCP port of the SQL Server. This port is used for the SQL Server to provide external services.|
|1434|SQL Server|The UDP port of the SQL Server. This port is used to return which TCP/IP port the SQL Server uses.|
|1521|Oracle|An Oracle communication port. This port needs to be enabled when Oracle SQL is deployed on the ECS instance.|
|3306|MySQL|The port through which the MySQL database provides external services.|
|3389|Windows Server Remote Desktop Services|This port is used to [connect to a Windows instance](reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Windows instance.md#).|
|8080|Proxy port|Similar to port 80, port 8080 is used by WWW agents to browse webpages. If you use port 8080 to access a website or use a proxy server, you must add `:8080` after the IP address. If you install the Apache Tomcat service, the default service port is 8080.|
|137, 138, and 139|NetBIOS protocol|-   Ports 137 and 138 are UDP ports used to transfer files through the network neighbor.
-   Port 139 provides access to the NetBIOS/SMB service.

The NetBIOS protocol is often used for Windows files, printer sharing, and Samba.|

## Typical applications of commonly used ports {#section_wx4_4cl_ngb .section}

|Scenario|Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
|:-------|:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
|Remote access to Linux instances through SSH|VPC|Configuration is not required.|Inbound|Allow|SSH \(22\)|22/22|Address field access|0.0.0.0/0|1|
|Classic network|Internet|
|Remote access to Windows instances through RDP|VPC|Configuration is not required.|Inbound|Allow|RDP \(3389\)|3389/3389|Address field access|0.0.0.0/0|1|
|Classic network|Internet|
|Ping ECS instances through the Internet|VPC|Configuration is not required.|Inbound|Allow|ICMP|-1/-1|Address field access or security group access|Set this parameter according to the authorization type.|1|
|Classic network|Internet|
|Use an ECS instance as a Web server.|VPC|Configuration is not required.|Inbound|Allow|HTTP \(80\)|80/80|Address field access|0.0.0.0/0|1|
|Classic network|Internet|
|Upload or download files through FTP.|VPC|Configuration is not required.|Inbound|Allow|Custom TCP|20/21|Address field access|0.0.0.0/0|1|
|Classic network|Internet|

**Note:** 

-   Some operators consider ports 135, 139, 444, 445, 5800, and 5900 as high-risk ports and block these ports by default. Therefore, even if the ports are enabled for ECS instances, the ports cannot be accessed in some regions. We recommend that you use non-high-risk ports to meet your specific service needs.
-   For more information about Windows instance service ports, see [Service overview and network port requirements for Windows](https://support.microsoft.com/zh-cn/kb/832017).

