# PostgreSQL 本地Slave搭建步骤 {#concept_gqk_kd5_2fb .concept}

PostgreSQL 被业界誉为最先进的开源数据库，目前阿里云数据库 PostgreSQL 版具有 NoSQL 兼容，高效查询，插件化管理，安全稳定的特性。本文档介绍使用阿里云 ECS 搭建 PostgreSQL 主从架构的操作步骤。

## 适用对象 {#section_opp_ld5_2fb .section}

适用于熟悉 ECS，熟悉 Linux 系统，熟悉 PostgreSQL 的阿里云用户。

## 前提条件 {#section_evn_md5_2fb .section}

已在安全组中添加规则放行 5432 端口。

## 基本流程 {#section_k1g_nd5_2fb .section}

使用阿里云 ECS 搭建 PostgreSQL 主从架构的操作步骤如下：

1.  选购 ECS 实例。
2.  主节点安装配置。
3.  从节点安装配置。
4.  检测验证。

**步骤 1：选购 ECS 实例**

搭建主从复制架构，需要选购2台专有网络类型的云服务器ECS实例，建议不分配公网IP，可按需购买 [弹性公网IP](https://help.aliyun.com/document_detail/51995.html) 绑定至对应ECS实例，进行配置操作。后续使用您可以根据实际情况考虑配置升级或者架构调优变更。

**步骤 2：安装 PostgreSQL**

在阿里云服务器上安装 PostgreSQL 有 2 种方式：

-   镜像部署
-   手动部署（源码编译安装/YUM安装）

本文档基于yum部署的方式，安装postgresql；您也可以在 [云市场基础环境](https://market.aliyun.com/software?spm=5176.doc51375.2.5.es71xO) 中搜索筛选，使用镜像部署，更加快捷方便。

本文环境软件明细：`CentOS 7.2 |PostgreSQL (9.5.6)`

**步骤 3：PostgreSQL 主节点配置**

1.  主节点上执行以下命令安装 PostgreSQL。

    ```
    # yum update -y 
     # yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-2.noarch.rpm -y
     # yum install postgresql95-server postgresql95-contrib -y
     # /usr/pgsql-9.5/bin/postgresql95-setup initdb
     # systemctl enable postgresql-9.5.service
     # systemctl start postgresql-9.5.service
    ```

2.  主节点上创建进行主从复制的数据库账号，并设置密码及登录和备份权限。

    ```
    # su - postgres
     # psql
     postgres=# CREATE ROLE replica login replication encrypted password 'replica';
     CREATE ROLE
     postgres=# SELECT usename from pg_user ;
     usename  
     ----------
     postgres
     replica
     (2 rows)
     postgres=# SELECT rolname from pg_roles ;
     rolname  
     ----------
     postgres
     replica
     (2 rows)
    ```

3.  修改pg\_hba.conf，设置replica用户白名单。

    ```
    # vim /var/lib/pgsql/9.5/data/pg_hba.conf
    ```

    在IPv4 local connections段添加下面两行内容。

    host all all 192.168.1.0/24 md5 允许VPC网段中md5密码认证连接 host replication replica 192.168.1.0/24 md5 允许用户从replication数据库进行数据同步。

4.  修改postgresql.conf。

    ```
    # vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    设置以下参数：

    -   wal\_level = hot\_standby 启用热备模式
    -   synchronous\_commit = on 开启同步复制
    -   max\_wal\_senders = 32 同步最大的进程数量
    -   wal\_sender\_timeout = 60s 流复制主机发送数据的超时时间
    -   max\_connections = 100 最大连接数，从库的max\_connections必须要大于主库的
5.  重启服务。

    ```
    # systemctl restart postgresql-9.5.service
    ```


**步骤 4：PostgreSQL从节点配置**

1.  安装postgres。

    ```
    # yum update -y
        # yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-        x86_64/pgdg-centos95-9.5-2.noarch.rpm -y
        # yum install postgresql95-server postgresql95-contrib -y
    ```

2.  使用pg\_basebackup基础备份的工具制定备份目录。

    ```
    # pg_basebackup -D /var/lib/pgsql/9.5/data -h 主节点IP -p 5432 -U replica -X stream -P
         Password: 
         30075/30075 kB (100%), 1/1 tablespace
    ```

3.  添加并修改recovery.conf。

    ```
    # cp /usr/pgsql-9.5/share/recovery.conf.sample /var/lib/pgsql/9.5/data/recovery.conf
     # vim /var/lib/pgsql/9.5/data/recovery.conf
    ```

    设置以下参数。

    -   standby\_mode = on \# 声明此节点为从库
    -   primary\_conninfo = ‘host=主节点IP port=5432 user=replica password=replica’ \# 对应主库的连接信息
    -   recovery\_target\_timeline = ‘latest’ \# 流复制同步到最新的数据
4.  修改postgresql.conf。

    ```
    # vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    设置以下参数。

    ```
    - max_connections = 1000             # 最大连接数，从节点需设置比主节点大
     - hot_standby = on                   # 开启热备
     - max_standby_streaming_delay = 30s  # 数据流备份的最大延迟时间
     - wal_receiver_status_interval = 1s  # 从节点向主节点报告自身状态的最长间隔时间
     - hot_standby_feedback = on          # 如果有错误的数据复制向主进行反馈
    ```

5.  修改数据目录属组属主。

    ```
    # chown -R postgres.postgres /var/lib/pgsql/9.5/data
    ```

6.  启动服务，设置开机自启。

    ```
    # systemctl start postgresql-9.5.service
     # systemctl enable postgresql-9.5.service
    ```


**步骤 5：检测验证**

1.  主节点中可查看到sender进程。

    ```
    # ps aux |grep sender
         postgres  2916  0.0  0.3 340388  3220 ?        Ss   15:38   0:00 postgres: wal sender     process replica 192.168.1.222(49640) streaming 0/F01C1A8
    ```

2.  从节点中可查看到receiver进程。

    ```
    # ps aux |grep receiver
     postgres 23284  0.0  0.3 387100  3444 ?        Ss   16:04   0:00 postgres: wal receiver process   streaming 0/F01C1A8
    ```

3.  主库中可查看到从库状态。

    ```
    
    replication=# select * from pg_stat_replication;
    pid | usesysid | usename | application_name | client_addr | client_hostname | client_port | backend_start | backend_xmin | state | sent_location | write_locati
    on | flush_location | replay_location | sync_priority | sync_state 
    ------+----------+---------+------------------+---------------+-----------------+------------- +-------------------------------+--------------+-----------+---------------+-------------
    ---+----------------+-----------------+---------------+------------
    2916 | 16393 | replica | walreceiver | 192.168.1.222 | | 49640 | 2017-05-02 15:38:06.188988+08 | 1836 | streaming | 0/F01C0C8 | 0/F01C0C8 
    | 0/F01C0C8 | 0/F01C0C8 | 0 | async
    (1 rows)
    ```


