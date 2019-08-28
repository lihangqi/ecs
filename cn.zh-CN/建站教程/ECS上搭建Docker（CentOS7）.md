# ECS上搭建Docker（CentOS7） {#concept_zmh_cpt_2fb .task}

本文介绍在CentOS系统上部署Docker的过程。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

本教程适用于熟悉Linux操作系统，刚开始使用阿里云ECS的开发者。

本教程示例步骤中使用的操作系统版本为`CentOS 7.2 64 3.10.0-514.6.2.el7.x86_64`。

**说明：** Docker要求64位的系统且内核版本至少为3.10。

## 主要内容 {#section_z74_yzt_kll .section}

本文主要介绍以下内容：

1.  [部署Docker](#section_gtl_cjs_ls2)
2.  [使用Docker](#section_x1c_w5u_5wb)
3.  [制作镜像](#section_i4r_m92_6ev)

## 部署Docker {#section_gtl_cjs_ls2 .section}

本节主要介绍手动安装Docker的操作步骤，您也可以在[云市场](https://market.aliyun.com/software)购买相应镜像，一键部署云服务器。

完成以下操作，部署Docker：

1.  添加yum源。 

    ``` {#codeblock_oax_1zi_ap3}
    # yum install epel-release –y
    # yum clean all
    # yum list
    ```

2.  安装并运行Docker。 

    ``` {#codeblock_zlr_hzt_wka}
    # yum install docker-io –y
    # systemctl start docker
    ```

3.  检查安装结果。 

    ``` {#codeblock_two_otm_v80}
    # docker info
    ```

    出现以下说明信息则表明安装成功。

    ![安装结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9774/156689253712347_zh-CN.png)


## 使用Docker {#section_x1c_w5u_5wb .section}

Docker有以下基本用法：

1.  管理Docker守护进程。

    ``` {#codeblock_g78_mck_ka9}
    # systemctl start docker     #运行Docker守护进程
    # systemctl stop docker      #停止Docker守护进程
    # systemctl restart docker   #重启Docker守护进程
    ```

2.  管理镜像。本文使用的是来自阿里云仓库的Apache镜像。

    ``` {#codeblock_437_xrc_5uf}
    # docker pull registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
    ```

    -   修改标签。由于阿里云仓库镜像的镜像名称很长，可以修改镜像标签以便记忆区分。

        ``` {#codeblock_dnc_jwg_vjz}
        # docker tag registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5:latest aliweb:v1
        ```

    -   查看已有镜像。

        ``` {#codeblock_7w9_io8_tkt}
        # docker images
        ```

    -   强制删除镜像。

        ``` {#codeblock_u3g_lox_mnd}
        # docker rmi –f registry.cn-hangzhou.aliyuncs.com/lxepoo/apache-php5
        ```

3.  管理容器。
    -   进入容器。e1xxxxxxxxxe是执行`docker images`命令查询到的ImageId，使用`docker run`命令进入容器。

        ``` {#codeblock_6jg_70g_z3a}
        # docker run –ti e1xxxxxxxxxe /bin/bash
        ```

    -   退出容器。使用`exit`命令退出当前容器。
    -   `run`命令加上`–d`参数可以在后台运行容器，`--name`指定容器命名为apache。

        ``` {#codeblock_cor_erv_3y9}
        # docker run -d --name apache e1xxxxxxxxxe
        ```

    -   进入后台运行的容器。

        ``` {#codeblock_sb8_qj2_ixc}
        # docker exec -ti apache /bin/bash
        ```

    -   将容器做成镜像。

        ``` {#codeblock_uio_yf5_dqr}
        # docker commit containerID/containerName newImageName:tag
        ```

    -   为了方便测试和恢复，将源镜像运行起来后，再做一个命名简单的镜像做测试。

        ``` {#codeblock_ulh_jkh_zof}
        # docker commit 4c8066cd8c01 apachephp:v1
        ```

    -   运行容器并将宿主机的8080端口映射到容器里去。

        ``` {#codeblock_lmf_y0l_pbk}
        # docker run -d -p 8080:80 apachephp:v1
        ```

        在浏览器输入宿主机IP加8080端口访问测试，出现以下内容则说明运行成功。

        ![映射结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9774/156689253712348_zh-CN.png)


## 制作镜像 {#section_i4r_m92_6ev .section}

完成以下操作，制作镜像：

1.  准备Dockerfile内容。 

    ``` {#codeblock_801_vp5_n6z}
    # vim Dockerfile 
    FROM apachephp:v1  #声明基础镜像来源
    MAINTAINER DTSTACK #声明镜像拥有者
    RUN mkdir /dtstact #RUN后面接容器运行前需要执行的命令，由于Dockerfile文件不能超过127行，因此当命令较多时建议写到脚本中执行
    ENTRYPOINT ping www.aliyun.com #开机启动命令，此处最后一个命令需要是可在前台持续执行的命令，否则容器后台运行时会因为命令执行完而退出。
    ```

2.  构建镜像。 

    ``` {#codeblock_zfk_4ru_3u6}
    docker build -t webcentos:v1 .   # . 是Dockerfile文件的路径，不能忽略
    docker images                    #查看是否创建成功
    docker run –d webcentos:v1       #后台运行容器
    docker ps                        #查看当前运行中的容器
    docker ps –a                     #查看所有容器，包括未运行中的
    docker logs CONTAINER ID/IMAGE   #如未查看到刚才运行的容器，则用容器id或者名字查看启动日志排错
    docker commit fb2844b6c070 dtstackweb:v1 #commit 后接容器id 和构建新镜像的名称和版本号。
    docker images                    #列出本地（已下载的和本地创建的）镜像
    docker push                      #将镜像推送至远程仓库，默认为 Docker Hub
    ```

3.  将镜像推送到registry。 

    其中ImageId和镜像版本号请您根据自己的镜像信息进行填写。

    ``` {#codeblock_72z_475_vtp}
    docker login --username=dtstack_plus registry.cn-shanghai.aliyuncs.com #执行后输入镜像仓库密码
    docker tag [ImageId] registry.cn-shanghai.aliyuncs.com/dtstack123/test:[镜像版本号]
    docker push registry.cn-shanghai.aliyuncs.com/dtstack123/test:[镜像版本号]
    ```

    在镜像仓库能查看到镜像版本信息则说明推送成功。


