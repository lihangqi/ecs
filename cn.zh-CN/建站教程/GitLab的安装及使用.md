# GitLab的安装及使用 {#concept_myh_s5s_2fb .concept}

本篇文档介绍了在阿里云上如何使用弹性云服务器的Linux实例手工部署GitLab。GitLab 是 Ruby 开发的自托管的 Git 项目仓库，可通过Web界面进行访问公开的或者私人项目。

## 前提条件 {#section_hlm_zhc_5gb .section}

-   部署GitLab的实例要求至少使用2个vCPU和4GB的内存。
-   参考[添加安全组规则](../../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)，添加如下表所示的安全组规则。

    |方向|协议/应用|端口/范围|源地址|
    |--|-----|-----|---|
    |入方向|HTTP\(80\)|80|0.0.0.0/0|


## Gitlab环境部署 {#section_lbj_kws_2fb .section}

**方法一：镜像部署**

镜像名称：[GitLab代码管理（Centos 64位 | GitLab）](https://market.aliyun.com/products/55530001/jxsc000067.html?spm=5176.730005.0.0.LuTu) | [镜像帮助文档](http://zy-res.oss-cn-hangzhou.aliyuncs.com/aliyun_Market_files/gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf?spm=5176.730006-jxsc000067.102.9.J5BUL1&file=gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf)

进入镜像详情页面，单击 **立即购买**，按提示步骤购买 ECS 实例。

购买完成之后，登录ECS 管理控制台，在左边导航栏里，单击 **实例**，进入 ECS 实例列表页,选择所购 ECS 实例所在的地域，并找到所购 ECS 实例，在 **IP 地址** 列获取该实例的公网 IP 地址。

**说明：** 镜像部署好后默认是禁止远端访问的，所以直接访问ECS服务器的公网IP是不能访问到GitLab的登录界面的，请先运行/alidata目录下的gitlab\_opennet.sh脚本，开启远程访问，然后再通过浏览器访问公网IP来访问GitLab的主页。

**方法二：手动部署**

1.  安装依赖包。

    ```
    sudo yum install -y curl policycoreutils-python openssh-server
    ```

2.  设置SSH开机自启动并启动SSH服务。

    ```
    sudo systemctl enable sshd
    sudo systemctl start sshd
    ```

3.  安装Postfix来发送通知邮件。

    ```
    sudo yum install postfix
    ```

4.  设置Postfix开机自启动。

    ```
    sudo systemctl enable postfix
    ```

5.  启动Postfix服务。
    1.  输入命令`vim /etc/postfix/main.cf`打开main.cf文件并找到下图内容：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473138837_zh-CN.png)

    2.  将这行代码改为`inet_interfaces = all`，然后按`Esc`键，然后输入`:wq`并回车以保存并关闭main.cf文件。
    3.  输入命令`sudo systemctl start postfix`启动Postfix服务。
6.  添加GitLab软件包仓库。

    ```
     curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
    ```

7.  安装GitLab。

    ```
    sudo EXTERNAL_URL="GitLab服务器的公网IP地址" yum install -y gitlab-ce
    ```

    **说明：** 您可从ECS 管理控制台的实例列表页找到GitLab服务器的公网IP地址。

8.  使用浏览器访问GitLab服务器的公网IP地址，显示如下页面，说明环境搭建成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473112259_zh-CN.png)


## GitLab使用 {#section_hmj_gxs_2fb .section}

**登录GitLab**

1.  在浏览器的地址栏中输入ECS服务器的公网IP即可登录GitLab的界面，第一次登录使用的用户名和密码为 root 和 5iveL!fe。
2.  首次登录会强制用户修改密码。密码修改成功后，输入新密码进行登录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473112260_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473112261_zh-CN.png)


**创建Project**

1.  安装Git工具linux：安装Git，使用自带的源安装。

    ```
    yum install git
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473112262_zh-CN.png)

2.  生成密钥文件。

    使用ssh-keygen生成密钥文件.ssh/id\_rsa.pub，再将公钥文件id-rsa.pub中的内容粘帖到GitLab服务器的SSH-key的配置中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212263_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212264_zh-CN.png)

3.  在GitLab的主页中新建一个Project。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212265_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212274_zh-CN.png)

4.  添加ssh key导入步骤2中生成的密钥文件内容：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212266_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212275_zh-CN.png)

    ssh key添加完成：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212267_zh-CN.png)

    项目地址，该地址在进行clone操作时需要用到：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212268_zh-CN.png)


**简单配置**

1.  配置使用Git仓库的人员姓名。

    ```
    git config --global user.name "上海驻云" 
    ```

2.  配置使用Git仓库的人员email，填写自己的公司邮箱。

    ```
    git config --global user.email "support@jiagouyun.com" 
    ```

3.  克隆项目，在本地生成同名目录，并且目录中会有所有的项目文件。

    ```
    git clone git@iZbp1h7fx16gkr9u4gk8v3Z:root/test.git
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212269_zh-CN.png)


**上传文件**

1.  进入到项目目录。

    ```
    cd test/ 
    ```

2.  创建需要上传到GitLab中的目标文件。

    ```
    echo “test” > /root/test.sh
    ```

3.  将目标文件或者目录拷贝到项目目录下。

    ```
    cp /root/test.sh ./ 
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212270_zh-CN.png)

4.  将test.sh文件加入到索引中。

    ```
    git add test.sh
    ```

5.  将test.sh提交到本地仓库。

    ```
    git commit -m “test.sh”
    ```

6.  将文件同步到GitLab服务器上。

    ```
    git push -u origin master
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212271_zh-CN.png)

7.  在网页中查看上传的test.sh文件已经同步到GitLab中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/155125473212272_zh-CN.png)


## 相关链接 {#section_rqd_4zs_2fb .section}

更多开源软件尽在云市场：[https://market.aliyun.com/software](https://market.aliyun.com/software)

