# 高级安全Windows防火墙概述以及最佳实践 {#concept_b1w_sxr_gfb .concept}

本文简单介绍Windows防火墙的概念，给出使用场景并列出了常见的防火墙操作。

## 简介 {#section_sfs_3zr_gfb .section}

在Windows NT6.0之后微软推出了高级安全Windows防火墙\(简称WFAS\)，高级安全Windows防火墙是分层安全模型的重要部分， 通过为计算机提供基于主机的双向网络通讯筛选， 高级安全Windows防火墙 阻止未授权的网络流量流向或流出本地计算机。高级安全 Windows 防火墙 还是用网络感知，以便可以将相应安全设置应用到计算机连接到的网络类型。Windows 防火墙和 Internet 协议保护 \(sec\) 配置设置集成到名为 高级安全 Windows 防火墙 的单个 Microsoft 管理控制台 \(MMC\)，高级安全Windows防火墙也成为网络隔离策略的重要部分。

## 使用场景 {#section_trz_jzr_gfb .section}

作为一个运维人员，越来越多的用户反映服务器被恶意攻击，密码被暴力破解等等，其实大多数原因都是自己给那些“入侵者”留的“后门”导致的。入侵者通过扫描主机开放的端口，一旦发现可以利用的端口，就会进行下一步的入侵，例如Windows的远程端口（3389）和Linux的远程端口（22）。既然知道了问题的关键，那么我们也有相应的对策，我们可以通过修改默认的远程端口以及限制远程的访问来关闭所谓的“后门”。那么如何限制远程访问呢？接下来我们就以阿里云ECS实例Windows Server 2008 R2为例，来实现对远程桌面的限制。

## 操作步骤 {#section_ifj_mzr_gfb .section}

1.  **查看防火墙状态** 

    阿里云ECS实例Windows Server 2008 R2防火墙默认是关闭的，键盘输入Win+R打开运行输入firewall.cpl 回车来打开Windows防火墙控制台，见下图。

    ![](images/12791_zh-CN_source.png)

    选择打开或关闭Windows防火墙。

    ![](images/12792_zh-CN_source.png)

    如下图，我们看到防火墙是默认关闭的。

    ![](images/12793_zh-CN_source.png)

2.  **启用防火墙** 

    还是通过上面的步骤开启防火墙，见下图。

    ![](images/12794_zh-CN_source.png)

    这里需要注意一点的是：启用之前请确认远程端口已经在里面，否则自己也将无法远程，不过高级安全Windows防护墙入站规则默认是放行3389端口的选择高级设置。

    ![](images/12795_zh-CN_source.png)

    选择入站规则，我们看到open port 3389这条入站规则默认是放行3389端口的。

    ![](images/12796_zh-CN_source.png)

3.  **配置高级安全Windows防火墙** 

    键盘输入Win+R打开运行输入wf.msc 回车来打开高级安全Windows防火墙，如下图。

    ![](images/12797_zh-CN_source.png)

    1.  **通过手工新建入站规则**

        ![](images/12798_zh-CN_source.png)

        在弹出的新建入站规则向导窗口，选择 端口 然后鼠标左键单击下一步。

        ![](images/12799_zh-CN_source.png)

        而后选择 TCP 并设置特定本地端口3389。

        ![](images/12800_zh-CN_source.png)

        下一步选择允许链接。

        ![](images/12801_zh-CN_source.png)

        下一步 默认配置即可。

        ![](images/12802_zh-CN_source.png)

        下一步 填写规则名称，例如 RemoteDesktop ,最后鼠标左键单击完成。

        ![](images/12803_zh-CN_source.png)

        看到我们刚刚添加的规则。

        ![](images/12804_zh-CN_source.png)

        以上步骤就是把Windows远程端口加入到高级安全Windows防火墙了，但是依然没有实现我们的限制访问，接下来我们来实现访问限制。

    2.  **配置作用域** 

        右键选中我们刚刚创建的入站规则，然后选择属性\>作用域\>远程IP地址\>添加（将需要远程此服务器的IP地址填写进去，注意：一旦启用作用域，除了作用域里面的IP地址，别的地址将无法远程链接此服务器）。

        ![](images/12805_zh-CN_source.png)

        添加远程IP地址。

        ![](images/12806_zh-CN_source.png)

    3.  **验证作用域** 

        我们在作用域——远程IP地址里面随便写个地址，看看远程连接会发生什么。

        ![](images/12807_zh-CN_source.png)

        远程连接断掉。

        ![](images/12808_zh-CN_source.png)

        如果远程连接没有断开，让我们把下图中open port 3389这条入站规则禁用掉就可以了。

        ![](images/12809_zh-CN_source.png)

        远程连接自己断开了，这就说明我们的作用域生效了，那现在自己都无法远程了，怎么办呢？别急，我们还有阿里云控制台，登录阿里云控制台，然后将上面的作用域地址换成自己的地址（这里要写办公环境的公网地址，除非您的办公环境和阿里云线上的环境打通，）就可以正常远程了。

        进入阿里云的控制台界面，找到相应实例打开远程连接。

        ![](images/12810_zh-CN_source.png)

        登录系统。

        ![](images/12811_zh-CN_source.png)

        与之前同样的方式，修改RemoteDesktop的作用域的远程IP地址，将之前测试设置的1.1.1.1换回自己的IP地址。

        ![](images/12812_zh-CN_source.png)

        换回自己的IP地址后可以正常远程了，如果不知道自己的公网IP，可以[点击此处](http://ip.taobao.com/)查看。

        ![](images/12813_zh-CN_source.png)

        以上就是使用高级安全Windows防火墙来实现对服务器远程访问的限制，其他的服务和端口都可以按照上面的方法来实现，例如，关闭不常用的135 137 138 445 端口，限制FTP和相关服务的访问等等，这样才能做到最大限度地保障服务器安全的运行。


## 命令行的方式 {#section_dcj_lns_gfb .section}

1.  导出防火墙配置到文件。

    ``` {#codeblock_tgz_2m2_umg}
    netsh advfirewall export c:\adv.pol
    ```

2.  导入防火墙配置文件到系统中。

    ``` {#codeblock_9tr_7r8_qti}
    netsh advfirewall import c:\adv.pol
    ```

3.  防火墙恢复默认设置。

    ``` {#codeblock_bxy_0j2_j1z}
    Netsh advfirewall reset
    ```

4.  关闭防火墙。

    ``` {#codeblock_qdz_18i_zil}
    netsh advfirewall set allprofiles state off
    ```

5.  开启防火墙。

    ``` {#codeblock_n5z_ddl_s3i}
    netsh advfirewall set allprofiles state on
    ```

6.  在所有配置文件中设置默认阻挡入站并允许出站通信。

    ``` {#codeblock_063_m7a_uyg}
    netsh advfirewall set allprofiles firewallpolicy blockinbound,allowoutbound
    ```

7.  删除名为 ftp 的规则。

    ``` {#codeblock_rsk_gej_aa1}
    netsh advfirewall firewall delete rule name=ftp
    ```

8.  删除本地端口 80 的所有入则。

    ``` {#codeblock_6r5_uae_soc}
    netsh advfirewall firewall delete rule name=all protocol=tcp localport=80
    ```

9.  添加远程桌面入站规则允许端口3389。

    ``` {#codeblock_gwr_1bv_6dg}
    netsh advfirewall firewall add rule name=远程桌面(TCP-In-3389) protocol=TCP dir=in localport=3389 action=allow
    ```


## 相关链接 {#section_lxd_dqs_gfb .section}

[Windows防火墙限制端口/IP/应用访问的方法以及例外的配置](https://www.alibabacloud.com/help/zh/faq-detail/40699.htm)

更多开源软件尽在[云市场](https://marketplace.alibabacloud.com/)

