# Use RTL compiler on an f3 instance {#concept_71547_zh .concept}

This article describes how to use the Register Transfer Level \(RTL\) compiler on an f3 instance.

**Note:** 

-   All the operations described in this article must be performed by one account in the same region.
-   We recommend that you use an f3 instance as a RAM user. To avoid unwanted operations, you must authorize the RAM user to perform required actions only. You must create a role for the RAM user and grant the role temporary permissions to access the OSS buckets. If you want to encrypt the IP address, authorize the RAM user to use Key Management Service \(KMS\). If you want the RAM user to check permissions, authorize the RAM user to view the resources of an account.

## Prerequisites {#section_agy_vy3_dfb .section}

-   [Create an f3 instance](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an f3 instance.md) and add a security group rule to allow the Internet access to SSH Port 22 of the instance.
-   Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to obtain the instance ID on the details page of the f3 instance.
-   [Create an OSS bucket](../../../../reseller.en-US/Quick Start/Create a bucket.md) in China East 2 \(Shanghai\) for the FaaS service.

    **Note:** The bucket will provide read and write access to the FaaS administrative account. We recommend that you do not store objects that are not related to FaaS.

-   To operate an f3 instance as a RAM user, do the following:
    -    [Create a RAM user](../../../../reseller.en-US/Quick Start/Create a RAM user.md) and [grant permissions](../../../../reseller.en-US/Quick Start/Attach policies to a RAM user.md).
    -    [Create a RAM user](../../../../reseller.en-US/User Guide/Identities/Role.md) and [grant permissions](../../../../reseller.en-US/User Guide/Authorization/Authorization.md).
    -   Create an AccessKey.

## Procedure { .section}

1.   [Connect to your f3 instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md).

    **Note:** It takes two or three hours to compile the project. We recommend that you use nohup or VNC to connect the instance so as to avoid unexpected disconnection.

2.  Download the [RTL reference design](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/f30002/f30002.tar.gz).
3.  Decompress the file.
4.  Configure the f3 environment.

    ```language-bash
    source /root/xbinst_oem/F3_env_setup.sh xdma
    
    ```

    **Note:** Run this command each time you open a new terminal window.

5.  Specify an OSS bucket.

    ```language-bash
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey # Replace hereIsYourSecretId and hereIsYourSecretKey with your RAM AK information
    faascmd auth --bucket=hereIsYourBucket # Replace hereIsYourBucket with the name of your OSS Bucket
    
    ```

6.  Run the following commands to compile the RTL project.

    ```language-bash
    cd <decompressed directory>/hw/ # Enter the decompressed hw directory
    sh compiling.sh
    
    ```

    **Note:** It takes two or three hours to compile the project.

7.  Upload the Netlist files and download the FPGA image. You can use the scripted process or the step-by-step process to finish this task.
    -   Scripted process: Applicable to the f3 instances with a single FPGA chip.

        1.  Run the following commands to upload the package and generate the image file.

            ```
            sh  /root/xbinst_oem/tool/faas_upload_and_create_image.sh <bit.tar.gz - the package to upload>
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401712110_en-US.png)

        2.  Download the image file.

            ```
            
            sh  /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - the package filename> 0 # The last number stands for the FPGA serial No. of the instance
            ```

            0 indicates the first FPGA of the f3 instance. For single-FPGA instances, the FPGA serial No. is always 0. For instances with multiple FPGAs, such as an instance with four FPGAs, the serial No. are 0, 1, 2 and 3.

            To download the same image to multiple FPGAs, add the serial No. to the end:

            ```
            sh faas_download_image.sh bit.tar.gz 0 1 2
            
            ```

    -   Step-by-step process:
        1.  Run the following commands to upload the package to your OSS bucket, and then upload gbs in your OSS bucket to the OSS bucket of the FaaS unit.

            ```language-bash
            faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
            faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=f30001
            
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401712112_en-US.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401712113_en-US.png)

        2.  Run the following command to check if the FPGA image is ready for downloading.

            ```
            faascmd list_images
            ```

            If the returned message shows `"State":"success"`, the FPGA image is ready for downloading. Find the FpgaImageUUID and note it down.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401812115_en-US.png)

        3.  Run the following command and then note down the FpgaUUID in the returned message.

            ```
            faascmd list_instances --instanceId=hereIsYourInstanceId # Replace hereIsYourInstanceId with your f3 instance ID
            ```

        4.  Run the following command to download the FPGA image.

            ```
            
            faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=f30001
            # Replace hereIsYourInstanceId with f3 instance ID, hereIsFpgaUUID with the obtained FpgaUUID, and hereIsImageUUID with the obtained FpgaImageUUID
            ```

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401812116_en-US.png)

        5.  Run the following command to check whether the image has been successfully downloaded.

            ```
            faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceId # Replace hereIsFpgaUUID with the obtained FpgaUUID, and hereIsYourInstanceId with f3 instance ID.
            ```

            Below is an example of the returned message. If the FPGA image UUID in the message is identical with the FPGA image UUID you note down, and the message shows `"TaskStatus":"valid"`, the image has been successfully downloaded.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/153924401812117_en-US.png)


## FAQ { .section}

**How to view the details of errors that occur during image uploading?**

If your project reports errors during image uploading \(such as compliation errors\), you can view the error details in either of the two ways:

-   Check faas\_compiling.log. When the upload script faas\_upload\_and\_create\_image.sh is used, faas\_compiling.log is automatically downloaded and printed onto the terminal if compliation fails.
-   Run the command to view the log file: `sh /root/xbinst_oem/tool/faas_checklog.sh <bit.tar.gz - package uploaded previously>` 

**How to reload the image?**

To reload the image, follow these steps:

1.  Run the commands on the instance to uninstall the driver.

    ```
    sudo rmmod xdma
    sudo rmmod xocl
    
    ```

2.  Download the image in either of the two ways:
    -   Use the script. The last number stands for the FPGA serial No. of the instance: `sh faas_download_image.sh bit.tar.gz 0` 
    -   Use faascmd: `faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=f30001` 
3.  Install the driver.

    ```
    sudo depmod
    sudo modprobe xdma
    
    ```


