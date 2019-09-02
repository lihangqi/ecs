# Linux实例搭建FTP站点 {#concept_ww3_123_ffb .task}

vsftpd是Linux下的一款小巧轻快、安全易用的FTP服务器软件。本教程以CentOS 7.2 64位操作系统为例，介绍如何在Linux实例上安装并配置vsftpd。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

Linux 实例搭建FTP站点具体步骤如下：

-   [步骤一： 安装vsftpd](#section_821_887_8np)
-   [步骤二： 配置vsftpd](#section_7bm_08s_pts)
-   [步骤三： 设置安全组](#section_cnf_mp9_o24)
-   [步骤四： 客户端测试](#section_zhf_ksd_coj)

## 视频教程 {#section_qbk_p6n_ch9 .section}

  

## 步骤一： 安装vsftpd {#section_821_887_8np .section}

完成以下操作，安装vsftpd。

1.  远程连接Linux实例。具体操作，请参见[使用用户名密码验证连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
2.  运行以下命令安装vsftpd。 

    ``` {#codeblock_kec_asf_iun}
    yum install -y vsftpd
    ```

    出现如下图所示界面，表示安装成功。

    ![install_vsftp_successfully](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/156715825212598_zh-CN.png)

3.  依次运行以下命令进入/etc/vsftpd目录，并查看该目录下的文件。 

    ``` {#codeblock_ypp_uss_tvo}
    cd /etc/vsftpd
    ```

    ``` {#codeblock_klw_e5z_sqc}
    ls
    ```

    ![install_vsftp_2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/156715825212599_zh-CN.png)

    **说明：** 

    -   /etc/vsftpd/vsftpd.conf是vsftpd的核心配置文件。
    -   /etc/vsftpd/ftpusers是黑名单文件，此文件中的用户不允许访问FTP服务器。
    -   /etc/vsftpd/user\_list是白名单文件，此文件中的用户允许访问FTP服务器。
4.  运行以下命令设置FTP服务开机自启动。 

    ``` {#codeblock_ez8_gnt_z24}
    systemctl enable vsftpd.service
    ```

5.  运行以下命令启动FTP服务。 

    ``` {#codeblock_izf_kx4_se6}
    systemctl start vsftpd.service
    ```

6.  运行以下命令查看FTP服务监听的端口。 

    ``` {#codeblock_64m_c7k_7dt}
    netstat -antup | grep ftp
    ```

    ![install_vsftpd_3](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/156715825212600_zh-CN.png)


vsftpd安装后默认开启了匿名访问FTP服务器的功能。使用匿名访问，您无需输入用户名密码即可登录FTP服务器，但没有权限修改或上传文件。

## 步骤二： 配置vsftpd {#section_7bm_08s_pts .section}

本节介绍以下两种配置vsftpd的方法，并提供了相关的参数说明，您可以根据具体需要进行参考。

-   方法一：配置匿名用户上传文件权限
-   方法二：配置本地用户登录

方法一：配置匿名用户上传文件权限

匿名访问FTP服务器是一种不安全的访问模式，任何人无需密码验证就可以登录到FTP服务器，这种模式一般只用来保存不重要的公开文件，不推荐在生产环境中使用。配置匿名用户上传文件的权限的操作步骤如下：

1.  修改配置文件/etc/vsftpd/vsftpd.conf。 

    1.  运行`vim /etc/vsftpd/vsftpd.conf`命令打开配置文件。
    2.  按i进入编辑模式。
    3.  将写权限修改为`write_enable=YES`。
    4.  将匿名上传权限修改为`anon_upload_enable=YES`。
    5.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。
    修改后的配置文件，如下图所示。

    ![匿名权限1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/156715825212602_zh-CN.png)

2.  依次运行以下命令更改/var/ftp/pub目录的权限，为FTP用户添加写权限，并重新加载配置文件。 

    ``` {#codeblock_43i_aou_qsr}
    chmod o+w /var/ftp/pub/
    ```

    ``` {#codeblock_a25_88h_93t}
    systemctl restart vsftpd.service
    ```

    ![匿名权限2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/156715825212603_zh-CN.png)


方法二：配置本地用户登录

本地用户登录是指用户使用Linux操作系统的账号和密码登录FTP服务器。vsftpd安装后默认只支持匿名访问FTP服务器，如果您试图使用本地用户登录服务器，将会被vsftpd服务拒绝。配置本地用户访问FTP服务器的操作步骤如下：

1.  运行以下命令为FTP服务创建一个Linux用户。本示例中，该用户名为ftptest。 

    ``` {#codeblock_hds_fxt_yaf}
    useradd ftptest
    ```

2.  运行以下命令修改ftptest用户的密码。 

    ``` {#codeblock_x83_54n_6mh}
    passwd ftptest
    ```

3.  运行以下命令创建一个供FTP服务使用的文件目录。 

    ``` {#codeblock_run_5jn_ib5}
    mkdir /var/ftp/test
    ```

4.  运行以下命令更改/var/ftp/test目录的拥有者为ftptest。 

    ``` {#codeblock_z6g_3sd_usi}
    chown -R ftptest:ftptest /var/ftp/test
    ```

5.  修改vsftpd.conf配置文件。 
    1.  运行`vim /etc/vsftpd/vsftpd.conf`命令打开配置文件。
    2.  按i进入编辑模式。
    3.  根据实际需要，配置FTP服务器为主动模式或被动模式。 
        -   主动模式下，客户端向服务端发送数据端口的信息，由服务端主动连接客户端发送的数据端口。配置FTP为主动模式的参数如下：

            ``` {#codeblock_fpw_5jt_a9n}
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

            ``` {#codeblock_bg4_ham_kn8}
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

            **说明：** 建议您把端口范围设在比较高的一段范围内，例如50000-50010，有助于提高访问FTP服务器的安全性。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。
6.  创建chroot\_list文件，并在文件中写入例外用户名单。 

    1.  运行`vim /etc/vsftpd/chroot_list`命令创建chroot\_list文件。
    2.  按i进入编辑模式。
    3.  输入例外用户名单。此名单中的用户不会被锁定在主目录，可以访问其他目录。
    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。
    **说明：** 如果没有例外用户也必须要有chroot\_list文件，内容可为空。

7.  运行以下命令重启vsftpd服务。 

    ``` {#codeblock_mgw_tpm_4b5}
    systemctl restart vsftpd.service
    ```


配置文件vsftpd.conf参数说明

运行命令`cat /etc/vsftpd/vsftpd.conf`可以查看配置文件内容。

-   用户登录控制参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |anonymous\_enable=YES|接受匿名用户|
    |no\_anon\_password=YES|匿名用户login时不询问口令|
    |anon\_root=（none）|匿名用户主目录|
    |local\_enable=YES|接受本地用户|
    |local\_root=（none）|本地用户主目录|

-   用户权限控制参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |write\_enable=YES|可以上传（全局控制）|
    |local\_umask=022|本地用户上传文件的umask|
    |file\_open\_mode=0666|上传文件的权限配合umask使用|
    |anon\_upload\_enable=NO|匿名用户可以上传|
    |anon\_mkdir\_write\_enable=NO|匿名用户可以建目录|
    |anon\_other\_write\_enable=NO|匿名用户修改删除|
    |chown\_username=lightwiter|匿名上传文件所属用户名|


## 步骤三： 设置安全组 {#section_cnf_mp9_o24 .section}

搭建好FTP站点后，您需要在实例安全组的入方向添加放行下列FTP端口的规则。

-   FTP为主动模式时：端口21。
-   FTP为被动模式时：端口21，以及配置文件/etc/vsftpd/vsftpd.conf中参数pasv\_min\_port和pasv\_max\_port之间的所有端口。

添加安全组规则的具体步骤，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 步骤四： 客户端测试 {#section_zhf_ksd_coj .section}

您可以通过FTP客户端或浏览器访问FTP服务器进行测试。本教程以windows自带的IE（Internet Explorer）浏览器为例，分别为您介绍FTP服务器配置为主动模式或被动模式时的访问步骤。

-   FTP服务器为主动模式
    1.  打开客户端的IE浏览器。
    2.  将浏览器设置为主动访问模式。选择**设置** \> **Internet 选项** \> **高级**。选中**启用 FTP 文件夹视图**，取消勾选**使用被动 FTP**。
    3.  在地址栏中输入`ftp://<FTP服务器IP地址>:FTP端口`，例如：`ftp://39.10.0.28:21`。
    4.  在弹出的对话框中，输入用户名和密码，即可对FTP文件进行相应权限的操作。
-   FTP服务器为被动模式
    1.  打开客户端的IE浏览器。
    2.  将浏览器设置为被动访问模式。选择**设置** \> **Internet 选项** \> **高级**。选中**启用FTP文件夹视图**和**使用被动FTP**。
    3.  在地址栏中输入`ftp://<FTP服务器IP地址>:FTP端口`，例如：`ftp://39.10.0.28:21`。
    4.  在弹出的对话框中，输入用户名和密码，即可对FTP文件进行相应权限的操作。

**说明：** 使用浏览器访问FTP服务器出错时，建议您清除浏览器缓存后再尝试。

对FTP服务进行安全加固。具体操作，请参见[安全加固方案](https://help.aliyun.com/knowledge_detail/37452.html) 。

