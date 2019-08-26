# 快速使用AMH建站 {#concept_qnl_rzs_2fb .concept}

AMH 是一套通过 Web 控制和管理服务器的 Linux 服务器管理系统以及虚拟主机管理系统。使用阿里云的云服务器 ECS 安装 AMH 可以快速地搭建出任意 PHP 网站。

阿里云云市场包含大量的镜像资源，您只需购买所需的镜像环境就可快速搭建出应用环境。

## 准备工作 {#section_olp_2bt_2fb .section}

提前创建好 ECS 实例，详情请参考 [创建实例](https://help.aliyun.com/document_detail/25424.html)。

## 镜像部署 {#section_ug5_fbt_2fb .section}

**说明：** 这里的镜像部署只针对还未购买 ECS 服务器的用户。

**操作步骤**

1.  登录 [阿里云云市场](https://market.aliyun.com/products/53398003/cmjj009429.html?spm=5176.730005.0.0.vdYTVv)，搜索关键字 **AMH4.2**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564012277_zh-CN.png)

2.  选择 **PHP运行环境**，单击 **立即购买**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564012278_zh-CN.png)

3.  配置 ECS 服务器，同时也会把 AMH 镜像环境安装进去，最后单击 **立即购买**，完成支付。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564012279_zh-CN.png)


## 手动部署 {#section_g4n_cct_2fb .section}

**AMH 4.2 编译安装**

AMH 4.2 为独立的一套 LNMP/Nginx 虚拟主机面板，安装请使用纯净系统。

1.  使用 root 账号登录 Linux 服务器。
2.  执行 amh 安装脚本。

    ```
    wget http://amh.sh/file/AMH/4.2/amh.sh && chmod 775 amh.sh && ./amh.sh 2>&1 | tee amh.log
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564012280_zh-CN.png)

3.  根据提示输入选择 1 ~ 3 选项。其中，1 代表安装 amh，2 代表卸载 amh，3 代表退出不做操作。输入 1 回车，接着输入 MySQL 和 AMH 的登录密码后进入安装流程。最后如看到安装成功提示，说明系统已安装完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112281_zh-CN.png)

    成功安装后，如有必要请删除日志文件 amh.log，若安装失败需协助安装请将错误日志反馈我们。进入AMH web端管理，默认账号为 admin。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112282_zh-CN.png)

    **说明：** 安装成功需花费 1 小时左右。


## AMH 使用流程 {#section_v3j_xct_2fb .section}

1.  进入 AMH 后台登录界面。

    **说明：** 输入 ECS 公网 ip:8888。

2.  使用镜像安装。默认帐号：admin 密码：cldera.com。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112283_zh-CN.png)

    登录成功后，您可以看到很多功能，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112284_zh-CN.png)

3.  在顶端导航栏中，单击 **虚拟主机**，开始创建空间。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112285_zh-CN.png)

4.  设置 **主标识域名** 和 **绑定域名** （其它默认），单击 **保存**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112286_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112287_zh-CN.png)

5.  在顶端导航栏中，选择 **MySQL** \> **快速建库**，继续创建 PHP 网站所需的 MySQL 数据库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112288_zh-CN.png)

    -   按下图所示完成数据库的创建，其中数据库编码一般选择 UTF8 即可。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112289_zh-CN.png)

    -   另一种创建是把 **localhost** 换成 **%**，这样可以远程管理 MYSQL。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112290_zh-CN.png)

        AMH 搭建网站准备工作完成后，可以通过 dedecms 系统安装默认网站。

6.  去官网下载 dedecms 系统上传到空间根目录。
7.  在导航栏中选择 **FTP**，新增 FTP 账号。（先使用AMH创建一个FTP 绑定到之前的空间）

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112291_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112292_zh-CN.png)

    **说明：** 该 FTP 需绑定到之前已创建的空间中。

8.  登录 FTP。登录后，FTP 中有 2 个默认主页文件，您可以直接删除。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112293_zh-CN.png)

    上传 dedecms 系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112294_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564112295_zh-CN.png)

9.  选择 FTP 创建的帐号，单击 **管理**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212296_zh-CN.png)

10. 登录 FTP，对已上传的文件进行解压。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212297_zh-CN.png)

    勾选需要解压的文件， 单击 **智能解压**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212298_zh-CN.png)

    解压完成后，开始安装网站。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212299_zh-CN.png)

11. 在浏览器中输入之前绑定的域名。该域名需要先解析到服务器。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212300_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212301_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212302_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9782/154817564212303_zh-CN.png)

    **说明：** 成操作后，您可以快速使用 AMH 建站。与其它 PHP 系统的安装使用都是相同的。


