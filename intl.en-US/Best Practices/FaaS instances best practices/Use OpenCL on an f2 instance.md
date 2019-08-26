# Use OpenCL on an f2 instance {#concept_62781_zh .concept}

This article introduces how to use Open Computing Language \(OpenCL\) to create an image file, and then download image to an FPGA chip.

**Note:** 

-   All the operations described in this article must be performed by one account in the same region.
-   We strongly recommend that you use an f2 instance as a RAM user. To avoid unwanted operations, you must authorize the RAM user to run required actions only. You must create a role for the RAM user and grant temporary permissions to the role to access the OSS buckets.

## Prerequisites {#section_nvh_dw3_dfb .section}

-   Create an F2 instance to ensure that the instance can access the public network, and the instance is in a security group that has added the rule to release access to the SSH \(22\) port.

    **Note:** The F2 instance can only use the FAAS F2 base mirror that mirrors the market. For more information, see [Create an F2 instance](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an f2 instance.md) .

-   Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
-   Sign up for OSS and [Create a bucket](../../../../reseller.en-US/Quick Start/Create a bucket.md). The bucket and F2 instances must belong to the same account and region.
-   To operate FPGA as a RAM user, do the following in advance:
    -    [Create a RAM](../../../../reseller.en-US/Quick Start/Create a RAM user.md) and [grant permissions](../../../../reseller.en-US/Quick Start/Attach policies to a RAM user.md).
    -    [Create a RAM](../../../../reseller.en-US/User Guide/Identities/Role.md) and [grant permissions](../../../../reseller.en-US/User Guide/Authorization/Authorization.md).
    -   Use the AccessKey to complete the authentication.

## Procedure { .section}

To create an image by using OpenCL on an f2 instance and download it to an FPGA chip, follow these steps.

## Step 1. Set up the environment { .section}

To set up the environment on an f2 instance, follow these steps.

1.   [Connect to an f2 instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md).
2.  Run `vim` to modify /root/xbinst\_oem/setup.sh: add a `#`at the beginning of line 5 , and comment out `unset XILINX_SDX`. Then save and exit.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465412093_en-US.png)

3.  Run the command to install Screen to keep the terminal session persistent.

    ```language-shell
    yum install screen -y
    
    ```

4.  Run the command to open a new screen.

    ```language-shell
    screen -S f2opencl
    
    ```

5.  Run the command to set up a secured environment to download a file.

    ```language-shell
    source /root/xbinst_oem/F2_env_setup.sh
    
    ```


## Step 2. Compile a binary file { .section}

To compile a binary file, follow these steps.

1.  Run the command to change the directory.

    ```language-shell
    cd /opt/Xilinx/SDx/2017.2/examples/vadd
    
    ```

2.  Run the `cat sdaccel.mk | grep "XDEVICE"` command to check the configuration of the `XDEVICE` parameter. Make sure it is set to `xilinx:aliyun-ku115-f2:4ddr-xpr:4.2`. If not, you must change this configuration.
3.  Modify the `common.mk` file using `vim`.

    ```language-shell
    vim ../common/common.mk
    
    ```

    Replace Line 63.

    ```language-shell
    CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} -o ${XCLBIN} ${KERNEL_DEFS} ${KERNEL_INCS}
    
    ```

    with

    ```language-shell
    CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} -o ${XCLBIN} ${KERNEL_DEFS} ${KERNEL_INCS} --xp param:compiler.acceleratorBinaryContent=dcp
    
    ```

    **Note:** You must submit a DCP file, not a bit file, to the compilation server. Therefore, you must add the parameter `--xp param:compiler.acceleratorBinaryContent=dcp` to enable Xilinx® OpenCL™ Compiler \(xocc\) to generate a DCP file.

4.  Run the command to compile the program.

    ```language-shell
    export XILINX_SDX=/opt/Xilinx/SDx/2017.2
    make -f sdaccel.mk xbin_hw
    
    ```

    If the following information is displayed, it means the compilation of the binary file is in progress. The process may take several hours. Please be patient.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465412094_en-US.png)


## Step 3. Check the packaging script { .section}

Run the command to check whether the packaging script exists or not.

```language-shell
file /root/xbinst_oem/sdaccel_package.sh

```

**Note:** A returned message containing `cannot open (No such file or directory)` means no packaging script exists. Then, download the script by running the following command.

```language-shell
wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/sdaccel_package.sh

```

## Step 4. Create an image { .section}

To create an image, follow these steps.

1.  Run the command to set up the OSS environment.

    ```language-shell
    # Replace hereIsMySecretId, hereIsMySecretKey, and hereIsMyBucket with your own AccessKeyID, AccessKeySecret, and OSS Bucket name
    faascmd config --id=hereIsMySecretId --key=hereIsMySecretKey 
    faascmd auth --bucket=hereIsMyBucket
    
    ```

2.  Run `ls` to get the file name.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465412095_en-US.png)

3.  Package binary files.

    ```language-shell
    /root/xbinst_oem/sdaccel_package.sh -xclbin=/opt/Xilinx/SDx/2017.2/examples/vadd/bin_vadd_hw.xclbin
    
    ```

    After the packaging is completed, you have a packaged file in the same directory, such as `17_10_28-021904_SDAccel_Kernel.tar.gz` in this example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465412096_en-US.png)

4.  Run the command to upload the packaged file to your own OSS bucket.

    ```language-shell
    # Replace the file name with the name of the packaged file
    faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
    
    ```

5.  Run the command to create an image.

    ```language-shell
    # Replace bit.tar.gz, hereIsFPGAImageName, and hereIsFPGAImageTag with the name of the packaged file, the image name, and the image tag
    faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=20171121
    
    ```

    The example returned result is displayed as follows. If `"State":"queued"`appears, this task is already in the queue, begin mirroring.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465412097_en-US.png)

    **Note:** It is time consuming to create a mirror. After a while, run the following command to view the mirror status.

    ```language-shell
    faascmd list_images
    
    ```

    In the returned result, if `"State":"success"` displays, it means the image is created successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465512098_en-US.png)

    Record the FpgaImageUUID.


## Step 5. Download the image { .section}

To download the image to an FPGA chip, follow these steps.

1.  Run the command to obtain the FpgaUUID.

    ```language-shell
    # Replace hereIsYourInstanceId with your f2 instance ID 
    faascmd list_instances --instanceId=hereIsYourInstanceId
    
    ```

    The following figure shows the predicted result.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465512099_en-US.png)

    **Note:** Record the FpgaUUID.

2.  Run the command to download the image.

    ```language-shell
    # Replace hereIsYourInstanceID with your f2 instance ID. Replace hereIsFpgaUUID with the recorded FpgaUUID. Replace hereIsImageUUID with the recorded FpgaImageUUID
    faascmd download_image  --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=20171121
    
    ```

    The example returned result is displayed as follows. The `"State":"committed"`means the image is downloaded successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465512100_en-US.png)

    **Note:** You can run the command to check whether the image is downloaded successfully or not.

    ```language-shell
    # Replace hereIsYourInstanceID with your f2 instance ID. Replace hereIsFpgaUUID with your recorded FpgaUUID
    faascmd fpga_status  --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID
    
    ```

    The example returned result is displayed as follows. If `"TaskStatus":"valid"`exists and the displayed FpgaImageUUID is your image FpgaImageUUID, the image is downloaded successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9829/153931465512102_en-US.png)


## Step 6. Run the Host program { .section}

Run the commands to run the Host program.

```language-shell
make -f sdaccel.mk host
unset XILINX_SDX
./vadd bin_vadd_hw.xclbin

```

If `Test Passed`is returned, the test is successful.

## Other common commands { .section}

In this section, some common commands for an FPGA instance are introduced.

|Task|Command|
|:---|:------|
|View the help document| `make -f ./sdaccel.mk help` |
|Run software simulation| `make -f ./sdaccel.mk run_cpu_em` |
|Run hardware simulation| `make -f ./sdaccel.mk run_hw_em` |
|Compile the host code only| `make -f ./sdaccel.mk host` |
|Compile and generate files for downloading| `make -f sdaccel.mk xbin_hw` |
|Clear a job directory| `make -f sdaccel.mk clean` |
|Force clear a job directory| `make -f sdaccel.mk cleanall` |

**Note:** 

-   During simulation of sdx2017.2, the device must be xilinx\_aliyun-ku115-f2\_4ddr-xpr\_4\_2.
-   During simulation, run the Xilinx simulation process. You do not need to set up the F2\_env\_setup environment.

