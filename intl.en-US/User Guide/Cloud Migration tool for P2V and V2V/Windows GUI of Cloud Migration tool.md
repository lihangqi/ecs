# Windows GUI of Cloud Migration tool {#WindowsGui .reference}

Cloud Migration tool version 1.2.9 and later supports a GUI for Windows OS. You can run the file go2aliyun\_gui.exe to access the GUI. If you are using an earlier version of the Cloud Migration tool, you can download the [compressed Cloud Migration tool](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip)for a better experience. The settings available for the Cloud Migration tool on the GUI are identical to those in the command line interface.

## Display introduction {#section_bxm_gx1_kfb .section}

When using the Cloud Migration tool on Windows, you can use either the GUI or the command line interface. As shown in the figure below:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22628/153949590413345_en-US.png)

## Display description {#section_vjd_yx1_kfb .section}

1.  Menu bar, consisting of **Config**, **Logs**, and **Help**.

2.  User-defined configurations \(user\_config.json\) editor. It is used to configure the source server. Configurations include your AccessKey information, source server operating system, system disk size, and the Alibaba Cloud region ID that the source service is being moved to. It is used to create the custom image configuration and information after the ECS image has been created. For more information, see *Using the Cloud Migration tool* to edit [user\_config.json](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

3.  List of system disk and data disks that are about to migrated. In this area, you can right-click to add disks to be migrated, and double click to access the disk information edit page.

4.  Task progress and log area. After running the cloud migration tool, you can track the task progress in this area, and troubleshoot any issues that arise in accordance with the interface prompts.

5.  Menu where you can click **Rsync** to set the upper bandwidth limit in KB/s for the transfer, click **Save User Config** to save the current page configuration for batch operation, or click **Clear Client Data** to initialize the client configuration file. For more information, see [Using the Cloud Migration tool](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

6.  Menu where you can click **Open Log File**to open the log file, or click **Open Log Dir** to open the path where the log file is located.

7.  Menu where you can check help documentation or Cloud Migration tool version information.

8.  You can add a data disk here. The Cloud Migration tool automatically queries the data disk of your server and displays occupied disk space. The size of the data disk must be greater than the space currently used on the source server data disk. For example, if the source server has 500 GiB of space and is using 100 GiB, you must specify a size larger than 100 GiB. The value must be greater than the occupied space of the data disk on the source server. For example, if the original data disk size is 500 GiB and the occupied space is 100 GiB, set this value to be greater than 100 GiB.


After you have configured the server information in the GUI, you can click **Start** to begin the cloud migration. After solving any problems, run the Cloud Migration tool to restore the migration. The cloud migration resumes from where it was stopped. If the prompt message `Goto Aliyun Finished!` appears in the task progress and log area, you can go to the image details page in the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to view the results. If the prompt message `Goto Aliyun Not Finished!` appears, you can select **Logs** from the menu and look through the logs to [troubleshoot the issue](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Troubleshooting.md#). After fixing any problems, run Cloud Migration Tool again to resume volume shrinking. The tool continues the most recent migration execution and does not start over.

