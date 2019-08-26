# Change the language settings of a Windows instance {#task_eyb_syt_hfb .task}

This topic uses an instance running the Windows Server 2016 public image as an example to describe how to download the German language pack from Windows Update and configure the language settings of an ECS instance by using the downloaded language pack. After you change the language settings for a target ECS instance, you can then use that instance to create a custom image based on the changed language settings.

Alibaba Cloud ECS provides only Chinese and English editions of Windows Server public images by default. However, you can use other language editions \(such as Arabic, German, Russian, or Japanese\) by downloading language packs from Windows Update to change the language settings of an ECS instance. Note that the information provided in this topic applies to instances running the Windows Server 2012 or later operating systems.

1.  Connect to the target Windows instance. For more information, see [Overview](../reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Open the PowerShell module.
3.  Run the following commands to temporarily disable Windows Server Update Services \(WSUS\). 

    ``` {#codeblock_f86_0jg_i2u}
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0
    Restart-Service -Name wuauserv
    ```

4.  Find the Control Panel, click **Clock, Language, and Region** \> **Language** \> **Add a language**.
5.  In the Add languages dialog box, select a language, for example, **Deutsch \(German\)** \> **Deutsch \(Deutschland\)**, and click **Add**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/156677835213242_en-US.png)

6.  Select the language, such as **Deutsch \(Deutschland\)**, and click **Move up** to change the language priority.
7.  Click **Options** next to the selected language to check online for language updates. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/156677835213243_en-US.png)

8.  Wait for about three minutes while the instance checks for updates. Once the update is available for download, click **Download and install language pack** and wait until the installation is complete. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/156677835213244_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/156677835213245_en-US.png)

9.  [Restart your instance](../reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console.
10. [Connect to the Windows instance](../reseller.en-US/Instances/Connect to instances/Overview.md#) again. The display language is now Deutsch \(German\).
11. Open the PowerShell ISE module and run the following commands to enable WSUS. 

    ``` {#codeblock_myn_81u_uat}
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1
    Restart-Service -Name wuauserv                    
    ```

12. Open **Windows Update**, check for security updates, and re-install all the security updates that are already done before the language settings.

Create multiple instances with the same language settings

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  [Create a custom image](../reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#) by using the Windows instance with the new display language.
3.  [Create a specified number of instances from the custom image](../reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22197/156677835213247_en-US.png)


