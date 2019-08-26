# Update a Red Hat VirtIO SICI driver in Windows {#concept_v4p_2xs_dhb .concept}

This topic describes how to update a Red Hat VirtIO SICI driver running in a Windows instance in Alibaba Cloud. In Alibaba Cloud, you can resize your disk online without the need to restart the instance. However, if your instance is created before March 30, 2019, you need to check whether you need to update the RedHat VirtIO SICI driver according to the information in this topic.

## Limits {#section_vhd_23y_dhb .section}

-   The RedHat VirtIO SICI driver is only supported by instances running Windows Server 2008 or later versions.
-   If you have multiple data disks in your Windows instance, a driver update may take up to two minutes to be completed.

## Download the driver {#section_vsy_j3y_dhb .section}

Download and decompress the [instdrv driver package](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/25367/APP_zh/1553675201254/instdrv.zip). The following table describes the files and folders that are extracted from the decompressed package.

|File/folder name|Description|
|:---------------|:----------|
|win7|Windows 7|
|Wlh|Windows 2008|
|Win8|Windows 2012|
|win10|Windows 2016/1709/10|
|amd64|64-bit|
|x86|32-bit|
|instdrv.exe|Checks whether your instance supports online disk resizing programs.|

## Check the driver version {#section_mhl_nhy_dhb .section}

**Method 1: Run the instdrv.exe file** 

1.  [Connect to the target Windows instance](../../../../../intl.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Open the Command Prompt \(cmd\).
3.  Enter the directory where instdrv.exe is located. In this example, the directory is `cd C:\\User|lizr\\Desktop\\instdrv\\`.
4.  Optional. Run instdrv.exe to view the user guide of the tool. Run the `instdrv.exe -v` command to view the tool version.
5.  Run the `instdrv.exe -c` command, and check whether the operating system supports online disk resizing.

    **Note:** If the response message indicates that support for online disk resizing is available, you can directly [resize a disk online](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#). Otherwise, you need to [update the RedHat VirtIO SICI driver](#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155505897941813_en-US.png)


**Method 2: Check the driver version manually** 

1.  Connect to the target Windows instance.
2.  Enter the system directory C:\\Windows\\System32\\drivers.
3.  Right-click the viostor.sys file, and then select **Properties**. Choose **Details** \> **File Version**.

    **Note:** If the version of the viostor.sys file is 58011 or later, you can directly [resize a disk online](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#). If the file version is earlier than 58011, you need to [update the RedHat VirtIO SICI driver](#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155505898041818_en-US.png)


## Update the RedHat VirtIO SICI driver {#section_pvf_cr1_qgb .section}

**Method 1: Run the pnputil command** 

1.  Open the Command Prompt \(cmd\).
2.  Enter the directory where the viostor.inf file is located. In this example, the directory is `cd C:\\Users\\Administrator\\Desktop\\amd`.
3.  Decompress the target .inf file to the specified <directory\>.
4.  Run the `pnputil –i –a <directory\>` command to add the driver package.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155505898041303_en-US.png)

5.  Log on to the ECS console and restart the instance, or call the API [RebootInstance](../../../../../intl.en-US/API Reference/Instances/RebootInstance.md#) to restart the instance to validate the updated driver.

**Method 2: Update the driver manually** 

1.  Open the Device Manager window.
2.  Right-click **Red Hat Vir** under **Disk drivers**, and then select **Update Driver Software**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/146927/155505898141810_en-US.png)

3.  Select **Browse my computer for driver software**.
4.  Select **Let me pick from a list of device drivers on my computer**.
5.  Click **Hard Disk**.
6.  Select the driver file viostor from the target folder, and then update the driver by following the wizard.
7.  Log on to the ECS console and restart the instance, or call the API [RebootInstance](../../../../../intl.en-US/API Reference/Instances/RebootInstance.md#) to restart the instance to validate the updated driver.

## What to do next {#section_kj1_ssy_dhb .section}

[Resize a disk online](intl.en-US/Block storage/Block storage/Resize cloud disks/Resize a cloud disk online/Resize a cloud disk online.md#).

