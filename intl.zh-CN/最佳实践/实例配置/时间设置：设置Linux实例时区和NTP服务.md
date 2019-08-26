# 时间设置：设置Linux实例时区和NTP服务 {#TimeCalibrationLinux .task}

目前，所有地域的阿里云ECS实例的默认时区为CST（China Standard Time），您可以根据自己的业务需求并参照本文为ECS实例设置或者修改时区。此外，NTP（Network Time Protocol）服务能保证您的云服务器ECS的时间与标准时间同步，您可以根据本文配置NTP服务。

时区和时间的同步性对于云服务器很重要（例如您在更新数据库时，时间的准确性对业务的影响会非常大），为避免实例上运行的业务逻辑混乱和避免网络请求错误，您需要将一台或多台实例设置在同一时区下，比如`Asia/Shanghai`或`America/Los Angeles`。此处以Centos 6.5实例为例，列举通过修改配置文件修改时区的方法：

**说明：** 修改时区后，请切记您需要运行`hwclock -w`更新实例硬件时钟。

1.  [远程连接](../../../../intl.zh-CN/用户指南/连接实例/连接实例概述.md#) Linux实例。 

    **说明：** 

    您需要以root身份打开并编辑时区配置文件，所以此处使用`sudo`命令。

2.  执行命令`sudo rm /etc/localtime`删除系统里的当地时间链接。 
3.  执行命令`sudo vi /etc/sysconfig/clock`用vim打开并编辑配置文件/etc/sysconfig/clock。 
4.  输入`i`添加时区城市，例如添加`Zone=Asia/Shanghai`，按下Esc键退出编辑并输入`:wq`保存并退出。 

    可执行命令`ls /usr/share/zoneinfo`查询时区列表，`Shanghai`为列表条目之一。

5.  执行命令`sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`更新时区修改内容。 
6.  执行命令`hwclock -w`更新硬件时钟（RTC）。 
7.  执行命令`sudo reboot`重启实例。 
8.  执行命令`date -R`查看时区信息是否生效，未生效可重走一遍步骤。 

Linux系统有`ntpd`和`ntpdate`两种方式实现NTP时间同步，其中，`ntpd`同步时间为步进式的逐渐调整时间，`ntpdate`为断点更新。新购实例可使用`ntpdate`更新服务，已经运行业务的实例建议使用`ntpd`同步时间。此处提供标准NTP服务配置和自定义NTP服务配置，您可以根据需要选择性地配置。关于更多NTP服务信息请参考 [内网和公共NTP服务器](intl.zh-CN/最佳实践/实例配置/时间配置：NTP服务器与其他基础服务.md#)。

**前提条件**

NTP服务的通信端口为UDP 123，设置NTP服务之前请确保您已经打开UDP 123端口。您可以通过`netstat -nupl`查看实例是否开通UDP 123端口。您可以参考文档 [添加安全组规则](../../../../intl.zh-CN/用户指南/安全组/添加安全组规则.md#) 放行UDP 123端口。

**启用标准NTP服务**

1.  [远程连接](../../../../intl.zh-CN/用户指南/连接实例/连接实例概述.md#) Linux实例。
2.  执行命令`sudo service ntpd start`运行NTP服务。
3.  执行命令`chkconfig ntpd on`启用NTP服务。
4.  执行命令`ntpstat`查看是否启用了NTP服务。
5.  （可选）执行命令`ntpq -p`可查看NTP服务对等端的列表信息；执行命令`sudo chkconfig --list ntpd`可查看NTP服务的运行级别。

**配置自定义NTP服务**

1.  [远程连接](../../../../intl.zh-CN/用户指南/连接实例/连接实例概述.md#) Linux实例。
2.  执行命令`sudo vi /etc/ntp.conf`用vim打开并编辑NTP服务配置文件。
3.  找到`server ntp 服务器 iburst`的信息后，输入`i`开始编辑文件，给您暂时不需要的NTP服务器句首加上`#`隐藏起来。
4.  新添加一行NTP服务器信息，格式为：`server 您需要添加的NTP服务器 iburst`。完成编辑后按下Esc键并输入`:wq`保存退出。
5.  执行命令`sudo service ntpd start`启用自定义的NTP服务。
6.  执行命令`chkconfig ntpd on`，启用NTP服务。
7.  执行命令`ntpstat`查看是否启用了NTP服务。

