# 部署Node.js项目（CentOS） {#concept_50775_zh .task}

本教程介绍如何在安装了CentOS 7.2系统的ECS实例上，安装Node.js并部署项目。

-   用于连接ECS实例的机器上已安装PuTTY。下载地址：[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/)。
-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

Node.js是一个基于Chrome V8引擎的JavaScript运行环境，用来方便快速地搭建易于扩展的网络应用。Node.js使用了一个事件驱动、非阻塞式I/O的模型，使其轻量又高效，非常适合运行在分布式设备的数据密集型的实时应用。Node.js的包管理器npm，是全球最大的开源库生态系统。Node.js的典型应用场景包括：

-   实时应用：如在线聊天，实时通知推送等等（例如socket.io）。
-   分布式应用：通过高效的并行I/O使用已有的数据。
-   工具类应用：海量的工具，小到前端压缩部署（例如grunt），大到桌面图形界面应用程序。
-   游戏类应用：游戏领域对实时和并发有很高的要求（例如网易的pomelo框架）。
-   利用稳定接口提升Web渲染能力
-   前后端编程语言环境统一：前端开发人员可以非常快速地切入到服务器端的开发（例如著名的纯Javascript全栈式MEAN架构）。

## 操作步骤 {#section_z74_yzt_kll .section}

在ECS实例上安装Node.js并部署项目的操作步骤如下：

1.  [步骤一：创建并连接ECS实例](#section_e0r_tml_c8k)
2.  [步骤二：部署Node.js环境](#section_tug_p3l_h9l)
3.  [步骤三：部署测试项目](#section_igz_e58_4zq)

## 步骤一：创建并连接ECS实例 {#section_e0r_tml_c8k .section}

完成以下操作，创建并连接ECS实例：

1.  使用公共镜像CentOS 7.2 64位，创建ECS实例。具体操作，请参见[创建ECS实例](../cn.zh-CN/个人版快速入门/创建ECS实例.md#)。
2.  使用root用户连接ECS实例。具体操作，请参见[使用用户名密码验证连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。

## 步骤二：部署Node.js环境 {#section_tug_p3l_h9l .section}

选择以下任意一种方法部署Node.js环境。

-   使用二进制文件安装

    该部署过程使用的安装包是已编译好的二进制文件。解压之后，在bin文件夹中就已存在node和npm，无需重复编译。

    完成以下操作，使用二进制文件部署Node.js环境：

    1.  下载Node.js安装包。

        ``` {#codeblock_8zo_2bg_g1i}
        wget https://nodejs.org/dist/v6.9.5/node-v6.9.5-linux-x64.tar.xz
        ```

    2.  解压文件。

        ``` {#codeblock_1kx_q0s_7cd}
        tar xvf node-v6.9.5-linux-x64.tar.xz
        ```

    3.  创建软链接，您就可以在任意目录下直接使用node和npm命令。

        ``` {#codeblock_or6_4uz_0g6}
        ln -s /root/node-v6.9.5-linux-x64/bin/node /usr/local/bin/node
        ln -s /root/node-v6.9.5-linux-x64/bin/npm /usr/local/bin/npm
        ```

    4.  查看node、npm版本。

        ``` {#codeblock_wy9_9jx_9xx}
        node -v
        npm -v
        ```

        至此，Node.js环境已安装完毕。软件默认安装在/root/node-v6.9.5-linux-x64/目录下。

    5.  如果需要将该软件安装到其他目录（例如：/opt/node/）下，请进行如下操作：

        ``` {#codeblock_4lp_n3t_ho3}
        mkdir -p /opt/node/
        mv /root/node-v6.9.5-linux-x64/* /opt/node/
        rm -f /usr/local/bin/node
        rm -f /usr/local/bin/npm
        ln -s /opt/node/bin/node /usr/local/bin/node
        ln -s /opt/node/bin/npm /usr/local/bin/npm
        ```

-   使用NVM安装多版本

    NVM（Node Version Manager）是Node.js的版本管理软件，使您可以轻松在Node.js各个版本间进行切换。适用于长期做node开发的人员或有快速更新node版本、快速切换node版本的场景。

    完成以下操作，使用NVM安装多个Node.js版本：

    1.  使用git将源码克隆到本地的~/.nvm目录下，并检查最新版本。

        ``` {#codeblock_jwr_mwy_406}
        yum install git
        git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
        ```

    2.  激活NVM。

        ``` {#codeblock_vp9_6oy_16w}
        echo ". ~/.nvm/nvm.sh" >> /etc/profile
        source /etc/profile
        ```

    3.  列出Node.js的所有版本。

        ``` {#codeblock_8dh_rk5_h2b}
        nvm list-remote
        ```

    4.  安装多个Node.js版本。

        ``` {#codeblock_ejc_bh1_dv2}
        nvm install v6.9.5
        nvm install v7.4.0
        ```

    5.  运行`nvm ls`查看已安装的Node.js版本，当前使用的版本为v7.4.0。返回结果如下所示。

        ``` {#codeblock_dns_3vf_f14}
        [root@iZXXXXZ .nvm]# nvm ls
              v6.9.5
        ->       v7.4.0
              system
        stable -> 7.4 (-> v7.4.0) (default)
        unstable -> 6.9 (-> v6.9.5) (default)
        ```

    6.  运行`nvm use v7.4.0`切换Node.js版本至v7.4.0。返回结果如下所示。

        ``` {#codeblock_lry_ylh_3q6}
        [root@iZXXXXZ .nvm]# nvm use v7.4.0
        Now using node v7.4.0
        ```


## 步骤三：部署测试项目 {#section_igz_e58_4zq .section}

完成以下操作，部署测试项目：

1.  新建项目文件example.js。 

    ``` {#codeblock_9zl_b7a_mna}
    cd ~
    touch example.js
    ```

2.  修改项目文件example.js。 
    1.  运行以下命令打开example.js。 

        ``` {#codeblock_lxg_3eo_kvh}
        vim example.js
        ```

    2.  按i进入编辑模式。
    3.  将以下项目文件内容粘贴到文件中。 

        ``` {#codeblock_n9u_2im_d02}
        const http = require('http');
        const hostname = '0.0.0.0';
        const port = 3000;
        const server = http.createServer((req, res) => { 
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Hello World\n');
        }); 
        
        server.listen(port, hostname, () => { 
            console.log(`Server running at http://${hostname}:${port}/`);
        });
        ```

        **说明：** 本示例中，项目配置的端口号为3000。实际应用过程中，您可以自行配置端口号，但是必须在ECS实例安全组的入方向添加安全组规则，放行您配置的端口号。具体操作，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

    4.  按Esc退出编辑模式，然后输入:wq并回车以保存并关闭文件。
3.  运行项目。 

    ``` {#codeblock_90o_q0j_lem}
    node ~/example.js &
    ```

4.  运行以下命令查看是否在监听项目端口。 

    ``` {#codeblock_9t9_jpx_49t}
    netstat -tpln
    ```

    本示例中，返回的结果列表中包含端口3000，表明项目正常运行。

5.  登录[ECS管理控制台](https://ecs.console.aliyun.com)，并在ECS实例安全组的入方向添加规则， 放行项目中配置的端口（本示例中端口号为3000）。 添加安全组规则的具体步骤，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
6.  在本地机器的浏览器中输入`http://<ECS实例公网IP地址>:端口号`访问项目。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9770/156715038912144_zh-CN.png)


**相关文档**  


[云中沙箱平台](https://edu.cloudcare.cn/courses/646394e08b66441ab43f7a5e037a318e/detail)

[云市场](https://market.aliyun.com/software)

