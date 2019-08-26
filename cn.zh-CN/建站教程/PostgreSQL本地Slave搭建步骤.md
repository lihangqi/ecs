# PostgreSQL本地Slave搭建步骤 {#concept_gqk_kd5_2fb .concept}

PostgreSQL被业界誉为最先进的开源数据库。目前阿里云数据库PostgreSQL版具有NoSQL兼容、高效查询、插件化管理、安全稳定的特性。本文档介绍使用阿里云服务器ECS搭建PostgreSQL主从架构的操作步骤。

## 项目配置 {#section_dp7_37f_sgz .section}

本教程在示例步骤中使用了以下版本的软件。操作时，请您以实际软件版本为准。

-   操作系统：CentOS 7.2
-   PostgreSQL：9.5.6

## 适用对象 {#section_opp_ld5_2fb .section}

熟悉阿里云服务器ECS、Linux系统、PostgreSQL的阿里云用户。

## 前提条件 {#section_evn_md5_2fb .section}

已在安全组入方向中添加规则放行5432端口。具体步骤，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 基本流程 {#section_k1g_nd5_2fb .section}

在阿里云服务器ECS上安装PostgreSQL有以下2种方式：

-   镜像部署（在[云市场基础环境](https://market.aliyun.com/software?spm=5176.doc51375.2.5.es71xO)中，搜索筛选PostgreSQL镜像）
-   手动部署（源码编译安装/yum安装）

本教程基于yum方式手动安装并搭建PostgreSQL主从复制架构，操作步骤如下：

1.  [选购ECS实例](#section_pav_wid_h44)
2.  [PostgreSQL主节点配置](#section_qgn_13v_8op)
3.  [PostgreSQL从节点配置](#section_o5u_jgk_048)
4.  [检测验证](#section_rk4_uqg_m71)

## 步骤一 选购ECS实例 {#section_pav_wid_h44 .section}

搭建主从复制架构，需要选购2台专有网络类型的ECS实例，一台ECS实例作为主节点，另一台ECS实例作为从节点。

**说明：** 建议您不为ECS实例分配公网IP，按需购买[弹性公网IP](https://help.aliyun.com/document_detail/51995.html)绑定至ECS实例，后续您可以根据实际情况考虑升级配置或调优架构。

## 步骤二 PostgreSQL主节点配置 {#section_qgn_13v_8op .section}

1.  在主节点上依次运行以下命令安装PostgreSQL。

    ``` {#codeblock_akm_4ar_g40}
    yum update -y
    ```

    ``` {#codeblock_ulv_0zj_ze3}
    yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-3.noarch.rpm -y
    ```

    ``` {#codeblock_zw8_rsp_187}
    yum install postgresql95-server postgresql95-contrib -y
    ```

    ``` {#codeblock_81v_5wy_jwv}
    /usr/pgsql-9.5/bin/postgresql95-setup initdb
    ```

    **说明：** 本教程以pgdg-centos95-9.5-3.noarch.rpm版本为例。实际安装时，请您使用最新版本。

2.  依次运行以下命令启动服务并设置服务开机自启动。

    ``` {#codeblock_keg_kdr_cja}
    systemctl start postgresql-9.5.service    #启动服务
    ```

    ``` {#codeblock_zs7_yw4_k4o}
    systemctl enable postgresql-9.5.service   #设置服务开机自启动
    ```

3.  在主节点上创建数据库账号replica（用于主从复制），并设置密码及登录权限和备份权限。
    1.  运行以下命令登录postgres。

        ``` {#codeblock_e0u_xdq_kfr}
        su - postgres
        ```

    2.  输入`psql`进入PostgreSQL交互终端。

        ``` {#codeblock_vp1_c7y_owl}
        -bash-4.2$ psql
        ```

    3.  输入以下SQL语句创建数据库账号replica，并设置密码及登录权限和备份权限。

        ``` {#codeblock_ffj_ymy_fxw}
        postgres=# CREATE ROLE replica login replication encrypted password 'replica';
        ```

    4.  查询账号和权限是否创建成功。
        1.  输入以下SQL语句，查询账号是否创建成功。

            ``` {#codeblock_duk_31z_tcb}
            postgres=# SELECT usename from pg_user;
            ```

            返回结果如下，表示已创建成功。

            ``` {#codeblock_45l_4ox_lrt}
            usename  
            ----------
            postgres
            replica
            (2 rows)
            ```

        2.  输入以下SQL语句，查询权限是否创建成功。

            ``` {#codeblock_hyo_tdu_y32}
            postgres=# SELECT rolname from pg_roles;
            ```

            返回结果如下，表示已创建成功。

            ``` {#codeblock_0uf_ivp_hw6}
            rolname  
            ----------
            postgres
            replica
            (2 rows)
            ```

    5.  输入`\q`后，按`Enter`键退出SQL终端。

        ``` {#codeblock_zhz_uaw_kfh}
        postgres=# \q
        ```

    6.  输入`exit`后，按`Enter`键退出postgres。

        ``` {#codeblock_z86_45q_tcb}
        -bash-4.2$ exit
        logout
        ```

4.  运行以下命令打开pg\_hba.conf文件，设置replica用户白名单。

    ``` {#codeblock_zsu_62v_erg}
    vim /var/lib/pgsql/9.5/data/pg_hba.conf
    ```

    在`IPv4 local connections`段添加下面两行内容。

    ``` {#codeblock_qmm_w20_qcu}
    host all all 192.168.1.0/24 md5              #允许VPC网段中md5密码认证连接
    host replication replica 192.168.1.0/24 md5  #允许用户从replication数据库进行数据同步
    ```

5.  运行以下命令打开postgresql.conf文件。

    ``` {#codeblock_ol3_dvb_m44}
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    设置以下参数：

    ``` {#codeblock_nko_7n8_ape}
    wal_level = hot_standby  #启用热备模式
    synchronous_commit = on  #开启同步复制
    max_wal_senders = 32     #同步最大的进程数量
    wal_sender_timeout = 60s #流复制主机发送数据的超时时间
    max_connections = 100    #最大连接数，从库的max_connections必须要大于主库的
    ```

6.  运行以下命令重启服务。

    ``` {#codeblock_1rk_u4e_jjo}
    systemctl restart postgresql-9.5.service
    ```


## 步骤三 PostgreSQL从节点配置 {#section_o5u_jgk_048 .section}

1.  依次运行以下命令安装postgres。

    ``` {#codeblock_w9f_foj_i8h}
    yum update -y
    ```

    ``` {#codeblock_mwo_ybo_dhd}
    yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-2.noarch.rpm -y
    ```

    ``` {#codeblock_ugi_qhw_0tc}
    yum install postgresql95-server postgresql95-contrib -y
    ```

2.  运行以下命令使用pg\_basebackup基础备份工具制定备份目录。

    ``` {#codeblock_trs_q0e_7yx}
    # pg_basebackup -D /var/lib/pgsql/9.5/data -h <主节点IP> -p 5432 -U replica -X stream -P
      Password: 
      30075/30075 kB (100%), 1/1 tablespace
    ```

3.  依次运行以下命令新建并打开recovery.conf文件。

    ``` {#codeblock_ryg_o1l_j44}
    cp /usr/pgsql-9.5/share/recovery.conf.sample /var/lib/pgsql/9.5/data/recovery.conf
    ```

    ``` {#codeblock_z75_x3e_mws}
    vim /var/lib/pgsql/9.5/data/recovery.conf
    ```

    设置以下参数。

    ``` {#codeblock_qy2_kcu_lf7}
    standby_mode = on     #声明此节点为从库
    primary_conninfo = ‘host=<主节点IP> port=5432 user=replica password=replica’ #对应主库的连接信息
    recovery_target_timeline = ‘latest’ #流复制同步到最新的数据
    ```

4.  运行以下命令打开postgresql.conf文件。

    ``` {#codeblock_ccf_t3y_u7k}
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    设置以下参数。

    ``` {#codeblock_xvz_ea0_j8q}
    max_connections = 1000             # 最大连接数，从节点需设置比主节点大
    hot_standby = on                   # 开启热备
    max_standby_streaming_delay = 30s  # 数据流备份的最大延迟时间
    wal_receiver_status_interval = 1s  # 从节点向主节点报告自身状态的最长间隔时间
    hot_standby_feedback = on          # 如果有错误的数据复制向主进行反馈
    ```

5.  运行以下命令修改数据目录的属组和属主。

    ``` {#codeblock_gom_yxb_ss0}
    chown -R postgres.postgres /var/lib/pgsql/9.5/data
    ```

6.  依次运行以下命令启动服务并设置服务开机自启动。

    ``` {#codeblock_tyi_shi_vh5}
    systemctl start postgresql-9.5.service   #启动服务
    ```

    ``` {#codeblock_k3d_ljk_5pg}
    systemctl enable postgresql-9.5.service  #设置服务开机自启动
    ```


## 步骤四 检测验证 {#section_rk4_uqg_m71 .section}

1.  运行以下命令在主节点中查看sender进程。

    ``` {#codeblock_8nn_3qa_8o5}
    ps aux |grep sender
    ```

    返回结果如下，表示可成功查看到sender进程。

    ``` {#codeblock_fok_99a_bo0}
    postgres  2916  0.0  0.3 340388  3220 ?        Ss   15:38   0:00 postgres: wal sender     process replica 192.168.1.222(49640) streaming 0/F01C1A8
    ```

2.  运行以下命令在从节点中查看receiver进程。

    ``` {#codeblock_ezw_i1i_bq0}
    ps aux |grep receiver
    ```

    返回结果如下，表示可成功查看到receiver进程。

    ``` {#codeblock_djf_et5_0xb}
    postgres 23284  0.0  0.3 387100  3444 ?        Ss   16:04   0:00 postgres: wal receiver process   streaming 0/F01C1A8
    ```

3.  输入以下SQL语句，在主库中查看从库状态。

    ``` {#codeblock_uyp_8mf_1by}
    replication=# select * from pg_stat_replication;
    ```

    返回结果如下，表示可成功查看到从库状态。

    ``` {#codeblock_96b_2lb_ltm}
    pid | usesysid | usename | application_name | client_addr | client_hostname | client_port | backend_start | backend_xmin | state | sent_location | write_locati
    on | flush_location | replay_location | sync_priority | sync_state 
    ------+----------+---------+------------------+---------------+-----------------+------------- +-------------------------------+--------------+-----------+---------------+-------------
    ---+----------------+-----------------+---------------+------------
    2916 | 16393 | replica | walreceiver | 192.168.1.222 | | 49640 | 2017-05-02 15:38:06.188988+08 | 1836 | streaming | 0/F01C0C8 | 0/F01C0C8 
    | 0/F01C0C8 | 0/F01C0C8 | 0 | async
    (1 rows)
    ```


