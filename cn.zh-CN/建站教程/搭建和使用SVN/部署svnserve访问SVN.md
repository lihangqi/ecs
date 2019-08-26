# 部署svnserve访问SVN {#task_1597495 .task}

本教程介绍如何通过svnserve访问模式来部署SVN。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

本教程手动部署SVN的示例步骤中使用了以下版本软件。操作时，请您以实际软件版本为准。

-   操作系统：公共镜像CentOS 7.2 64位
-   SVN：1.7.14
-   Apache：2.4.6

## 操作步骤 {#section_fxi_ocf_52q .section}

通过svnserve访问模式部署SVN的操作步骤如下：

1.  [步骤一：安装SVN](#section_h54_dqf_pyz)
2.  [步骤二：配置SVN](#section_qui_xbb_dke)
3.  [步骤三：配置安全组规则](#section_9qx_vu2_6zo)
4.  [步骤四：使用Windows客户端测试](#section_frq_nei_7ay)

## 步骤一：安装SVN {#section_h54_dqf_pyz .section}

您可以采用以下任一种方法安装SVN：

-   使用镜像市场的SVN镜像
    1.  单击[SVN版本控制镜像](https://market.aliyun.com/products/55530001/jxsc000061.html)进入购买页。
    2.  单击**立即购买**。
    3.  输入账号和密码，登录ECS控制台。
    4.  镜像配置项中已选择为SVN版本控制镜像。按页面提示，完成其他配置项并购买ECS实例。详情请参见[使用向导创建实例](../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。
-   手动安装SVN
    1.  [远程连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
    2.  运行以下命令安装SVN。

        ``` {#codeblock_90i_lm5_qzi}
        yum install subversion
        ```

    3.  运行以下命令查看SVN版本。

        ``` {#codeblock_6ml_3bk_pyo}
        svnserve --version
        ```

        ![查看SVN版本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384112528_zh-CN.png)


## 步骤二：配置SVN {#section_qui_xbb_dke .section}

完成以下操作，配置SVN：

1.  运行以下命令创建版本库根目录。 

    ``` {#codeblock_mvg_f02_stx}
    mkdir /var/svn
    ```

2.  依次运行以下命令创建版本库。 

    ``` {#codeblock_xbm_t6r_2y3}
    # cd /var/svn
    # svnadmin create /var/svn/svnrepos
    ```

3.  依次运行以下命令查看自动生成的版本库文件。 

    ``` {#codeblock_0z1_5zd_n4s}
    # cd svnrepos
    # ls
    ```

    ![查看版本库文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384112529_zh-CN.png)

    Subversion目录说明如下表：

    |目录|说明|
    |--|--|
    |db|存放所有的版本控制数据文件。|
    |hooks|放置hook脚本文件。|
    |locks|用来追踪存取文件库的客户端。|
    |format|一个文本文件，文件中只包含一个整数，表示当前文件库配置的版本号。|
    |conf|SVN仓库的配置文件（仓库的访问账号、权限等）。|

4.  设置SVN仓库的账号和密码。 
    1.  运行`cd conf/`命令。
    2.  运行`vi passwd`命令，打开用户配置文件。
    3.  按`i`键进入编辑模式。
    4.  移动光标至`[users]`块中，添加用户账号和密码。 

        **说明：** 添加账号和密码的格式为：账号=密码。例如，suzhan（账号） = redhat（密码），如下图所示（注意等号两端要有一个空格）。

        ![添加账号和密码](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384112530_zh-CN.png)

    5.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。
5.  设置账号的读写权限。 
    1.  运行`vi authz`命令，打开权限控制文件。
    2.  按`i`键进入编辑模式。
    3.  移动光标至文件末尾，并添加如下代码（其中，suzhan表示账号，r表示读权限，w表示写权限）： 

        ``` {#codeblock_5cv_jpj_877}
        [/]
        suzhan=rw
        ```

        ![设置账号读写权限](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384112531_zh-CN.png)

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。
6.  修改SVN服务配置。 
    1.  运行`vi svnserve.conf`打开SVN服务配置文件。
    2.  按`i`键进入编辑模式。
    3.  移动光标找到如下配置行，删除行前面的注释符\#和空格： 

        ``` {#codeblock_lif_rae_bf5}
        anon-access = read #匿名用户可读，您也可以设置 anon-access = none，不允许匿名用户访问。设置为 none，可以使日志日期正常显示
        auth-access = write #授权用户可写
        password-db = passwd #使用哪个文件作为账号文件
        authz-db = authz #使用哪个文件作为权限文件
        realm = /var/svn/svnrepos #认证空间名，版本库所在目录
        ```

        **说明：** 每行不能以空格开始，且等号两端要有一个空格。

        ![修改svn服务配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384112532_zh-CN.png)

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。
7.  运行以下命令启动SVN版本库。 

    ``` {#codeblock_2wb_bxm_m7c}
    svnserve -d -r /var/svn/
    ```

8.  运行命令`ps -ef |grep svn`查看SVN服务是否开启。 

    如果返回结果如下图所示，表示SVN服务已经开启。

    ![查看SVN服务状态](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384212533_zh-CN.png)

    **说明：** 运行`killall svnserve`命令可停止SVN服务。


## 步骤三：配置安全组规则 {#section_9qx_vu2_6zo .section}

SVN服务的默认端口为TCP 3690。您需要登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)，放行TCP 3690端口。具体操作，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 步骤四：使用Windows客户端测试 {#section_frq_nei_7ay .section}

完成以下操作，使用Windows客户端测试：

1.  在本机下载并安装[TortoiseSVN客户端](http://tortoisesvn.net/downloads.html)。
2.  右键单击本地项目文件夹。本示例中，项目文件夹为C:\\KDR。
3.  在弹出菜单中，选择**SVN检出**。
4.  填写如下信息后，单击**确定**。 

    -   指定**版本库URL**，格式为svn://实例公网IP地址/SVN仓库名。本示例中，SVN仓库名为svnrepos。
    -   指定**检出至目录**。本示例中，目录为C:\\KDR。
    ![检出设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384212535_zh-CN.png)

    如果出现下图所示信息，表示检出成功。

    ![检出成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/156646384212536_zh-CN.png)

    **说明：** 第一次登录需要输入账号和密码，即您在passwd文件中设置的账户和密码。


