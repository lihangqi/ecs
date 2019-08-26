# Modify the default remote access port {#concept_51644_zh .concept}

This topic describes how to modify the remote port of a Windows or Linux instance.

## Modify the default remote port of a Windows instance {#section_dss_hyq_gfb .section}

This section describes how to modify the remote port of a Windows instance running Windows Server 2008.

1.   [Connect to the Windows instance](../reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  Run regedit.exe to open Registry Editor.
3.  On the left-side navigation pane of the Registry Editor, find HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp\\PortNumber.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612757_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612758_en-US.png)

4.  In the dialog box, select **Decimal as Base**, and then type a number in the **Value data** field as the new remote port number, which is 3399 in this example. Click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612759_en-US.png)

5.  \(Optional\) If you have enabled firewall, open the new port on the firewall.
6.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs), find the instance, and then select **More** \> **Restart**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612760_en-US.png)

7.  After the instance is restarted, click the **Manage** of the instance to enter the Instance Details page. Click **Security Groups**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612761_en-US.png)

8.  On the Security Groups page, click **Add Rules**.
9.  On the Security Group Rules page, click **Add Security Group Rule**. Add a new security group rule to allow access to the new remote port. For more information about adding security group rules, see [Add security group rules](../reseller.en-US/User Guide/Security groups/Add security group rules.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612762_en-US.png)

10. Connect to the instance by accessing the IP address ending with the new port number. For example, 192.168.1.2:3399 in this example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916712763_en-US.png)

    **Note:** Only the default port 3389 can be used for access by Mac remote desktop users.


## Modify the default remote port of a Linux instance {#section_ds5_3yq_gfb .section}

This section describes how to modify the remote port of a Linux instance running CentOS 6.8.

**Note:** Do not modify the 22 port directly, first add the new default remote port. Set two ports first and delete one after the test succeeds. It ensures that you can use port 22 to debug any problems if you cannot connect the instance through the new port.

1.  [Connect to the Linux instance](../reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  Run vim /etc/ssh/sshd\_config.
3.  Press the "I" key on the keyboard to enter the Edit mode. Add new remote service port \(for example, Port 1022\). Enter Port 1022 under Port 22.
4.  Press "ESC" and enter : wq to exit the editing.
5.  Restart the instance by executing the following command. You can then log on to the Linux instance through 22 port and 1022 port.

    ```
    /etc/init.d/ssh restart
    ```

6.  \(Optional\) Configure the firewall. When you use Linux versions earlier than CentOS 7 and has enabled firewall iptables, note that iptables do not intercept access by default. If you configured iptables rules, run iptables -A INPUT -p tcp --dport 1022 -j ACCEPT to configure the firewall. Then perform service iptables restart to restart the firewall.

    **Note:** Firewalld is installed by default on CentOS 7 and later versions. If you have enabled firewalld.service, open TCP port 1022 by running the command firewall-cmd --add-port=1022/tcp --permanent. If success is returned, TCP port 1022 is opened.

7.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs), find the instance, and then select **Manage**.
8.  Enter the Instance Details page. Click **Security Groups**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916612761_en-US.png)

9.  On the Security Groups page, click **Add Rules**.
10. On the Security Group Rules page, click **Add Security Group Rule**. Add a new security group rule to allow access to the new remote port. For more information about adding security group rules, see [Add security group rules](../reseller.en-US/User Guide/Security groups/Add security group rules.md#).
11. Use the SSH tool to connect to the new port to test if the default remote port is modified successfully. Enter the new port number in **Port** when logging on to the instance, which is 1022 in this example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9797/154684916712765_en-US.png)

12. Once you successfully connect the instance through port 1022, run vim /etc/ssh/sshd\_config again to remove port 22.
13. Run /etc/init.d/sshd to restart the instance and the default remote port is successfully modified. Connect to the instance by accessing the IP address ending with the new port number.

