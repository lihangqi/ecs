# GUI of Cloud Migration tool \(Windows\) {#WindowsGui .reference}

The Cloud Migration tool of v1.2.9 and later supports a GUI for Windows. You can run the file go2aliyun\_gui.exe to access the GUI of Cloud Migration tool. The settings available for the Cloud Migration tool on the GUI are the same as those in the command line interface. If your version of the Cloud Migration tool is earlier than v1.2.9, we recommend that you [download](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip) the latest version of the tool.

## GUI overview {#section_bxm_gx1_kfb .section}

An overview of the Cloud Migration tool GUI for Windows, and different interface areas within the GUI, are shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22628/155902523545134_en-US.png)

1.  Menu bar: Includes the drop-down menu items **Config**, **Logs**, **Help**, and **Language**.

2.  Configurations \(user\_config.json\) editor: The text fields where a user enters configuration parameters for the source server. Such parameters include the AccessKey, the source server operating system, the size of the system disk, the ID of the Alibaba Cloud region to which the source server is being migrated, and the name of the generated ECS image. For more information, see [Edit user\_config.json](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).

3.  Disk list: A list of the system disk and data disks that are to be migrated. In this area, you can right-click to add disks to be migrated, and double click on a target disk to access its disk information editing page.

4.  Task progress and log: After you run the Cloud Migration tool, you can check the task progress in this area and perform troubleshooting tasks according to the logs.

5.  The **Config** menu, where you can click **Rsync** to set the bandwidth upper limit in KB/s for data transfer, click **Save User Config** to save the current page configuration for batch operation, or click **Clear Client Data** to initialize the client configuration file. For more information, see [Use the Cloud Migration tool](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).

6.  The **Log** menu, where you can click **Open Log File** to open the log file, or click **Open Log Dir** to open the directory where the log file is located.

7.  The **Help** menu, where you can find detailed help documentation or Cloud Migration tool version information.

8.  The **Language** menu, where you can change the languages settings of the GUI.

9.  Add data disks: The Cloud Migration tool automatically queries the available data disks attached to your source server and displays occupied disk space. The size of the target data disk must be greater than the space currently occupied by the data on the source data disk. For example, if the source data disk has a total of 500 GiB of space, but only 100 GiB is occupied by data, you must specify a disk size that is larger than 100 GiB.


## Procedure {#section_3lc_jgr_u5i .section}

1.  Open the GUI of the Cloud Migration tool for Windows.
2.  Configure the required server information.
3.  Click **Start**.
4.  Check the migration result.
    -   If the message `Goto Aliyun Finished!` appears in the task progress and log area, you can go to the image details page in the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to view the results.
    -   If the message `Goto Aliyun Not Finished!` appears, select **Logs** from the menu and view the corresponding logs to [troubleshoot the issue](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Troubleshooting.md#). Then, run the Cloud Migration tool again to resume the migration from where the task stopped.

