# Best practices for OpenCL on an f3 instance {#concept_d3c_4sl_2fb .concept}

This topic describes how to use Open Computing Language \(OpenCL\) to create an image, and then download it to an FPGA chip in an f3 instance.

**Note:** 

-   All the operations described in this topic must be performed by one account in the same region.
-   We recommend that you use an f3 instance as a RAM user. You must create a role for the RAM user and grant the role temporary permissions to access the specified OSS buckets.

## Prerequisites {#section_j5c_ctl_2fb .section}

-   [Create an f3 instance](../../../../../intl.en-US/User Guide/Instances/Create an instance/Create an f3 instance.md).

    **Note:** 

    -   Only the image we share with you can be used on an f3 instance.
    -   Select Assign public IP when creating an instance, so that the instance can access the Internet.
    -   The security group of the f3 instance has added the rule for allowing access to the SSH port 22.
-   Log on to the ECS console and obtain the instance ID of your f3 instance.
-   Create an OSS bucket in the same region as your f3 instance by using the same account. For more information, see Sign up for OSS and [Create a bucket](../../../../../intl.en-US/Quick Start/Create a bucket.md).
-   To operate FPGA as a RAM user, do the following in advance:
    -    [Create a RAM user](../../../../../intl.en-US/Quick Start/Create a RAM user.md) and [grant permissions](../../../../../intl.en-US/Quick Start/Authorize RAM users.md).
    -    [Create a RAM role](../../../../../intl.en-US//Identities/Roles.md) and [grant permissions](../../../../../intl.en-US//Authorization management/Authorization.md).
    -   Obtain the AccessKey ID and AccessKey Secret.

## Procedure {#section_eyg_ltl_2fb .section}

To create an image and download it to an FPGA chip on an f3 instance by using OpenCL, follow these steps.

## Step 1. Set up the environment {#section_wvk_ntl_2fb .section}

To set up the environment, follow these steps:

1.  [Connect to the f3 instance](../../../../../intl.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md).

    **Note:** The subsequent compilation process may take a few hours. We recommend that you log on through screen or nohub, so as to avoid forced logout due to an SSH timeout.

2.  Run the command to install Screen.

    ```
    yum install screen -y
    ```

3.  Run the command to enter Screen.

    ```
    screen -S f3opencl
    ```

4.  Run the command to set up the environment.

    ```
    source /root/xbinst_oem/f3_env_setup.sh xocl  # Run the command each time you open a new terminal window
    ```

    **Note:** 

    -   Configuring the environment involves installing the xocl driver, setting the vivado environment variable, checking the vivado license, detecting the aliyun-f3 sdaccel platform, configuring 2018.2 runtime, and detecting the faascmd version.
    -   If you want to run an emulation of sdaccel, do not run the above command to configure the environment. Instead, you only need to configure the environment variable for vivado separately.
    -   We recommend that you use Makefile for emulation.

## Step 2. Compile a binary file {#section_qcn_vtl_2fb .section}

-   **Example 1: vadd**

    To compile the vadd binary file, follow these steps:

    1.  Copy the `example` directory.

        ```
        cp -rf /opt/Xilinx/SDx/2018.2/examples . /
        ```

    2.  Enter the `vadd` directory.

        ```
        cd examples/vadd/
        ```

    3.  Run the command `cat sdaccel.mk | grep "XDEVICE="` to view the value of `XDEVICE`. Make sure its configuration is `XDEVICE=xilinx_aliyun-f3_dynamic_5_0`.
    4.  Follow these steps to modify the `common.mk` file.
        1.  Run the `vim ../common/common.mk` command to open the file.
        2.  At the end of the code line 61, add the compilation parameter `--xp param:compiler.acceleratorBinaryContent=dcp` \(the parameter may be in the line 60-62, depending on your file\). The modified code is:

            ```
            CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} -o ${XCLBIN} ${KERNEL_DEFS} ${KERNEL_INCS} --xp param:compiler.acceleratorBinaryContent=dcp
            ```

            **Note:** Given that you must submit a DCP file to the compilation server, you need to add the parameter `--xp param:compiler.acceleratorBinaryContent=dcp`, so that Xilinx® OpenCL™ Compiler \(xocc\) generates a DCP file \(instead of a bit file\) after the placement and routing is complete.

    5.  Run the command to compile the program.

        ```
        make -f sdaccel.mk xbin_hw
        ```

        If the following information is displayed, the compilation of the binary file has started. This process may take several hours.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21515/154777961512150_en-US.png)

-   **Example 2: kernel\_global\_bandwidth**

    Follow these steps to compile the kernel\_global\_bandwidth binary file:

    1.  Clone `xilinx 2018.2 example`.

        ```
        git clone https://github.com/Xilinx/SDAccel_Examples.git
        cd SDAccel_Examples/
        git checkout 2018.2
        ```

        **Note:** The git branch must be the 2018.2 version.

    2.  Run the `cd getting_started/kernel_to_gmem/kernel_global_bandwidth/` command to enter the directory.
    3.  Follow these steps to modify the `Makefile` file.
        1.  Run the `vim Makefile` command to open the file.
        2.  Set `DEVICES=xilinx_aliyun-f3_dynamic_5_0`.
        3.  In the code line 33, add the compilation parameter `--xp param:compiler.acceleratorBinaryContent=dcp`. The modified code is:

            ```
            CLFLAGS +=--xp "param:compiler.acceleratorBinaryContent=dcp" --xp "param:compiler.preserveHlsOutput=1" --xp "param:compiler.generateExtraRunData=true" --max_memory_ports bandwidth -DNDDR_BANKS=$(ddr_banks)
            ```

    4.  Run the command to compile the program.

        ```
        make TARGET=hw
        ```

        If the following information is displayed, the compilation of the binary file has started. This process may take several hours.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21515/154777961536971_en-US.png)


## Step 3. Check the packaging script {#section_rjl_d5l_2fb .section}

Run the command to check whether the packaging script exists or not.

```
file /root/xbinst_oem/sdaccel_package.sh
```

If the returned message contains `cannot open (No such file or directory)`, the file does not exist. You need to download the script by running the following command.

```
wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/sdaccel_package.sh
```

## Step 4. Create an image {#section_h1l_g5l_2fb .section}

To create an image, follow these steps:

1.  Run the command to set up the OSS environment.

    ```
    faascmd config --id=hereIsMySecretId --key=hereIsMySecretKey #Replace hereIsMySecretId, hereIsMySecretKey with your AccessKeyID, AccessKeySecret
    faascmd auth --bucket=hereIsMyBucket # Replace hereIsMyBucket with your bucket name
    ```

2.  Run the `ls` command to obtain the file suffixed by `.xclbin`.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21515/154777961512152_en-US.png)

3.  Run the command to package the binary file.

    ```
    /root/xbinst_oem/sdaccel_package.sh -xclbin=/opt/Xilinx/SDx/2017.4.op/examples/vadd/bin_vadd_hw.xclbin
    ```

    After the packaging is completed, you can find a package file in the same directory, as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21515/154777961612154_en-US.png)


## Step 5. Download the image {#section_ft5_k5l_2fb .section}

You can use a scripted process or step-by-step process to upload the package file and download the FPGA image.

-   **Scripted process**: Only applicable to f3 instances with one FPGA chip.

    1.  Run the following commands to upload the package and generate the image file.

        ```
        sh /root/xbinst_oem/tool/faas_upload_and_create_image.sh <bit.tar.gz - the package to upload>
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612110_en-US.png)

    2.  Download the image file.

        ```
        sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package name> <0/1> # The last number <0/1> stands for the FPGA serial No. in the instance
        ```

        0 indicates the first FPGA of the f3 instance. For single-FPGA instances, the FPGA serial No. is always 0. For instances with multiple FPGAs, such as an instance with four FPGAs, the serial No. are 0, 1, 2 and 3.

        To download the same image to multiple FPGAs, add the serial No. to the end. For example, run the command to download the same image to four FPGA chips:

        ```
        sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package name> 0
        sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package name> 1
        sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package name> 2
        sh /root/xbinst_oem/tool/faas_download_image.sh <bit.tar.gz - package name> 3
        ```

-   **Step-by-step process**: [Use the faascmd tool](intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Use faascmd.md#) to perform operations.
    1.  Run the command to upload the package to your OSS bucket. Then, upload gbs in your OSS bucket to the OSS bucket in the FaaS administrative unit.

        ```language-bash
        faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
        faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=hereIsFPGAImageName --tags=hereIsFPGAImageTag --encrypted=false --shell=hereIsShellVersionOfFPGA
        
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612112_en-US.png)

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612113_en-US.png)

    2.  Run the command to view if the FPGA image is downloadable.

        ```
        faascmd list_images
        ```

        If the returned message shows `State`:`compiling`, the FPGA image is being compiled. If the returned message shows `State`:`success`, the FPGA image is ready for downloading. Find FpgaImageUUID and note it down.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612115_en-US.png)

    3.  Run the following command. In the returned message, find and note down FpgaUUID.

        ```
        faascmd list_instances --instanceId=hereIsYourInstanceId # Replace hereIsYourInstanceId with the f3 instance ID
        ```

    4.  Run the command to download the FPGA image.

        ```
        
        faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=hereIsShellVersionOfFpga
        # Replace hereIsYourInstanceId with the f3 instance ID, hereIsFpgaUUID with the FpgaUUID, and hereIsImageUUID with the FpgaImageUUID
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612116_en-US.png)

    5.  Run the command to view if the image is downloaded successfully.

        ```
        faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceId # Replace hereIsFpgaUUID with the obtained FpgaUUID, and hereIsYourInstanceId with the f3 instance ID
        ```

        Below is an example of the returned message. If the FpgaImageUUID in the message is the same as the FpgaImageUUID you note down and the message shows `"TaskStatus":"valid"`, the image is downloaded successfully.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9830/154777961612117_en-US.png)


## Step 6: Run the Host program {#section_tft_w5l_2fb .section}

To run the Host program, follow these steps:

1.  Run the following command to configure the environment.

    ```
    source /root/xbinst_oem/f3_env_setup.sh xocl  # Run the command each time you open a new terminal window
    ```

2.  Configure the sdaccel.ini file.

    In the directory where the Host binary file is located, run the `vim sdaccel.ini` command to create the sdaccel.ini file and enter the following content.

    ```
    [Debug]
    profile=true
    [Runtime]
    runtime_log = "run.log"
    hal_log = hal.log
    ert=false
    kds=false
    ```

3.  Run the Host.
    -   For vadd, run the command:

        ```
        make -f sdaccel.mk host
        ./vadd bin_vadd_hw.xclbin
        ```

    -   For kernel\_global\_bandwidth, run the command:

        ```
        ./kernel_global
        ```


If `Test Passed` is returned, the test is successful.

## Other common commands {#section_ltf_z5l_2fb .section}

This section introduces some common commands for f3 instances.

|Task|Command|
|:---|:------|
|View the help document|`make -f ./sdaccel.mk help`|
|Run software emulation|`make -f ./sdaccel.mk run_cpu_em`|
|Run hardware emulation|`make -f ./sdaccel.mk run_hw_em`|
|Compile the host code only|`make -f ./sdaccel.mk host`|
|Compile and generate files for downloading|`make -f sdaccel.mk xbin_hw`|
|Clean a work directory|`make -f sdaccel.mk clean`|
|Forcibly clean a work directory|`make -f sdaccel.mk cleanall`|

**Note:** 

-   During emulation, follow the Xilinx emulation process. You do not need to set up the f3\_env\_setup environment.
-   The SDAccel runtime and SDAccel development platform are available in the official f3 images provided by Alibaba Cloud. You can also download them at [SDAccel runtime](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/xbinst_oem.tar.gz) and [SDAccel development platform](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/platforms.tar.gz).

