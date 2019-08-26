# Configure language settings for multiple instances {#task_eyb_syt_hfb .task}

This tutorial takes German as an example. The German language package is downloaded from Windows Update. A custom image is then created that uses the German language and German keyboard settings. You can then use the custom image to create as many instances as required.

Currently, Alibaba Cloud ECS provides only Chinese and English editions of Windows Server images. If you want to use other language editions, such as Arabic, German, or Russian, you can follow this tutorial to set up and deploy your ECS instances.

1.  [Connect to the Windows instance](../reseller.en-US/User Guide/Connect to instances/Overview.md#). 
2.  Open the PowerShell module. 
3.  Run the following commands to disable WSUS temporarily. 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0
    Restart-Service -Name wuauserv
    ```

4.  Find the Control Panel, click **Clock, Language, and Region** \> **Language** \> **Add a language**. 
5.  In the Add languages dialog box, select a language, for example, **Deutsch \(German\)** \> **Deutsch \(Deutschland\)**, and click **Add**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756913242_en-US.png)

6.  Select the language, such as **Deutsch \(Deutschland\)**, and click **Move up** to change the language priority. 
7.  Click **Options** next to the selected language to check online for language updates. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756913243_en-US.png)

8.  Wait for about 3 minutes while the instance checks for updates. Once the update is available for download, click **Download and install language pack** and wait until the installation is complete. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950756913244_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/153950757013245_en-US.png)

9.  [Restart your instance](../reseller.en-US/User Guide/Instances/Restart an instance.md#), and the display language is changed on next logon. 
10. [Connect to the Windows instance](../reseller.en-US/User Guide/Connect to instances/Overview.md#) again. The display language is now Deutsch \(German\). 
11. Open the PowerShell ISE module and run the following commands to turn WSUS back on. 

    ```
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1
    Restart-Service -Name wuauserv
    
    ```

12. Open **Windows Update**, check for security updates, and re-install all the security updates that are already done before the language settings. 

Create multiple instances with the same language settings

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  and [create a custom image](../reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#) by using the Windows instance with the new display language.
3.  [Create a specified number of instances from the custom image](../reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

