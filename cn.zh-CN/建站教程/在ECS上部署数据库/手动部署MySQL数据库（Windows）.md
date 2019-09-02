# 手动部署MySQL数据库（Windows） {#task_1925617 .task}

本教程介绍如何在Windows系统ECS实例上手动部署MySQL数据库。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

1.  购买Windows Server 2012实例。具体操作，请参见[使用向导创建实例](../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。
2.  使用管理终端连接ECS实例。连接方式请参见[使用管理终端连接Windows实例](../cn.zh-CN/实例/连接实例/连接Windows实例/使用管理终端连接Windows实例.md#)。
3.  下载并安装插件vcredist\_x86.exe。 

    ![install_mysql_1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877612376_zh-CN.png)

4.  在[MySQL官网](https://www.mysql.com/)下载MySQL的安装包。
5.  安装MySQL。 

    1.  双击打开mysql-installer-community-5.6.15.0.msi安装MySQL。 

        ![install_mysql_2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877612377_zh-CN.png)

    2.  选择第一项**Install MySQL Products**。 

        ![install_mysql_3](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877612378_zh-CN.png)

    3.  勾选接受协议和跳过检测更新，进入下一步，单击**Custom**，也就是自定义安装。右边选择MySQL的安装位置和数据库位置，单击**Next**。 本示例步骤中，MySQL的安装位置和数据库位置均使用默认值，如下图所示。

        ![install_mysql_4](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877612379_zh-CN.png)

    4.  保持默认值不变，单击**Next**， 然后单击**Execute**，开始执行安装。 

        ![install_mysql5](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877712380_zh-CN.png)

    5.  单击**Next**至配置页面，选择**Server Machine**。 

        ![install_mysql6](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877712381_zh-CN.png)

    6.  保持默认值不变，单击**Next**，输入管理员root的密码，直至完成安装。
    安装完成后会在页面出现MySQL的管理命令控制台。

    ![install_mysql7](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/156715877712382_zh-CN.png)

6.  在已购ECS实例安全组入方向添加规则并放行3306端口。具体操作，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

