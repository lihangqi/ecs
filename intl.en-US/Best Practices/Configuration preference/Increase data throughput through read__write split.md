# Increase data throughput through read/write split {#concept_bp5_qw5_hfb .concept}

This topic describes how to split read and write operations at the application layer and system layer. To improve overall system performance and optimize user experience, you can reduce the load of your primary database through read/write split.

## Split read and write at the application layer {#section_ndg_sw5_hfb .section}

At the application layer, read/write split is implemented through coding. Before the Service method is called, AOP is used to decide whether to use the read database or the write database. The method names can be used to implement the target action. For example, the read database is used for method names starting with `query`, `find` or `get`, and the write database is used for others.

 **Advantages** 

-   The program easily switches between multiple data sources automatically.
-   Middleware is not required.
-   Currently, any databases are supported.

 **Disadvantages** 

-   Manual operations are not supported.
-   Data sources cannot be added dynamically.

## Split read and write at the system layer {#section_qdg_sw5_hfb .section}

You can use either the Distributed Relational Database Service \(DRDS\) or the middleware MySQL Proxy to split read and write operations at the system layer.

The following procedure describes how to implement read/write split by using MySQL Proxy.

## MySQL Proxy overview {#section_rdg_sw5_hfb .section}

MySQL Proxy is a simple program that is situated between your client and MySQL server and that can monitor, analyze, or transform their communication. Its flexibility allows for a wide variety of uses, including load balancing, failover, query analysis, and query filtering and modification.

MySQL Proxy principle

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790813249_en-US.png)

MySQL Proxy is an intermediate-layer proxy that acts as a connection pool to forward connection requests from the front-end application to the back-end database. By using the lua script, MySQL Proxy can perform complex connection control and filtering to implement read/write split and load balancing. MySQL Proxy is transparent to the application, which only needs to be connected to the listening port of MySQL Proxy. In this case, the proxy server may be considered as a Single Point of Failure \(SPOF\), but the use of multiple proxy servers implements redundancy. Therefore, you only need to configure multiple proxy connections in the connection pool of the application server.

Advantages

-   Read/write split can be implemented without modifying the source program.
-   Data sources can be added dynamically without restarting the program.

Disadvantages

-   The program relies on the middleware, making it difficult to switch databases.
-   Performance decreases because the middleware serves as a forwarding proxy.

## Procedure {#section_udg_sw5_hfb .section}

 **Environment** 

-   Master database IP address: 121.40.18.26
-   Slave database IP address: 101.37.36.20
-   MySQL Proxy IP address: 116.62.101.76

 **Preparations** 

1.  Create three ECS instances and install MySQL.
2.  Build master/slave databases and ensure data consistency.

 **Primary environment** 

1. Modify the MySQL configuration file.

``` {#codeblock_7m4_hk4_mii}
vim /etc/my.cnf
[mysqld]
server-id=202                  # Set the unique ID of the server. The default ID is 1.
log-bin=mysql-bin              # Enable binary logs.
```

 **Secondary environment** 

``` {#codeblock_ot3_0ps_zlt}
[mysqld]
server-id=203
```

2. Restart the MySQL service on the master/slave servers.

``` {#codeblock_r4d_rjh_ftu}
/etc/init.d/mysqld restart
```

3. Create an account on the master server and grant permissions to the slave server.

``` {#codeblock_pzg_zs4_st1}
mysql -uroot -p95c7586783
grant replication slave on *.* to 'syncms'@'Enter slave-IP' identified by '123456';
flush privileges;
```

4. View the primary database status.

``` {#codeblock_0fn_7cf_kug}
mysql> show master status;
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913250_en-US.png)

5. Configure the secondary database.

``` {#codeblock_ydr_kws_vo9}
change master to master_host='Enter master-IP', master_user='syncms',      master_password='123456', master_log_file='mysql-bin. 000005', master_log_pos=602;
```

6. Start the slave synchronization process and view the status.

``` {#codeblock_pkp_2t6_906}
start slave;
show slave status\G
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913251_en-US.png)

7. Verify master/slave synchronization.

 **Operations on the primary database** 

``` {#codeblock_zc5_0ne_eq7}
mysql> create database testproxy;
mysql> create table testproxy.test1(ID int primary key,name char(10) not null);
mysql> insert into testproxy.test1 values(1,'one');
mysql> insert into testproxy.test1 values(2,'two');
mysql> select * from testproxy.test1;
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913252_en-US.png)

**Operations on the secondary database** 

Search the secondary database for the data of the testproxy.test1 table. If the data matches that in the primary database, master/slave synchronization is successful.

``` {#codeblock_0kn_us9_87p}
select * from testproxy.test1;
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913253_en-US.png)

## Configure read/write split {#section_o2g_sw5_hfb .section}

1.  Install MySQL Proxy.

    ``` {#codeblock_yal_418_r5u}
    wget https://cdn.mysql.com/archives/mysql-proxy/mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit.tar.gz
    mkdir /alidata
    tar xvf mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit.tar.gz 
    mv mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit/  /alidata/mysql-proxy-0.8.5
    ```

2.  Set environment variables.

    ``` {#codeblock_r6k_tfx_rln}
    vim /etc/profile                     # Add the following information:
    PATH=$PATH:/alidata/mysql-proxy-0.8.5/bin
    export $PATH
    source /etc/profile                  # Validate the environment variables.
    mysql-proxy -V
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913254_en-US.png)

3.  Set the read-write split parameters.

    ``` {#codeblock_my6_tdy_d6f}
    cd /alidata/mysql-proxy-0.8.5/share/doc/mysql-proxy/
    vim  rw-splitting.lua
    ```

    MySQL Proxy will detect client connections. If the number of connections does not exceed the preset value of `min_idle_connections`, read/write split will not be performed. By default, read/write split will be performed for at least four connections and at most eight connections. To simplify testing read/write split, the number of connections is modified to one at least and two at most, and can be adjusted in real application environments based on your specific needs.

    Before the modification

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351790913255_en-US.png)

    After the modification

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013256_en-US.png)

4.  Copy the lua administration script \(admin.lua\) to the directory where the read-write split script \(rw-splitting.lua\) is located.

    ``` {#codeblock_112_i5f_xz7}
    cp /alidata/mysql-proxy-0.8.5/lib/mysql-proxy/lua/admin.lua /alidata/mysql-proxy-0.8.5/share/doc/mysql-proxy/
    ```


## Grant permissions {#section_x2g_sw5_hfb .section}

1.  Grant permissions in the master database. The permissions will also be granted in the slave database due to master/slave synchronization.

    ``` {#codeblock_vxi_xda_pc4}
    mysql -uroot -p95c7586783
    grant all on *.* to 'mysql-proxy'@'Enter MySQL Proxy IP' identified by '123456';
    flush privileges;
    ```

2.  Start MySQL Proxy.

    ``` {#codeblock_5c6_dck_3v2}
    mysql-proxy --daemon --log-level=debug --log-file=/var/log/mysql-proxy.log --plugins=proxy -b Enter master-IP:3306 -r Enter slave-IP:3306 --proxy-lua-script="/alidata/mysql-proxy-0.8.5/share/doc/mysql-proxy/rw-splitting.lua" --plugins=admin --admin-username="admin" --admin-password="admin" --admin-lua-script="/alidata/mysql-proxy-0.8.5/share/doc/mysql-proxy/admin.lua"
    ```

3.  View the port and relevant processes.

    ``` {#codeblock_zek_aw4_m47}
    netstat -tpln
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013257_en-US.png)

    ``` {#codeblock_wq8_f4n_g0y}
    ps -ef | grep mysql
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013258_en-US.png)


## Test read/write split {#section_ffg_sw5_hfb .section}

1.  Disable slave replication.

    ``` {#codeblock_v63_hve_03y}
    stop slave;
    ```

2.  Log on to the back end of MySQL Proxy.

    ``` {#codeblock_x81_kbn_jxd}
    mysql  -u  admin -padmin -P 4041 -h MySQL-Proxy-IP
    select * from backends;                # View the status.
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013259_en-US.png)

    The first connection will access the master database.

    ``` {#codeblock_9zj_kns_wmd}
    mysql -umysql-proxy -p123456 -h 116.62.101.76 -P 4040
    insert into testproxy.test1 values(3,'three');             # Add a data record. Slave replication is disabled. Therefore, the record exists in the primary database but does not exist in the secondary database.
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013260_en-US.png)

    Create additional test connections. If the data displayed in the testproxy.test1 table is the same as that in the secondary database, read/write split is successful.

    ``` {#codeblock_lm5_cpu_rve}
    mysql -umysql-proxy -p123456 -h 116.62.101.76 -P 4040
    select * from testproxy.test1;
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9808/156351791013261_en-US.png)


