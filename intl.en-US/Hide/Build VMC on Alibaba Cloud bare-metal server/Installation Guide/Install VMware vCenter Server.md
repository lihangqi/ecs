# Install VMware vCenter Server {#task_abz_v5s_ggb .task}

VMware vCenter Server allows you to manage multiple hosts from either a physical or virtual Windows machine and use the advanced features. This topic describes how to install VMware vCenter Server.

1.  Remotely connect to a Windows instance.
2.  When you connect to the Windows instance, an identity authentication error may occur due to Windows patch updates. For more information, see [How to solve authentication errors caused by CredSSP encryption oracle remediation when connecting to Windows instances](https://www.alibabacloud.com/help/faq-detail/71931.htm).
3.  Disable security enhancement configuration before the installation. Otherwise, a confirmation dialog box will be displayed repeatedly and interrupt the installation when you access an URL.

    **Note:** For more information, see [Internet Explorer Enhanced Security Configuration changes the browsing experience](https://support.microsoft.com/en-us/help/815141/internet-explorer-enhanced-security-configuration-changes-the-browsing)

4.  Install the Adobe Flash Player plugin.
5.  Purchase and download VMware vCenter Server.

1.   Double-click the VMware vCenter Server installation file, select **I accept the terms of the license agreement**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618435724_en-US.png)

 
2.   Select **Embedded Deployment**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618435726_en-US.png)

 
3.   Set the username and password, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535727_en-US.png)

 
4.  In the **System Name** text box, enter the IP address of the Windows instance.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535728_en-US.png) 
5.   Select **Use Windows Local System Account**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535729_en-US.png)

 
6.   Select **Use an embedded database \(VMware Postgres\)**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535730_en-US.png)

 
7.   In the **Configure Ports** dialog box, set the ports, as shown in the following figure, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535731_en-US.png)

 
8.   Set the **Destination Directory**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535732_en-US.png)

 
9.   Select **Join the VMware Customer Experience Improvement Program**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535733_en-US.png)

 
10.  In the **Ready to install** window, confirm your settings, and then click **Install**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535734_en-US.png)

 
11.  Click **Launch vSphere Web Client**, or enter the IP address of the Windows instance to open the vSphere Web Client logon page.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535735_en-US.png)

 
12.  Enter the username and password that you set for VMware vCenter Server, and then click **Login** to log on to VMware vCenter Server through vSphere Web Client.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83717/154705618535963_en-US.png)

 

