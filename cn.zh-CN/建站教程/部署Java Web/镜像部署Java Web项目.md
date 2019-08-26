# 镜像部署Java Web项目 {#concept_52806_zh .concept}

Tomcat 作为一个开源且免费的 Java Web 服务器，常用来作为 Web 开发的工具。它可以托管由 Servlet、JSP 页面（动态内容）、HTML 页面、JS、样式表、图片（静态内容）组成的 Java Web 应用程序。

## 部署方式 {#section_clr_m2f_2fb .section}

在阿里云服务器下部署 Java 提供 3 种部署方式：

-   [JAVA 镜像部署](https://market.aliyun.com/products/53400005/cmjj016483.html)
-   [一键安装包部署](https://market.aliyun.com/products/56092004/cmgj000342.html)
-   [手动部署（源码编译安装/YUM安装）](http://help.aliyun.com/document_detail/51376.html)

一般推荐使用镜像部署，尤其适合新手，使用更加快捷方便（阿里云的云市场提供了丰富的镜像软件，[点击查看](https://market.aliyun.com/software)）。而安装包部署以及手动部署适合对 Linux 命令有基本了解的用户，可以满足用户个性化部署的要求。本文主要介绍镜像和手工部署的方式。

## 镜像部署 {#section_k52_2ff_2fb .section}

1.  单击 [JAVA 环境（CentOS7.3 Nginx Tomcat8 JDK）](https://market.aliyun.com/products/53400005/cmjj016483.html) 进入镜像详情页。
2.  单击 **立即购买**，按提示步骤购买 ECS 实例。
3.  登录 [ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。
4.  在左边导航栏中，单击 **实例**，进入 ECS 实例列表页。
5.  选择所购 ECS 实例所在的地域，找到已购的 ECS 实例，在 **IP 地址** 列获取该实例的公网 IP 地址。
6.  在浏览器地址栏中输入 `http://公网 IP 地址` 后，收藏在线文档。

    **说明：** 若输入公网后无法显示下述页面，请检查安全组公网入方向已开通80端口。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9765/153795999612101_zh-CN.png)

7.  使用 Putty 登录 Linux 服务器，参考 [连接Linux实例](http://help.aliyun.com/document_detail/51798.html)。

    **说明：** 若创建实例时未设置密码，root需 [重置实例密码](http://help.aliyun.com/document_detail/25439.html)。

8.  使用 Winscp 工具将 Java 代码放入 /data/wwwroot/default 中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9765/153795999612103_zh-CN.png)

9.  默认 Tomcat 是以一般 www 用户运行，将网站代码权限改为 www，执行命令：

    ```
    chown -R www.www /data/wwwroot
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9765/153795999612104_zh-CN.png)

10. 重启 Tomcat。

    ```
    service tomcat restart
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9765/153795999612105_zh-CN.png)

11. 在浏览器地址栏中输入公网 IP 地址，完成验证。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9765/153795999612106_zh-CN.png)


