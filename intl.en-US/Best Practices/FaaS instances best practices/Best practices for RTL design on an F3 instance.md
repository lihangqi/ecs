# Best practices for RTL design on an F3 instance {#concept_71547_zh .concept}

This topic describes how to implement the Register Transfer Level \(RTL\) design on an F3 instance.

**Note:** 

-   All the operations described in this topic must be performed by one account in the same region.
-   We recommend that you use an F3 instance as a RAM user. To avoid unwanted operations, you must authorize the RAM user to perform required actions only. To use the FaaS service, you need to authorize the FaaS service account to access the OSS bucket that you specify. Therefore, you need to create the service role faasRole in the RAM console, and grant it the faasPolicy permission. If you want to encrypt IP addresses by using the Key Management Service \(KMS\), you must authorize the KMS-related permissions in faasPolicy.

## Prerequisites {#section_agy_vy3_dfb .section}

-   [Create an F3 instance](../../../../../intl.en-US/User Guide/Instances/Create an instance/Create an f3 instance.md) and add a security group rule to allow Internet access to SSH port 22 of the instance.
-   Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) to obtain the instance ID on the details page of the F3 instance.
-   [Create an OSS bucket](../../../../../intl.en-US/Quick Start/Create a bucket.md) in China East 2 \(Shanghai\) for the FaaS service.

    **Note:** The bucket will provide read and write access to the FaaS administrative account. We recommend that you do not store objects that are not related to FaaS.

-   To operate an F3 instance as a RAM user, do the following:
    -    [Create a RAM user](../../../../../intl.en-US/Quick Start/Create a RAM user.md) and [grant permissions](../../../../../intl.en-US/Quick Start/Authorize RAM users.md).
    -    [Create a RAM role](../../../../../intl.en-US//Identities/Roles.md) and [grant permissions](../../../../../intl.en-US//Authorization management/Authorization.md).
    -   Create the AccessKey ID and AccessKey Secret.

## Procedure { .section}

1.   [Connect to your F3 instance](../../../../../intl.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md).

    **Note:** It takes two or three hours to compile the project. We recommend that you use nohup or VNC to connect to the instance to avoid unexpected disconnection.

2.  Download and decompress the [RTL reference design](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/f3_hdk.tar.gz).
3.  Configure the F3 environment.

    -   If the driver is `xdma`, run the following command to configure the environment:

        ```language-bash
        source /root/xbinst_oem/F3_env_setup.sh xdma #Run this command each time you open a new terminal window
        
        ```

    -   If the driver is `xocl`, run the following command to configure the environment:

        ```language-bash
        source /root/xbinst_oem/F3_env_setup.sh xocl #Run this command each time you open a new terminal window
        ```

    **Note:** Configuring the environment mainly includes mounting the xdma or xocl driver, setting the vivado environment variable, checking the vivado license, detecting the aliyun-f3 sdaccel platform, configuring 2018.2 runtime, and detecting the faascmd version.

4.  Specify an OSS bucket.

    ```language-bash
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey #Replace hereIsYourSecretId and hereIsYourSecretKey with your RAM user AccessKey
    faascmd auth --bucket=hereIsYourBucket #Replace hereIsYourBucket with your OSS bucket name
    
    ```

5.  Run the following commands to compile the RTL project:

    ```language-bash
    cd <decompressed directory>/hw/ # Enter the decompressed hw directory
    sh compiling.sh
    
    ```

    **Note:** It takes two or three hours to compile the project.

6.  Upload the Netlist files and download the FPGA image. You can use the scripted process or the step-by-step process to finish this task.
    -   **Scripted process**: Applicable to the F3 instances with a single FPGA chip.

        1.  Run the following commands to upload the package and generate the image file:

            ```
            sh /root/xbinst_oem/tool/faas_upload_and_create_image.sh <bit.tar.gz - the package to upload>
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712110_en-US.png)

        2.  Download the image file.

            ```
            sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - the package filename> <0/1> # The last number <0/1> stands for the FPGA serial No. of the instance
            ```

            0 indicates the first FPGA of the F3 instance. For single-FPGA instances, the FPGA serial No. is always 0. For instances with multiple FPGAs, such as an instance with four FPGAs, the serial No. are 0, 1, 2 and 3.

            To download the same image to multiple FPGAs, add the serial No. to the end of the command. For example, to download the same image to four FPGAs, use the following commands:

            ```
            sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package filename> 0
            sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package filename> 1
            sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package filename> 2
            sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package filename> 3
            ```

    -   **Step-by-step process**: [Use the faascmd tool](intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Use faascmd.md#) to perform the operations.
        1.  Run the following commands to upload the package to your OSS bucket, and then upload gbs in your OSS bucket to the OSS bucket of the FaaS unit:

            ```language-bash
            faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
            faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=hereIsShellVersionOfFPGA
            
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712112_en-US.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712113_en-US.png)

        2.  Run the following command to check if the FPGA image is ready for downloading:

            ```
            faascmd list_images
            ```

            If the returned message shows `State`:`compiling`, the FPGA image is being compiled, and you still need to wait. If the returned message shows `State`:`success`, the FPGA image is ready for downloading. Find the FpgaImageUUID and note it down.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712115_en-US.png)

        3.  Run the following command. In the returned message, note down the FpgaUUID.

            ```
            faascmd list_instances --instanceId=hereIsYourInstanceId # Replace hereIsYourInstanceId with the f3 instance ID
            ```

        4.  Run the following command to download the FPGA image:

            ```
            
            faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=hereIsShellVersionOfFpga
            # Replace hereIsYourInstanceId with the f3 instance ID, hereIsFpgaUUID with the obtained FpgaUUID, and hereIsImageUUID with the obtained FpgaImageUUID
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712116_en-US.png)

        5.  Run the following command to check whether the image has been successfully downloaded:

            ```
            faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceId # Replace hereIsFpgaUUID with the obtained FpgaUUID, and hereIsYourInstanceId with the f3 instance ID
            ```

            The following is an example of the returned message. If the FpgaImageUUID in the message is identical to the FpgaImageUUID you note down, and the message shows `"TaskStatus":"valid"`, the image has been successfully downloaded.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154771164712117_en-US.png)


## FAQ { .section}

**How do I view the details of errors that occur during image upload?**

If your project reports errors during image upload, such as compilation errors, you can view the error details in two ways:

-   Check faas\_compiling.log. When the upload script faas\_upload\_and\_create\_image.sh is used, faas\_compiling.log is automatically downloaded and printed onto the terminal if compilation fails.
-   Run the command to view the log file: `sh /root/xbinst_oem/tool/faas_checklog.sh <bit.tar.gz - package uploaded previously>` 

**How do I reload the image?**

To reload the image, follow these steps:

1.  Uninstall the driver.
    -   If you have installed the `xdma` driver, run the command `sudo rmmod xdma` in the instance to uninstall it.
    -   If you have installed the `xocl`driver, run the command `sudo rmmod xocl` in the instance to uninstall it.
2.  Download the image in either of the two ways :
    -   Use the script.

        ```
        sh faas_download_image.sh bit.tar.gz <0/1> #The last number stands for the FPGA serial No. of the instance
        ```

    -   Use faascmd.

        ```
        faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=hereIsShellVersionOfFpga
        ```

3.  Install the driver.
    -   To install the `xdma` driver, run the following command:

        ```
        sudo depmod
        sudo modprobe xdma
        ```

    -   To install the `xocl` driver, run the following command:

        ```
        sudo depmod 
        sudo modprobe xocl
        ```


