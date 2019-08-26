# Build LNMP environment under CentOS 6 {#concept_rqy_ww2_2fb .concept}

This article describes how to build LNMP environment under CentOS on an ECS instance with the basic configuration.

-   Linux: A family of free and open-source UNIX-like software operating systems \(OS\).
-   Nginx: A lightweight HTTP and reverse proxy server.
-   MySQL: A relational database management system.
-   PHP: A scripting language that is especially suited for web development.

## Audience {#section_pmz_2x2_2fb .section}

This method is applicable to individual users who are familiar with Linux, but new to website construction by using Alibaba Cloud ECS.

## Procedure {#section_ghz_hx2_2fb .section}

Follow these steps to build LNMP environment on an ECS instance:

1.  Prepare the compiling environment.
2.  Install Nginx.
3.  Install MySQL.
4.  Install MySQL.
5.  Test.

**Step 1: Prepare the compiling environment**

Follow these steps to prepare the compiling environment. You can also buy LNMP images at the [Cloud Market](https://partners-intl.aliyun.com/marketplace/vodafone/) to start your ECS instance for website quick building.

1.  Check the version of the operating system.

    ```
    # cat /etc/redhat-release 
    CentOS release 6.5 (Final)
    ```

    **Note:** This article is based on a Linux instance running CentOS 6.5. You may have different OS versions. The same is applicable to the Nginx, MySQL, and PHP versions mentioned in the following paragraphs.

2.  Disable SELINUX.

    Run the command to modify the configuration file, which permanently takes effect after you restart the service.

    ```
    # sed -i 's/SELINUX=. */SELINUX=disabled/g' /etc/selinux/config
    ```

    Run the command to make the configuration take effect immediately.

    ```
    # setenforce 0
    ```

3.  Security group setting.

    Add a security rule to accept Internet access to the Web server on the instance.


**Step 2: Install Nginx**

Nginx is a small and highly-efficient Web server based on Linux. Follow these steps to install Nginx:

1.  Add a user to run the Nginx service process.

    ```
    # groupadd -r nginx    
    # useradd -r -g nginx  nginx
    ```

2.  Download the source code package, decompress it, and then compile.

    ```
    # wget http://nginx.org/download/nginx-1.10.2.tar.gz
    # tar xvf nginx-1.10.2.tar.gz -C /usr/local/src
    # yum groupinstall "Development tools"
    # yum -y install gcc wget gcc-c++ automake autoconf libtool libxml2-devel libxslt-devel perl-devel perl-ExtUtils-Embed pcre-devel openssl-devel
    # cd /usr/local/src/nginx-1.10.2
    # ./configure \
    --prefix=/usr/local/nginx \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --pid-path=/var/run/nginx.pid \
    --lock-path=/var/run/nginx.lock \
    --http-client-body-temp-path=/var/tmp/nginx/client \
    --http-proxy-temp-path=/var/tmp/nginx/proxy \
    --http-fastcgi-temp-path=/var/tmp/nginx/fcgi \
    --http-uwsgi-temp-path=/var/tmp/nginx/uwsgi \
    --http-scgi-temp-path=/var/tmp/nginx/scgi \
    --user=nginx \
    --group=nginx \
    --with-pcre \
    --with-http_v2_module \
    --with-http_ssl_module \
    --with-http_realip_module \
    --with-http_addition_module \
    --with-http_sub_module \
    --with-http_dav_module \
    --with-http_flv_module \
    --with-http_mp4_module \
    --with-http_gunzip_module \
    --with-http_gzip_static_module \
    --with-http_random_index_module \
    --with-http_secure_link_module \
    --with-http_stub_status_module \
    --with-http_auth_request_module \
    --with-mail \
    --with-mail_ssl_module \
    --with-file-aio \
    --with-ipv6 \
    --with-http_v2_module \
    --with-threads \
    --with-stream \
    --with-stream_ssl_module
    # make && make install
    # mkdir -pv /var/tmp/nginx/client
    ```

3.  Add a SysV startup script.

    ```
    # vim /etc/init.d/nginx
    #!/bin/sh 
    # 
    # nginx - this script starts and stops the nginx daemon 
    # 
    # chkconfig:   - 85 15 
    # description: Nginx is an HTTP(S) server, HTTP(S) reverse \ 
    #               proxy and IMAP/POP3 proxy server 
    # processname: nginx 
    # config:      /etc/nginx/nginx.conf 
    # config:      /etc/sysconfig/nginx 
    # pidfile:     /var/run/nginx.pid 
    # Source function library. 
    . /etc/rc.d/init.d/functions
    # Source networking configuration. 
    . /etc/sysconfig/network
    # Check that networking is up. 
    [ "$NETWORKING" = "no" ] && exit 0
    nginx="/usr/sbin/nginx"
    prog=$(basename $nginx)
    NGINX_CONF_FILE="/etc/nginx/nginx.conf"
    [ -f /etc/sysconfig/nginx ] && . /etc/sysconfig/nginx
    lockfile=/var/lock/subsys/nginx
    start() {
     [ -x $nginx ] || exit 5
     [ -f $NGINX_CONF_FILE ] || exit 6
     echo -n $"Starting $prog: " 
     daemon $nginx -c $NGINX_CONF_FILE
     retval=$?
     echo 
     [ $retval -eq 0 ] && touch $lockfile
     return $retval
    }
    stop() {
     echo -n $"Stopping $prog: " 
     killproc $prog -QUIT
     retval=$?
     echo 
     [ $retval -eq 0 ] && rm -f $lockfile
     return $retval
    killall -9 nginx
    }
    restart() {
     configtest || return $?
     stop
     sleep 1
     start
    }
    reload() {
     configtest || return $?
     echo -n $"Reloading $prog: " 
     killproc $nginx -HUP
    RETVAL=$?
     echo 
    }
    force_reload() {
     restart
    }
    configtest() {
    $nginx -t -c $NGINX_CONF_FILE
    }
    rh_status() {
     status $prog
    }
    rh_status_q() {
     rh_status >/dev/null 2>&1
    }
    case "$1" in
     start)
         rh_status_q && exit 0
     $1
         ;;
     stop)
         rh_status_q || exit 0
         $1
         ;;
     restart|configtest)
         $1
         ;;
     reload)
         rh_status_q || exit 7
         $1
         ;;
     force-reload)
         force_reload
         ;;
     status)
         rh_status
         ;;
     condrestart|try-restart)
         rh_status_q || exit 0
             ;;
     *)
       echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}" 
         exit 2
    esac
    ```

4.  Grant the permission to run the script.

    ```
    # chmod +x /etc/init.d/nginx
    ```

5.  Add Nginx to the service management list, and set it to automatically start on startup.

    ```
    # chkconfig --add nginx
    # chkconfig  nginx on
    ```

6.  Start the service.

    ```
    # service nginx start
    ```

7.  Access the instance by using http://Public IP address. If the following page appears, Nginx is installed successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9763/153949532212982_en-US.png)


**Step3: Install MySQL**

1.  Prepare the compiling environment.

    ```
    # yum groupinstall "Server Platform Development"  "Development tools" -y
    # yum install cmake -y
    ```

2.  Create a directory to store the data of MySQL.

    ```
    # mkdir /mnt/data
    # groupadd -r mysql
    # useradd -r -g mysql -s /sbin/nologin mysql
    # id mysql
    uid=497(mysql) gid=498(mysql) groups=498(mysql)
    ```

3.  Change the owner and group of the data directory.

    ```
    # chown -R mysql:mysql /mnt/data
    ```

4.  Decompress and compile the stable source code package downloaded from [MySQL official website](https://www.mysql.com/). In this article, we use version 5.6.24.

    ```
    # tar xvf mysql-5.6.24.tar.gz -C  /usr/local/src
    # cd /usr/local/src/mysql-5.6.24
    # cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
    -DMYSQL_DATADIR=/mnt/data \
    -DSYSCONFDIR=/etc \
    -DWITH_INNOBASE_STORAGE_ENGINE=1 \
    -DWITH_ARCHIVE_STORAGE_ENGINE=1 \
    -DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
    -DWITH_READLINE=1 \
    -DWITH_SSL=system \
    -DWITH_ZLIB=system \
    -DWITH_LIBWRAP=0 \
    -DMYSQL_TCP_PORT=3306 \
    -DMYSQL_UNIX_ADDR=/tmp/mysql.sock \
    -DDEFAULT_CHARSET=utf8 \
    -DDEFAULT_COLLATION=utf8_general_ci
    # make && make install
    ```

5.  Change the group of the installation directory to mysql.

    ```
    # chown -R mysql:mysql /usr/local/mysql/
    ```

6.  Initializes the database.

    ```
    # /usr/local/mysql/scripts/mysql_install_db --user=mysql --datadir=/mnt/data/
    ```

    **Note:** After completing the minimum installation of the CentOS 6.5 operating system, a my.cnf file is generated under the /etc directory. You must rename this file. For example, rename it as /etc/my.cnf.bak. Otherwise, this file will interfere with the correct configuration for MySQL source code installation, leading to MySQL start failure.

7.  Copy the configuration file and startup script.

    ```
    # cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
    # chmod +x /etc/init.d/mysqld
    # cp support-files/my-default.cnf /etc/my.cnf
    ```

8.  Set automatic start on startup.

    ```
    # chkconfig mysqld  on 
    # chkconfig --add mysqld
    ```

9.  Modify the installation path and data storage path in the configuration file.

    ```
    # echo -e "basedir = /usr/local/mysql\ndatadir = /mnt/data\n" >> /etc/my.cnf
    ```

10. Set the PATH environment variable.

    ```
    # echo "export PATH=$PATH:/usr/local/mysql/bin" > /etc/profile.d/mysql.sh      
    # source /etc/profile.d/mysql.sh
    ```

11. Start the service.

    ```
    # service mysqld start 
    # mysql -h 127.0.0.1
    ```


**Step 4: Install PHP-FPM**

Nginx cannot process PHP. As a Web server, when Nginx receives a request, it does not support directly calling or parsing the external program. It must use FastCGI to call such programs. However, in case of PHP requests, Nginx will transfer the request to a PHP interpreter, and return the result to the client. PHP-FPM is a FastCGI process manager that supports parsing PHP code. PHP-FPM provides better PHP process management methods, which can effectively control the memory and process, and can support smoothly reloading PHP configuration.

1.  Install dependency package.

    ```
    # yum install libmcrypt libmcrypt-devel mhash mhash-devel libxml2 libxml2-devel bzip2 bzip2-devel
    ```

2.  Decompress the source code package downloaded from the official website, and then compile and install it.

    ```
    # tar xvf php-5.6.23.tar.bz2 -C /usr/local/src
    # cd /usr/local/src/php-5.6.23
    # ./configure --prefix=/usr/local/php \
    --with-config-file-scan-dir=/etc/php.d \
    --with-config-file-path=/etc \
    --with-mysql=/usr/local/mysql \
    --with-mysqli=/usr/local/mysql/bin/mysql_config \
    --enable-mbstring \
    --with-freetype-dir \
    --with-jpeg-dir \
    --with-png-dir \
    --with-zlib \
    --with-libxml-dir=/usr \
    --with-openssl \
    --enable-xml \
    --enable-sockets \
    --enable-fpm \
    --with-mcrypt \
    --with-bz2
    # make && make install
    ```

3.  Add the PHP and PHP-FPM configuration files.

    ```
    # cp /usr/local/src/php-5.6.23/php.ini-production /etc/php.ini
    # cd /usr/local/php/etc/
    # cp php-fpm.conf.default php-fpm.conf
    # sed -i 's@;pid = run/php-fpm.pid@pid = /usr/local/php/var/run/php-fpm.pid@' php-fpm.conf
    ```

4.  Add the PHP-FPM startup script.

    ```
    # cp /usr/local/src/php-5.6.23/sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
    # chmod +x /etc/init.d/php-fpm
    ```

5.  Add PHP-FPM to the service list, and set it to automatically start on startup.

    ```
    # chkconfig --add php-fpm     
    # chkconfig --list php-fpm     
    # chkconfig php-fpm on
    ```

6.  Start the service.

    ```
    # service php-fpm start
    ```

7.  Follow these steps to configure Nginx to support fastcgi: Back up the default configuration file.

    ```
    # cp /etc/nginx/nginx.conf /etc/nginx/nginx.confbak
    # cp /etc/nginx/nginx.conf.default /etc/nginx/nginx.conf
    ```

    Edit /etc/nginx/nginx.conf: Add a home page in the PHP format into the supported home page formats as follows.

    ```
    location / {
      root   /usr/local/nginx/html;
      index  index.php index.html index.htm;
    }
    ```

    Delete comments in front of the following content.

    ```
    location ~ \.php$ {
      root           /usr/local/nginx/html;
      fastcgi_pass    127.0.0.1:9000;
      fastcgi_index   index.php;
      fastcgi_param  SCRIPT_FILENAME  /usr/local/nginx/html/$fastcgi_script_name;
      include        fastcgi_params;
    }
    ```

    Reload the Nginx configuration file.

    ```
    # service nginx reload
    ```

    Create an index.php test page under /usr/local/nginx/html/, the content of which is shown as follows.

    ```
    # cat index.php 
    <?php
    $conn=mysql_connect('127.0.0.1','root','');
    if ($conn){
    echo "LNMP platform connect to mysql is successful!";
    }else{
    echo "LNMP platform connect to mysql is failed!";
    }
    phpinfo();
    ?>
    ```

    Access the instance by using http://Public IP address/index.php. If the following page appears, LNMP environment is built successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9763/153949532212981_en-US.png)


