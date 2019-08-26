# Linux实例搭建FTP站点 {#concept_ww3_123_ffb .concept}

vsftpd 是 Linux 下的一款小巧轻快、安全易用的 FTP 服务器软件，是一款在各个 Linux 发行版中最受推崇的 FTP 服务器软件。本文以 CentOS 7.2 64位操作系统为例，说明如何在 Linux 实例上安装 vsftpd。

Linux 实例搭建 FTP 站点具体操作步骤如下：

-   [步骤一： 安装 vsftpd](#)
-   [步骤二： 配置 vsftpd](#)
-   [步骤三： 设置安全组](#)
-   [步骤四： 客户端测试](#)

## 步骤一： 安装 vsftpd {#section_d55_c23_ffb .section}

1.  [远程连接](../../../../intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接Linux实例.md#) 并登录到 Linux 实例。
2.  运行以下命令安装 vsftpd。

    ```
    yum install -y vsftpd
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390812597_zh-CN.png)

    出现下图表示安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390812598_zh-CN.png)

3.  运行以下命令打开及查看 `etc/vsftpd`。

    ```
    cd /etc/vsftpd
    ls
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912599_zh-CN.png)

    **说明：** 

    -   `/etc/vsftpd/vsftpd.conf` 是核心配置文件。
    -   `/etc/vsftpd/ftpusers` 是黑名单文件，此文件里的用户不允许访问 FTP 服务器。
    -   `/etc/vsftpd/user_list` 是白名单文件，是允许访问 FTP 服务器的用户列表。
4.  运行以下命令设置开机自启动。

    ```
    systemctl enable vsftpd.service
    ```

5.  运行以下命令启动 FTP 服务。

    ```
    systemctl start vsftpd.service
    ```

6.  运行以下命令查看 FTP 服务端口。

    ```
    netstat -antup | grep ftp
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912600_zh-CN.png)


## 步骤二： 配置 vsftpd {#section_wpy_x23_ffb .section}

vsftpd 安装后默认开启了匿名 FTP 的功能，使用匿名 FTP，用户无需输入用户名密码即可登录 FTP 服务器，但没有权限修改或上传文件。

文本介绍了以下几个配置 vsftpd 的方法以及相关的参数说明，您可以根据具体需要进行参考。

-   配置匿名用户上传文件权限
-   配置本地用户登录
-   vsftpd.conf 的配置文件参数说明

**配置匿名用户上传文件权限**

修改 `vsftpd.conf` 的配置文件的选项，可以赋予匿名 FTP 更多的权限。

1.  修改 `/etc/vsftpd/vsftpd.conf`：
    1.  运行 `vim /etc/vsftpd/vsftpd.conf`。
    2.  按 **i** 键进入编辑模式。
    3.  将写权限修改为 `write_enable=YES`。
    4.  将匿名上传权限修改为 `anon_upload_enable=YES`。
    5.  按 **Esc** 键退出编辑模式，然后输入 `:wq` 保存并退出文件。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912602_zh-CN.png)

2.  运行以下命令更改 `/var/ftp/pub` 目录的权限，为 FTP 用户添加写权限，并重新加载配置文件。

    ```
    chmod o+w /var/ftp/pub/
    systemctl restart vsftpd.service
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912603_zh-CN.png)


**配置本地用户登录**

本地用户登录就是指用户使用 Linux 操作系统中的用户账号和密码登录 FTP 服务器。

vsftpd 安装后默只支持匿名 FTP 登录，用户如果试图使用 Linux 操作系统中的账号登录服务器，将会被 vsftpd 拒绝，但可以在 vsftpd 里配置用户账号和密码登录。具体步骤如下：

1.  运行以下命令创建 ftptest 用户。

    ```
    useradd ftptest
    ```

2.  运行以下命令修改 ftptest 用户密码。

    ```
    passwd ftptest
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912604_zh-CN.png)

3.  修改 `/etc/vsftpd/vsftpd.conf`：
    1.  运行 `vim /etc/vsftpd/vsftpd.conf`。
    2.  按键 **i** 进入编辑模式。
    3.  将是否允许匿名登录 FTP 的参数修改为 `anonymous enable=NO`。
    4.  将是否允许本地用户登录 FTP 的参数修改为 `local_enable=YES`。
    5.  按键 **Esc** 退出编辑模式，然后按键 `：wq` 保存并退出文件。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912605_zh-CN.png)

4.  运行以下命令重新加载配置文件。

    ```
    systemctl restart vsftpd.service
    ```


**vsftpd.conf 的配置文件参数说明**

运行命令 `cat /etc/vsftpd/vsftpd.conf` 查看配置文件内容。

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

搭建好 FTP 站点后，您需要在实例的安全组的入方向添加一条放行 FTP 端口的规则，具体步骤参见 [添加安全组规则](../../../../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。

## 步骤四： 客户端测试 {#section_cn2_xf3_ffb .section}

打开客户端的 **计算机**，在路径栏输入 `ftp://服务器 IP 地址:FTP 端口`（如果不填端口则默认访问21端口），例如：`ftp://0.0.0.0:20`。弹出输入用户名和密码的对话框表示配置成功，正确的输入用户名和密码后，即可对 FTP 文件进行相应权限的操作。

**说明：** 客户端使用此方法访问 FTP 站点时，需要对 IE 浏览器进行设置，才能打开 FTP 的文件夹。 打开 IE 浏览器，选择 **设置** \> **Internet 选项** \> **高级**。勾选 **启用 FTP 文件夹视图**，取消勾选 **使用被动 FTP**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21756/154390390912606_zh-CN.png)

## 后续操作 {#section_lxz_dg3_ffb .section}

您可以参考 [安全加固方案](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm) 对 FTP 服务进行安全加固。

