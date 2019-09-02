# GitLab的安装及使用 {#concept_myh_s5s_2fb .concept}

GitLab是Ruby开发的自托管的Git项目仓库，可通过Web界面访问公开的或者私人的项目。本篇教程介绍如何在阿里云上使用云服务器ECS的Linux实例手动部署GitLab。

## 前提条件 {#section_hlm_zhc_5gb .section}

-   部署GitLab的实例要求至少使用2个vCPU和4GiB的内存。
-   添加如下表所示的安全组规则。具体步骤，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

    |方向|协议/应用|端口/范围|源地址|
    |--|-----|-----|---|
    |入方向|HTTP\(80\)|80|0.0.0.0/0|


## Gitlab环境部署 {#section_lbj_kws_2fb .section}

 **方法一：镜像部署** 

镜像名称：[GitLab代码管理（Centos 64位 | GitLab）](https://market.aliyun.com/products/55530001/jxsc000067.html?spm=5176.730005.0.0.LuTu) | [镜像帮助文档](http://zy-res.oss-cn-hangzhou.aliyuncs.com/aliyun_Market_files/gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf?spm=5176.730006-jxsc000067.102.9.J5BUL1&file=gitlab%E4%BB%A3%E7%A0%81%E7%AE%A1%E7%90%86%EF%BC%88centos%2064%E4%BD%8D%20%20gitlab%EF%BC%89.pdf)

1.  进入镜像详情页面，单击**立即购买**，按提示步骤购买ECS实例。
2.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
3.  在左侧导航栏，选择**实例与镜像** \> **实例**。
4.  在顶部状态栏处，选择地域。
5.  在实例列表页面，找到所购ECS实例，并在**IP 地址**列获取该实例的公网IP地址。

**说明：** 镜像部署成功后默认禁止远程访问，所以直接访问ECS服务器的公网IP无法访问GitLab的登录界面，请先运行/alidata目录下的gitlab\_opennet.sh脚本，开启远程访问，然后再通过浏览器访问公网IP来访问GitLab的主页。

 **方法二：手动部署** 

1.  安装依赖包。

    ``` {#codeblock_ksb_9cy_wn9}
    sudo yum install -y curl policycoreutils-python openssh-server
    ```

2.  设置SSH开机自启动并启动SSH服务。

    ``` {#codeblock_9b3_9gj_9i1}
    sudo systemctl enable sshd
    sudo systemctl start sshd
    ```

3.  安装Postfix来发送通知邮件。

    ``` {#codeblock_j05_xsc_6s9}
    sudo yum install postfix
    ```

4.  设置Postfix开机自启动。

    ``` {#codeblock_6n2_pz4_p93}
    sudo systemctl enable postfix
    ```

5.  启动Postfix服务。
    1.  运行命令`vim /etc/postfix/main.cf`打开main.cf文件，找到下图内容：

        ![set_inet](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849038837_zh-CN.png)

    2.  按`i`键进入编辑模式。
    3.  将这行代码改为`inet_interfaces = all`。
    4.  按`Esc`键，然后输入`:wq`并回车以保存并关闭main.cf文件。
    5.  运行命令`sudo systemctl start postfix`启动Postfix服务。
6.  添加GitLab软件包仓库。

    ``` {#codeblock_bpl_1bw_xzw}
     curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
    ```

7.  安装GitLab。

    ``` {#codeblock_igu_89e_kac}
    sudo EXTERNAL_URL="GitLab服务器的公网IP地址" yum install -y gitlab-ce
    ```

    **说明：** 您可从ECS管理控制台的实例列表页找到GitLab服务器的公网IP地址。

8.  使用浏览器访问GitLab服务器的公网IP地址，返回页面如下图所示，说明环境搭建成功。

    ![sign_in](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012259_zh-CN.png)


## GitLab使用 {#section_hmj_gxs_2fb .section}

 **登录GitLab** 

1.  在浏览器的地址栏中，输入ECS服务器的公网IP即可进入GitLab的登录界面，首次登录使用用户名`root`。
2.  首次登录会强制用户修改密码。密码修改成功后，输入新密码进行登录。

    ![修改登录密码](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012260_zh-CN.png)

    ![GitLab欢迎页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012261_zh-CN.png)


 **创建Project** 

1.  使用Linux自带的软件源安装Git工具。

    ``` {#codeblock_28i_7gi_pw2}
    yum install git
    ```

    ![install_git](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012262_zh-CN.png)

2.  生成密钥文件。

    使用ssh-keygen生成密钥文件.ssh/id\_rsa，再将公钥文件id-rsa.pub中的内容粘帖到GitLab服务器的SSH-key的配置文件中。

    ![密钥](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012263_zh-CN.png)

    ![公钥](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012264_zh-CN.png)

3.  在GitLab的主页中新建一个Project。

    ![new_project](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849012265_zh-CN.png)

    ![new_project_2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112274_zh-CN.png)

4.  添加ssh key，导入步骤2中生成的密钥文件内容。

    ![import-sshkey-1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112266_zh-CN.png)

    ![import-sshkey-2](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112275_zh-CN.png)

    ssh key添加完成后，如下图所示。

    ![import-ssh-key-complete](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112267_zh-CN.png)

    保存项目地址，该地址在进行克隆操作时需要用到。

    ![项目地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112268_zh-CN.png)


 **简单配置** 

1.  配置使用Git仓库的人员姓名。

    ``` {#codeblock_thh_ejv_13x}
    git config --global user.name "姓名" 
    ```

2.  配置使用Git仓库的人员email，填写自己的公司邮箱。

    ``` {#codeblock_3ub_jkc_2xf}
    git config --global user.email "abc@example.com" 
    ```

3.  克隆项目，在本地生成同名目录，并且目录中会有所有的项目文件。

    ``` {#codeblock_adf_bqj_fur}
    git clone git@iZxxxxxxxxxxxxxxxxx3Z:root/test.git
    ```

    ![简单配置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112269_zh-CN.png)


 **上传文件** 

1.  进入到项目目录。

    ``` {#codeblock_fij_8ug_3ew}
    cd test/ 
    ```

2.  创建需要上传到GitLab中的目标文件。

    ``` {#codeblock_wsr_xej_10p}
    echo “test” > /root/test.sh
    ```

3.  将目标文件或者目录复制到项目目录下。

    ``` {#codeblock_ej5_7es_crz}
    cp /root/test.sh ./ 
    ```

    ![上传文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849112270_zh-CN.png)

4.  将test.sh文件加入到索引中。

    ``` {#codeblock_qdm_1lq_sx4}
    git add test.sh
    ```

5.  将test.sh提交到本地仓库。

    ``` {#codeblock_7e0_fuz_kj0}
    git commit -m “test.sh”
    ```

6.  将文件同步到GitLab服务器上。

    ``` {#codeblock_8zq_9an_zc2}
    git push -u origin master
    ```

    ![文件同步命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849212271_zh-CN.png)

7.  在网页中查看上传的test.sh文件已经同步到GitLab中。

    ![文件同步结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9777/156715849212272_zh-CN.png)


