# Time setting: Synchronize NTP servers and change time zone for Linux instances {#TimeCalibrationLinux .task}

The current default time zone for Alibaba Cloud ECS instances across all regions is CST \(China Standard Time\). In addition, the NTP \(Network Time Protocol\) service guarantees that your instances are synchronized with the standard time. Follow these steps in this topic to change the time zone for your ECS instances and configure your NTP service.

Synchronizing time and the time zone is crucial for Elastic Compute Service \(ECS\) instances, for example, an inaccurate time may have a significant impact on business when updating your database. To avoid both business disruptions running on your instances and networking request errors, you must configure one or more instances in the same time zone, such as `Asia/Shanghai` or `America/Los Angeles`. Take CentOS 6.5 as an example to demonstrate how to change the time zone by modifying configuration file.

**Note:** After you change the time zone for an instance, always run `hwclock -w` to update the real-time clock \(RTC\) of the instance.

1.  [Connect](../../../../reseller.en-US/User Guide/Connect to instances/Overview.md#) to the Linux instance. 

    **Note:** 

    Only a root user can open and edit time zone configuration files, so we use the `sudo` command here.

2.  Run `sudo rm /etc/localtime` to delete the local time in the instance. 
3.  Run `sudo vi /etc/sysconfig/clock` to edit the configuration file /etc/sysconfig/clock. 
4.  Enter `i` to add the time zone and city. For example, add `Zone=Asia/Shanghai`. Press Esc to exit the edit and enter `:wq` to save and exit. 

    Optional. Run `ls /usr/share/zoneinfo` to query the list of available time zones. For example, `Shanghai` is one of them.

5.  Run `sudo ln -sf /usr/share/zoneinfo/XXXX/XXXXXXX /etc/localtime` to update the time zone change, for example, run sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime. 
6.  Run `hwclock -w` to update the RTC. 
7.  Run `sudo reboot` to restart the instance. 
8.  Run `date -R` to check whether the new time zone is effective or not. If not, repeat the preceding steps. 

The Linux instance offers the `ntpdate` and the `ntpd` two approaches of synchronizing the NTP service. The `ntpdate` can be used to force an immediate update and the `ntpd` offers a systematic approach. The `ntpdate` service can be used for new instances, whereas `ntpd` is recommended for instances that run your business. Both standard and custom NTP service configurations are provided in this section. For more information about the NTP service, see [internal and public NTP server](reseller.en-US/Best Practices/Configuration preference/Time setting: NTP servers and other public services.md#).

**Prerequisites**

The communication port of the NTP service is UDP 123. Before configuring the service, make sure that you enabled the UDP port 123. You can use `netstat -nupl` in the Linux instance to make sure whether the UDP port 123 is enabled or not. For more information, see [add a security group rule](../../../../reseller.en-US/User Guide/Security groups/Add security group rules.md#).

**Set up standard NTP service**

1.  [Connect](../../../../reseller.en-US/User Guide/Connect to instances/Overview.md#) to the Linux instance.
2.  Run `sudo service ntpd start` to enable the NTP service.
3.  Run `chkconfig ntpd on` to enable the NTP service.
4.  Run `ntpstat` to check whether the NTP service is enabled or not.
5.  Optional. Run `ntpq -p` to view a list of NTP service peers. Run `sudo chkconfig --list ntpd` to view the NTP service running level.

**Set up custom NTP service**

1.  [Connect](../../../../reseller.en-US/User Guide/Connect to instances/Overview.md#) to the Linux instance.
2.  Run `sudo vi /etc/ntp.conf` to edit the NTP service configuration files.
3.  After finding the information about `ntp server XXXX iburst`, enter `i` and start editing the file. NTP servers that are not currently needed can be hidden by adding a pound \(`#`\) at the beginning of the lines.
4.  Add a new line of NTP server information in the format of `server XXXX iburst`, and the XXXX is the custom NTP endpoint. For more information, see Internet and intranet NTP servers. After editing, press Esc and enter `:wq` to save and exit.
5.  Run `sudo service ntpd start` to enable the customized NTP service.
6.  Run `chkconfig ntpd on` to enable the NTP service.
7.  Run `ntpstat` to check whether the NTP service is enabled or not.

