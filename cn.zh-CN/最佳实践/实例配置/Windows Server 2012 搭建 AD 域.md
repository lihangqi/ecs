# Windows Server 2012 搭建 AD 域 {#concept_g11_p3v_hfb .concept}

Active Directory（简称AD，即" 活动目录"的意思），是微软服务的核心组件，其主要优势是实现高效管理，例如批量管理用户、部署应用和更新补丁等。许多微软组件例如 Exchange 和故障转移群集也需要 AD 域环境。本文通过 Windows Server 2012 实例示范如何搭建 AD 域。

## 名词解释 {#section_lvc_53v_hfb .section}

-   Domain Controllers（DC）：域控制器

-   Organizational Unit（OU）：组织单位

-   Distinguished name（DN）：识别名

-   Canonical Name（CN）：正式名称


## 安装指南 {#section_kvc_53v_hfb .section}

**必要条件**

-   安装者必须拥有管理员权限。

-   安装分区为NTFS分区。

-   需要支持DNS。

-   需要支持TCP/IP协议，并且需要有固定IP。任何服务器都应该使用固定IP，防止重启实例后IP地址发生变化。本文采用是阿里云VPC网络，手动修改IP会导致IP失效，如果想修改IP，您可以通过控制台修改。


**环境**

网络采用VPC， 虚拟交换机网段为 192.168.100.0/24，并使用网关。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070813272_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913271_zh-CN.png)

**域名**

-   lyonz.com

-   DC：192.168.100.105

-   需要加入域的客户机（Client）IP：192.168.100.106


![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913273_zh-CN.png)

## 修改DC 的基本信息 {#section_svc_53v_hfb .section}

修改DC主机名

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913274_zh-CN.png)

修改DC 的DNS（将DNS地址指向自己的IP）

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913275_zh-CN.png)

**说明：** 这里不要手动修改服务器的IP地址（手动修改服务器IP不会生效，也无需担心服务器IP会重启发生改变），如果要修改请在控制台操作。

开始安装

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913276_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913277_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913278_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913279_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913280_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913281_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913282_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913283_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976070913284_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013285_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013286_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013287_zh-CN.png)

## 验证客户端的加入 {#section_hwc_53v_hfb .section}

在云上安装AD和我们线下安装AD步骤其实一样，但客户端加入域的步骤稍有不同，需要先修改客户端的SID，这是因为阿里云ECS Windows Server 2012系统采用的同一个镜像，所以SID是相同的，如果不修改，在加入域的时候会提示SID相同。

## 修改客户端的SID {#section_iwc_53v_hfb .section}

Winodws Server 2012：

在 powershell 界面执行如下命令：

首先切换到脚本存放的路径，

```
.\Sysprep.ps1 -ReserveHostname -ReserveNetwork -skiprearm -post_action "reboot"
```

执行上面的命令后，服务器会重新初始化SID，初始化完成后，机器会重启，服务器启动后需要注意两点：

（1）服务器IP地址会从DHCP变成固定IP地址，这里你可以重新改成DHCP，我前面说过，如果想修改ECS 的地址最好从控制台操作。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013288_zh-CN.png)

（2）服务器无法PING 通，这是因为服务器SID初始化完成后，也将服务器防火墙的配置修改成微软默认的配置，也就是将"来宾或公用网络"打开，导致无法ping 通服务器和远程。这个时候我们就需要在web console 界面将防火墙"来宾或公用网络"关闭，或者放行需要开放的端口。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013289_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013290_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013291_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013292_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013293_zh-CN.png)

## 修改客户端的基本信息 {#section_qwc_53v_hfb .section}

DNS 指向 DC 的IP地址，您可以根据业务需求修改主机名。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013294_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013295_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9810/153976071013296_zh-CN.png)

以上就是阿里云ECS Windows Server 2012 搭建域以及客户端加入域的过程，如果您已经在线下或者虚拟机搭建了 AD 域，在阿里云上搭建 AD 域时需要注意修改客户端SID。

## 相关链接 {#section_uwc_53v_hfb .section}

-   [域控常见问题配置](https://help.aliyun.com/knowledge_list/42491.html?spm=5176.7740846.6.774.orvkCg)

-   更多开源软件尽在[云市场](https://market.aliyun.com/software)


