# 部署RabbitMQ {#concept_th4_cr1_ffb .concept}

RabbitMQ是一个AMQP的开源实现，用于在分布式系统中存储转发消息，有良好的易用性、扩展性和高可用性。RabbitMQ使用Erlang语言编写服务器端，并支持多种客户端，如Python、Ruby、.NET、Java、JMS、C、PHP、ActionScript、XMPP 和 STOMP，同时也支持AJAX。

## 部署方式 {#section_oth_vs1_ffb .section}

您可以参考以下两种方式部署RabbitMQ：

-   [RabbitMQ镜像部署](cn.zh-CN/建站教程/部署RabbitMQ.md#section_hvf_bt1_ffb)：适合新手使用。
-   [RabbitMQ手动部署](cn.zh-CN/建站教程/部署RabbitMQ.md#section_gr4_zy1_ffb)：适合对Linux命令有基本了解的用户，能够个性化部署。

## 镜像部署 {#section_market_image .section}

1.  单击[RabbitMQ环境 \( CentOS7.3 Erlang19.3 \)](https://market.aliyun.com/products/55530001/cmjj017527.html)进入镜像详情页。
2.  单击**立即购买**，按提示步骤购买ECS实例。
3.  登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)。
4.  在左侧导航栏中，单击**实例**，进入ECS实例列表页。
5.  选择所购ECS实例所在的地域，并找到所购ECS实例，在**IP 地址**列获取该实例的公网 IP 地址。
6.  在浏览器地址栏中输入公网IP地址，下载操作文档。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9776/155503366312515_zh-CN.png)

7.  登录Linux实例，具体步骤请参见[使用用户名密码验证连接Linux实例](../../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
8.  初始化RabbitMQ。

    ```
    # cd /root/oneinstack 
    # ./init_rabbitmq.sh
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9776/155503366312516_zh-CN.png)

9.  进入管理页面，浏览器访问`http://公网IP:15672`。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9776/155503366312517_zh-CN.png)


## 手动部署 {#section_gr4_zy1_ffb .section}

本教程使用以下操作系统和软件版本：

-   操作系统：公共镜像CentOS 7.3 64位
-   RabbitMQ版本：rabbitmq-server -3.6.9
-   erlang版本：erlang19.3
-   JDK版本：JDK1.8.0\_121

 **前提条件** 

添加安全组规则，放行端口15672和5672入方向规则。

 **操作步骤** 

1.  安装依赖包。

    ```
    yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
    ```

2.  下载erlang安装包。

    ```
    wget http://erlang.org/download/otp_src_19.3.tar.gz
    ```

3.  解压缩erlang安装包。

    ```
    tar xzf otp_src_19.3.tar.gz
    ```

4.  创建一个文件夹。

    ```
    mkdir /usr/local/erlang
    ```

5.  编译并安装erlang。

    ```
    # cd otp_src_19.3
    # ./configure --prefix=/usr/local/erlang --without-javac
    # make && make install
    ```

6.  输入命令`vi /etc/profile`打开profile配置文件。按下`i`键，然后在文件末尾处添加如下内容：

    ```
    export PATH=$PATH:/usr/local/erlang/bin
    ```

    按下`Esc`键，然后输入`:wq`并回车以保存并关闭文件。

7.  输入命令`source /etc/profile`使环境变量生效。
8.  输入命令`erl -version`检查安装结果。
9.  下载RabbitMQ安装包。

    ```
    wget -P /root "https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.9/rabbitmq-server-3.6.9-1.el7.noarch.rpm"
    ```

10. 导入签名密钥。

    ```
    sudo rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
    ```

11. 安装RabbitMQ Server。

    ```
    # cd /root
    # sudo yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
    ```

12. 允许RabbitMQ开机自启动。

    ```
    sudo systemctl enable rabbitmq-server
    ```

13. 启动RabbitMQ。

    ```
    sudo systemctl start rabbitmq-server
    ```

14. 为保证数据安全，建议您删除默认用户。RabbitMQ默认的账号用户名和密码都是guest。

    ```
    sudo rabbitmqctl delete_user guest
    ```

15. 创建一个新用户。

    ```
    sudo rabbitmqctl add_user 用户名 密码
    ```

16. 将创建的新用户设置为管理员。

    ```
    sudo rabbitmqctl set_user_tags 用户名 administrator
    ```

17. 赋予新创建的用户所有权限。

    ```
    sudo rabbitmqctl set_permissions -p / 用户名 ".*" ".*" ".*"
    ```

18. 启用RabbitMQ的web管理界面。

    ```
    sudo rabbitmq-plugins enable rabbitmq_management
    ```

19. 使用浏览器访问`http://公网IP:15672`，显示如下页面，说明RabbitMQ安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9776/155503366339377_zh-CN.png)

20. 输入之前创建的用户名和密码后单击**Login**，进入RabbitMQ管理界面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9776/155503366339379_zh-CN.png)


