# 搭建和使用SVN {#concept_pqr_4bb_ffb .concept}

Subversion（简称SVN）是一个开源的版本控制系统，管理随时间改变的数据。SVN服务支持svnserve和http访问模式，本教程分别介绍这两种访问模式的部署方法。

## SVN简介 {#section_esy_dcb_ffb .section}

SVN管理的数据存放在中央资料档案库（Repository）中。该档案库会记录文件的每一次变动，这样您就可以把数据恢复至旧版本或浏览文件的变动历史。SVN中常用的概念和操作如下：

-   Repository（源代码库）：源代码统一存放的地方。
-   Checkout（提取）：该操作用于从Repository中提取一份源代码到本地。
-   Commit（提交）：该操作用于将修改代码后的代码提交到Repository。
-   Update（更新）：该操作用于同步本地源代码与Repository中的源代码。

使用SVN管理代码的常见流程为：

1.  Checkout（您提取源代码到本地）。
2.  其他人修改并提交源代码到Repository。
3.  Update（您获得最新的代码）。
4.  您修改并调试成功源代码。
5.  Commit（提交修改后的代码到Repository，其他程序员即可看到您的修改）。

SVN管理源代码的单位为行。如果您与其他程序员同时修改了一个文件中的代码：

-   若修改的代码在不同行，SVN会自动合并两种修改。
-   若修改的代码在同一行，SVN会提示文件冲突（Conflict），需要手动确认。

## 项目配置 {#section_ru9_yxn_l9x .section}

本教程手动部署SVN的示例步骤中使用了以下版本软件。操作时，请您以实际软件版本为准。

-   操作系统：公共镜像CentOS 7.2 64位
-   SVN：1.7.14
-   Apache：2.4.6

## 部署模式 {#section_zpd_31d_vxl .section}

本教程为您提供以下两种访问模式的部署方法：

-   [svnserve访问模式](#section_4pd_hjh_m1v)
-   [http访问模式](#section_d2a_lz0_11r)

## 部署svnserve访问SVN模式 {#section_4pd_hjh_m1v .section}

 **基本流程** 

1.  安装SVN
2.  配置SVN
3.  配置安全组规则
4.  客户端测试访问

 **步骤一：安装SVN** 

您可以采用以下任一种方法安装SVN：

-   使用镜像市场的SVN镜像
    1.  单击[SVN版本控制镜像](https://market.aliyun.com/products/55530001/jxsc000061.html)进入购买页。
    2.  单击**立即购买**。
    3.  输入账号和密码，登录ECS控制台。
    4.  镜像配置项中已选择为SVN版本控制镜像。按页面提示，完成其他配置项并购买ECS实例。详情请参见[使用向导创建实例](../../../../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。
-   手动安装SVN
    1.  [远程连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
    2.  运行以下命令安装SVN。

        ```
        yum install subversion
        ```

    3.  运行以下命令查看SVN版本。

        ```
        svnserve --version
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712528_zh-CN.png)


 **步骤二：配置SVN** 

1.  运行以下命令创建版本库根目录。

    ```
    mkdir /var/svn
    ```

2.  依次运行以下命令创建版本库。

    ```
    # cd /var/svn
    # svnadmin create /var/svn/svnrepos
    ```

3.  依次运行以下命令查看自动生成的版本库文件。

    ```
    # cd svnrepos
    # ls
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712529_zh-CN.png)

    Subversion目录说明：

    |目录|说明|
    |--|--|
    |db|存放所有的版本控制数据文件。|
    |hooks|放置hook脚本文件。|
    |locks|用来追踪存取文件库的客户端。|
    |format|一个文本文件，文件中只包含一个整数，表示当前文件库配置的版本号。|
    |conf|SVN仓库的配置文件（仓库的访问账号、权限等）。|

4.  按以下步骤为SVN仓库设置账号和密码：
    1.  运行`cd conf/`命令。
    2.  运行`vi passwd`命令，打开用户配置文件。
    3.  按`i`键进入编辑模式。
    4.  移动光标至`[users]`块中，添加用户账号和密码。

        **说明：** 添加账号和密码的格式为：账号=密码。例如，suzhan（账号） = redhat（密码），如下图所示（注意等号两端要有一个空格）。

    5.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712530_zh-CN.png)

5.  按以下步骤为账号设置读写权限：
    1.  运行`vi authz`命令，打开权限控制文件。
    2.  按`i`键进入编辑模式。
    3.  移动光标至文件末尾，并添加如下代码（其中，suzhan表示账号，r表示读权限，w表示写权限）：

        ```
        [/]
        suzhan=rw
        ```

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712531_zh-CN.png)

6.  按以下步骤修改SVN服务配置。
    1.  运行`vi svnserve.conf`打开SVN服务配置文件。
    2.  按`i`键进入编辑模式。
    3.  移动光标找到如下配置行，删除行前面的注释符\#和空格：

        ```
        anon-access = read #匿名用户可读，您也可以设置 anon-access = none，不允许匿名用户访问。设置为 none，可以使日志日期正常显示
        auth-access = write #授权用户可写
        password-db = passwd #使用哪个文件作为账号文件
        authz-db = authz #使用哪个文件作为权限文件
        realm = /var/svn/svnrepos #认证空间名，版本库所在目录
        ```

        **说明：** 每行不能以空格开始，且等号两端要有一个空格。

    4.  按`Esc`键退出编辑模式，并输入`:wq`保存并退出。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712532_zh-CN.png)

7.  运行以下命令启动SVN版本库。

    ```
    svnserve -d -r /var/svn/
    ```

8.  运行命令`ps -ef |grep svn`查看SVN服务是否开启。

    如果返回结果如下图所示，表示SVN服务已经开启。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712533_zh-CN.png)

    **说明：** 运行`killall svnserve`命令可停止SVN服务。


 **步骤三：添加安全组规则** 

SVN服务的默认端口为TCP 3690。您需要登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)，[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)放行TCP 3690端口。

 **步骤四：使用Windows客户端测试** 

1.  在本机下载并安装[TortoiseSVN客户端](http://tortoisesvn.net/downloads.html)。
2.  右键单击本地项目文件夹。本示例中，项目文件夹为C:\\KDR。
3.  在弹出菜单中，选择**SVN检出**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712534_zh-CN.png)

4.  填写如下信息后，单击**确定**。

    -   指定资源库URL，格式为`svn://实例公网IP地址/SVN仓库名`。本示例中，SVN仓库名为svnrepos。
    -   指定**检出至目录**。本示例中，目录为C:\\KDR。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712535_zh-CN.png)

    如果出现下图所示信息，表示检出成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974712536_zh-CN.png)

    **说明：** 第一次登录需输入账号和密码，即您在passwd文件中设置的账户和密码。


## 部署http访问SVN模式 {#section_d2a_lz0_11r .section}

 **基本流程** 

1.  安装SVN
2.  安装Apache
3.  安装mod\_dav\_svn
4.  配置SVN
5.  配置Apache
6.  配置安全组规则
7.  浏览器测试访问

 **步骤一：安装SVN** 

1.  [远程连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
2.  运行以下命令安装SVN。

    ```
    yum install subversion
    ```

3.  运行以下命令查看SVN版本。

    ```
    svnserve --version
    ```


 **步骤二：安装Apache** 

1.  运行以下命令安装httpd。

    ``` {#codeblock_k21_i04_zdy}
    yum install httpd
    ```

2.  运行以下命令查看httpd版本。

    ``` {#codeblock_su5_0uk_7qk}
    httpd -version
    ```


 **步骤三：安装mod\_dav\_svn** 

1.  运行以下命令安装mod\_dav\_svn。

    ``` {#codeblock_2x5_nbh_ig4}
    yum install mod_dav_svn
    ```


 **步骤四：配置SVN** 

1.  运行以下命令创建版本库根目录。

    ```
    mkdir /var/svn
    ```

2.  运行以下命令创建SVN仓库。

    ``` {#codeblock_gbi_49r_m0l}
    svnadmin create /var/svn/svnrepo
    ```

3.  运行以下命令修改SVN仓库的用户组为apache。

    ``` {#codeblock_hmz_amc_f8l}
    chown -R apache:apache /var/svn/svnrepo
    ```

4.  运行以下命令创建用户配置文件passwd。

    ``` {#codeblock_cqf_2jc_6t5}
    touch /var/svn/passwd 
    ```

5.  运行以下命令创建用户admin并设置密码。本示例中，密码设置为admin123。

    ``` {#codeblock_42k_89t_cf4}
    htpasswd /var/svn/passwd admin
    ```

6.  运行以下命令创建用户访问权限文件。

    ``` {#codeblock_gyy_g49_5ef}
    cp /var/svn/svnrepo/conf/authz /var/svn/authz
    ```


 **步骤五：配置Apache** 

1.  运行`vim /etc/httpd/conf.d/subversion.conf`命令打开httpd配置文件。
2.  按`i`键进入编辑模式。
3.  输入以下配置信息：

    ``` {#codeblock_cyl_ags_o50}
    <Location /svn>
    DAV svn
    SVNParentPath /var/svn
    AuthType Basic
    AuthName "Authorization SVN"
    AuthzSVNAccessFile /var/svn/authz
    AuthUserFile /var/svn/passwd
    Require valid-user
    </Location>
    ```

4.  按`Esc`键后，输入`:wq`保存并关闭文件。
5.  运行以下命令启动Apache服务。

    ``` {#codeblock_u6c_woh_whx}
    systemctl start httpd.service
    ```


 **步骤六：添加安全组规则** 

SVN服务的默认端口为TCP 3690。您需要登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)，[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)放行TCP 3690端口。

 **步骤七：浏览器测试访问** 

1.  打开浏览器。
2.  输入网址`http://<ECS实例公网IP>/svn/<SVN仓库名>`。本示例中，SVN仓库名为svnrepo。
3.  按回车键。
4.  输入账号和密码，即您在passwd文件中设置的账号和密码。本示例中，账号为admin，密码为admin123。

    返回结果如下图所示，表示成功访问之前新建的SVN仓库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974844304_zh-CN.png)


## 下一步 {#section_bxy_32b_ffb .section}

SVN部署完成后，您可以下载项目到本地机器，还可以提交本地修改到服务端系统库、获取系统库更新、还原删除的文件。

 **提交修改** 

按以下步骤提交修改：

1.  在项目文件空白处单击右键，选择**SVN提交**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974812537_zh-CN.png)

2.  输入本次提交的版本更新信息（所作修改的注释）、勾选要提交的操作内容，单击**确定**，即可把本机项目提交到SVN服务器资源库，覆盖掉资源库项目从而实现更新。

    **说明：** 

    -   如果发生提交冲突，即两人都提交修改，后提交者由于版本落后会提交失败。这时，您可以先备份自己的项目，然后从服务端下载最新的项目，并将自己的项目覆盖到本地项目文件夹，再单击SVN提交即可成功提交。
    -   若您提交的项目中删除了某个文件，则会显示如下图所示信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974812538_zh-CN.png)


 **获取更新** 

SVN服务端系统库上的项目更新后，您可在本机项目文件空白处单击右键下载最新项目，选择**SVN更新**，即可自动完成下载，并会提示所做的更新有哪些。

**说明：** 在原项目文件夹内选择SVN更新，会自动覆盖原有内容。建议您先备份，再更新，防止自己本来的项目内容丢失。

 **SVN还原** 

1.  打开一个文件夹，右键检出数据。
2.  删掉数据。
3.  根据您是否已提交修改选择相应的操作：
    -   未提交时，右键单击空白处，选择**TortoiseSVN** \> **SVN 还原**。
    -   已提交时，服务端系统库中数据已得到同步，系统也会将其保存的数据删除。此时，您需要采取以下方法还原数据：
        1.  查看日志，确认删除了哪些文件。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974812539_zh-CN.png)

        2.  将删掉的文件保存版本至删除前的位置。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9780/155902974812540_zh-CN.png)

4.  打开原文件夹，选择**SVN提交**，即可同步文件和系统库中的数据。

## 相关链接 {#section_qrq_w2b_ffb .section}

更多开源软件尽在[云市场](https://market.aliyun.com/software)。

