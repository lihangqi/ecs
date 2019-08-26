# Linux实例搭建FTP站点 {#concept_ww3_123_ffb .concept}

vsftpd 是 Linux 下的一款小巧轻快、安全易用的 FTP 服务器软件。本教程以 CentOS 7.2 64位操作系统为例，说明如何在 Linux 实例上安装并配置 vsftpd。

Linux 实例搭建 FTP 站点具体操作步骤如下：

-   [步骤一： 安装 vsftpd](#)
-   [步骤二： 配置 vsftpd](#)
-   [步骤三： 设置安全组](#)
-   [步骤四： 客户端测试](#)

## 视频教程 {#section_ug4_jh5_hhb .section}

  

## 步骤一： 安装 vsftpd {#section_d55_c23_ffb .section}

1.  [远程连接](../../../../../cn.zh-CN/实例/实例生命周期/连接实例/使用用户名密码验证连接Linux实例.md#)并登录到 Linux 实例。
2.  运行命令`yum install -y vsftpd`安装 vsftpd。出现下图表示安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/155434705512598_zh-CN.png)

3.  运行以下命令进入`/etc/vsftpd`目录，并查看该目录下的文件。

    ```
    cd /etc/vsftpd
    ls
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/155434705512599_zh-CN.png)

    **说明：** 

    -   `/etc/vsftpd/vsftpd.conf` 是 vsftpd 的核心配置文件。
    -   `/etc/vsftpd/ftpusers` 是黑名单文件，此文件里的用户不允许访问 FTP 服务器。
    -   `/etc/vsftpd/user_list` 是白名单文件，此文件里的用户允许访问 FTP 服务器。
4.  运行以下命令设置FTP服务开机自启动。

    ```
    systemctl enable vsftpd.service
    ```

5.  运行以下命令启动 FTP 服务。

    ```
    systemctl start vsftpd.service
    ```

6.  运行以下命令查看 FTP 服务监听的端口。

    ```
    netstat -antup | grep ftp
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/155434705512600_zh-CN.png)


## 步骤二： 配置 vsftpd {#section_wpy_x23_ffb .section}

vsftpd 安装后默认开启了匿名访问 FTP 服务器的功能。使用匿名访问，您无需输入用户名密码即可登录 FTP 服务器，但没有权限修改或上传文件。

本教程介绍了以下两种配置 vsftpd 的方法，并提供了相关的参数说明，您可以根据具体需要进行参考。

-   配置匿名用户上传文件权限
-   配置本地用户登录

 **配置匿名用户上传文件权限** 

匿名访问FTP服务器是一种不安全的访问模式，任何人无需密码验证就可以登录到FTP服务器，这种模式一般只用来保存不重要的公开文件，不推荐在生产环境中使用。如果您需要配置匿名用户上传文件的权限，可以参考以下步骤配置：

1.  修改`/etc/vsftpd/vsftpd.conf`。
    1.  运行`vim /etc/vsftpd/vsftpd.conf`。
    2.  按**i** 键进入编辑模式。
    3.  将写权限修改为`write_enable=YES`。
    4.  将匿名上传权限修改为`anon_upload_enable=YES`。
    5.  按**Esc**键退出编辑模式，然后输入`:wq`保存并退出文件。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/155434705512602_zh-CN.png)

2.  运行以下命令更改`/var/ftp/pub`目录的权限，为 FTP 用户添加写权限，并重新加载配置文件。

    ```
    chmod o+w /var/ftp/pub/
    systemctl restart vsftpd.service
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/155434705512603_zh-CN.png)


 **配置本地用户登录** 

本地用户登录是指用户使用 Linux 操作系统的账号和密码登录 FTP 服务器。

vsftpd 安装后默认只支持匿名访问 FTP 服务器，如果您试图使用 Linux 操作系统中的账号登录服务器，将会被 vsftpd 服务拒绝。您可以参考以下步骤配置 vsftpd 服务，以使用Linux账号和密码访问FTP服务器。

1.  运行以下命令为FTP服务创建一个Linux用户。本示例中，该用户名为ftptest。

    ```
    useradd ftptest
    ```

2.  运行以下命令修改ftptest 用户的密码。

    ```
    passwd ftptest
    ```

3.  创建一个供FTP服务使用的文件目录。

    ```
    mkdir /var/ftp/test
    ```

4.  更改/var/ftp/test目录的拥有者为ftptest。

    ```
    chown -R ftptest:ftptest /var/ftp/test
    ```

5.  输入命令`vim /etc/vsftpd/vsftpd.conf`打开vsftpd.conf配置文件并按键**i**进入编辑模式。
6.  修改vsftpd.conf配置文件。

    FTP服务器可以配置为主动模式或被动模式。

    -   主动模式下，客户端向服务端发送数据端口的信息，由服务端主动连接客户端发送的数据端口。配置FTP为主动模式的参数如下：

        ```
        #禁止匿名登录FTP服务器
        anonymous_enable=NO
        #允许本地用户登录FTP服务器
        local_enable=YES
        #设置本地用户登录后所在的目录
        local_root=/var/ftp/test
        #全部用户被限制在主目录
        chroot_local_user=YES
        #启用例外用户名单
        chroot_list_enable=YES
        #指定例外用户列表，这些用户不被锁定在主目录
        chroot_list_file=/etc/vsftpd/chroot_list
        
        #配置其他参数
        allow_writeable_chroot=YES
        local_umask=022
        dirmessage_enable=YES
        xferlog_enable=YES
        connect_from_port_20=YES
        xferlog_std_format=YES
        listen=YES
        pam_service_name=vsftpd
        userlist_enable=YES
        tcp_wrappers=YES
        ```

    -   被动模式下，服务端开启并发送数据端口的信息给客户端，由客户端连接服务端开启的数据端口，服务端被动接受连接。在被动模式下，您需要配置服务端可以开启的数据端口范围。配置FTP为被动模式的参数如下：

        ```
        #禁止匿名登录FTP服务器
        anonymous_enable=NO
        #允许本地用户登录FTP服务器
        local_enable=YES
        #设置本地用户登录后所在目录
        local_root=/var/ftp/test
        #全部用户被限制在主目录
        chroot_local_user=YES
        #启用例外用户名单
        chroot_list_enable=YES
        #指定例外用户列表，这些用户不被锁定在主目录
        chroot_list_file=/etc/vsftpd/chroot_list
        #开启被动模式
        pasv_enable=YES
        #FTP服务器公网IP
        pasv_address=<FTP服务器公网IP>
        #设置被动模式下，建立数据传输可使用port范围的最小值
        pasv_min_port=port number
        #设置被动模式下，建立数据传输可使用port范围的最大值
        pasv_max_port=port number
        
        #配置其他参数
        local_umask=022
        dirmessage_enable=YES
        xferlog_enable=YES
        xferlog_std_format=YES
        tcp_wrappers=YES
        allow_writeable_chroot=YES
        listen=YES
        listen_ipv6=NO
        pam_service_name=vsftpd
        userlist_enable=YES
        ```

        **说明：** 建议您把端口范围设在比较高的一段范围内，比如50000-50010，有助于提高访问FTP服务器的安全性。

7.  按**Esc**键退出编辑模式，然后按键`:wq`保存并退出文件。
8.  运行`vim /etc/vsftpd/chroot_list`命令创建chroot\_list文件，并写入不受只可以访问其主目录限制的例外用户名单。

    **说明：** 如果没有例外用户也必须要有chroot\_list文件，内容可为空。

9.  按键**Esc**退出编辑模式，然后按键`:wq`保存并退出文件。
10. 运行以下命令重启vsftpd服务。

    ```
    systemctl restart vsftpd.service
    ```


 **vsftpd.conf 的配置文件参数说明** 

运行命令`cat /etc/vsftpd/vsftpd.conf`查看配置文件内容。

用户登录控制：

|参数|说明|
|:-|:-|
|anonymous\_enable=YES|接受匿名用户|
|no\_anon\_password=YES|匿名用户login时不询问口令|
|anon\_root=\(none\)|匿名用户主目录|
|local\_enable=YES|接受本地用户|
|local\_root=\(none\)|本地用户主目录|

用户权限控制：

|参数|说明|
|:-|:-|
|write\_enable=YES|可以上传\(全局控制\)|
|local\_umask=022|本地用户上传文件的umask|
|file\_open\_mode=0666|上传文件的权限配合umask使用|
|anon\_upload\_enable=NO|匿名用户可以上传|
|anon\_mkdir\_write\_enable=NO|匿名用户可以建目录|
|anon\_other\_write\_enable=NO|匿名用户修改删除|
|chown\_username=lightwiter|匿名上传文件所属用户名|

## 步骤三： 设置安全组 {#section_unb_wf3_ffb .section}

搭建好 FTP 站点后，您需要在实例安全组的入方向添加放行下列 FTP 端口的规则。

-   FTP 为主动模式时：端口21。
-   FTP 为被动模式时：端口21，以及配置文件/etc/vsftpd/vsftpd.conf中参数pasv\_min\_port和pasv\_max\_port之间的所有端口。

添加安全组规则的具体步骤，请参见[添加安全组规则](../../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 步骤四： 客户端测试 {#section_cn2_xf3_ffb .section}

您可以通过 FTP 客户端或浏览器访问 FTP 服务器进行测试。本教程以windows自带的IE（Internet Explorer）浏览器为例，分别为您介绍 FTP 服务器配置为主动模式或被动模式时的访问步骤。

**FTP服务器为主动模式** 

1.  打开客户端的 IE 浏览器。
2.  将浏览器设置为主动访问模式。选择 **设置** \> **Internet 选项** \> **高级** 。勾选 **启用 FTP 文件夹视图**，取消勾选 **使用被动 FTP**。
3.  在地址栏中输入`ftp://<FTP服务器IP地址>:FTP端口`，例如：`ftp://39.10.0.28:21`。
4.  在弹出的对话框中，输入用户名和密码，即可对 FTP 文件进行相应权限的操作。

**FTP服务器为被动模式** 

1.  打开客户端的 IE 浏览器。
2.  将浏览器设置为被动访问模式。选择 **设置** \> **Internet 选项** \> **高级** 。勾选 **启用 FTP 文件夹视图**，勾选 **使用被动 FTP**。
3.  在地址栏中输入`ftp://<FTP服务器IP地址>:FTP端口`，例如：`ftp://39.10.0.28:21`。
4.  在弹出的对话框中，输入用户名和密码，即可对 FTP 文件进行相应权限的操作。

**说明：** 使用浏览器访问 FTP 服务器出错时，建议您清除浏览器缓存后再尝试。

## 后续操作 {#section_lxz_dg3_ffb .section}

您可以参考 [安全加固方案](https://help.aliyun.com/knowledge_detail/37452.html) 对 FTP 服务进行安全加固。

