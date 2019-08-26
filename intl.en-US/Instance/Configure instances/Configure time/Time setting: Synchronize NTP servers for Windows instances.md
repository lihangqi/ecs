# Time setting: Synchronize NTP servers for Windows instances {#TimeCalibrationWindows .concept}

Network Time Protocol \(NTP\) is a networking protocol for clock synchronization between computer systems over networks. For highly time-sensitive applications \(such as those in the communication industry\), clock variation between different computers may lead to serious data inconsistencies. You can use the NTP service to synchronize clocks of all servers within the network. The current default time zone for Alibaba Cloud ECS instances across all regions is CST \(China Standard Time\).

This article describes how use the NTP service to synchronize the clock of a Windows ECS instance running Windows Server 2008 R2 Enterprise Edition x64.

Windows Time service is enabled by default on Windows Server. You must enable the NTP service in the instance to make sure that the NTP service can normally synchronize time after successful NTP service configuration. To check and enable the NTP service, follow these steps:

1.   [Connect to a Windows instance](../../../../../reseller.en-US/Instance/ECS instance life cycle/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#). Select **Start** \> **All Programs** \> **Accessories** \> **Run** to open the Run dialog box, and run `services.msc`.
2.  In the Services window, double click the **Windows Time** service.
3.  In the Windows Time Properties \(Local Computer\) dialog box, follow these steps:

    1.  Set **Startup type** to **Automatic**.
    2.  Check if the **Service status** is **Started**. If not, click **Start**.
    After completing the settings, click **Apply**, and then click **OK**.

    ![Start Windows Time service.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9806/155102411713081_en-US.png)


## Modify the default NTP server address { .section}

time.windows.com is used as the default NTP server in Windows Server, but synchronization errors may frequently occur due to network issues. When using a Windows instance, you can replace the default NTP server with the intranet NTP server provided by Alibaba Cloud. For more information, see [Internet and intranet NTP servers](reseller.en-US/Instance/Configure instances/Configure time/Time setting: NTP servers and other public services.md#). To modify the default NTP server address, follow these steps:

1.   [Connect to a Windows instance](../../../../../reseller.en-US/Instance/ECS instance life cycle/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  In the notification area of the task bar, click Date and Time, and then click **Change date and time settings**.
3.  In the Date and Time dialog box, click the **Internet Time** tab, and then click **Change settings**.
4.  In the Internet Time Settings dialog box, select **Synchronize with an Internet time server**, type an Alibaba Cloud intranet NTP server address \(for detailed list, see [Internet and intranet NTP servers](reseller.en-US/Instance/Configure instances/Configure time/Time setting: NTP servers and other public services.md#)\), and then click **Update now**.

You are prompted if the synchronization is successful.

## Modify NTP synchronization interval { .section}

The default NTP synchronization interval is 5 minutes. To modify the NTP synchronization interval, follow these steps:

1.  [Connect to a Windows instance](../../../../../reseller.en-US/Instance/ECS instance life cycle/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Select **Start** \> **All Programs** \> **Accessories** \> **Run** to open the Run dialog box, and run `regedit`.
3.  On the left-side navigation pane of the Registry Editor, find HKEY\_LOCAL\_MACHINE/SYSTEM/CurrentControlSet/services/W32Time/TimeProviders/NtpClient, and then double click SpecialPollInterval.
4.  In the Edit DWORD \(32-bit\) Value dialog box, select **Decimal** as the **Base**, and then type the **Value data** as needed. The number you typed is the synchronization interval you need. Unit: seconds.

