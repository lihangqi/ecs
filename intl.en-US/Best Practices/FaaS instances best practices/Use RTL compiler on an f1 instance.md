# Use RTL compiler on an f1 instance {#concept_n5c_vt3_dfb .concept}

This topic describes how to use Register Transfer Level \(RTL\) compiler on an f1 instance.

**Note:** 

-   All the operations described in this topic must be performed by one account in the same region.
-   We strongly recommend that you use an f1 instance as a RAM user. To avoid unwanted operations, you must authorize the RAM user to perform required actions only. You must create a role for the RAM user and grant temporary permissions to the role to access the OSS buckets. If you want to encrypt the IP address, grant the RAM user to use Key Management Service \(KMS\). If you want the RAM user to check permissions, authorize the RAM user to view the resources of an account.

## Prerequisites {#section_il5_153_dfb .section}

-   Create an f1 instance and add a security group rule to allow Internet access to SSH Port 22 of the instance.

    **Note:** Only the image we share with you can be used on an f1 instance. For more information, see [Create an f1 instance](../../../../intl.en-US/Instances/Instance type families/Compute optimized type family with FPGA/Create an f1 instance.md) .

-   Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) to obtain the instance ID.
-   Activate OSS and [create an OSS bucket](../../../../intl.en-US/Quick Start/Create a bucket.md) to upload your files. The OSS bucket and the f1 instance must be owned by one account and operated in the same region.
-   For encryption, activate [Key Management Service \(KMS\)](../../../../intl.en-US/Quick Start/Quick start.md#).
-   To operate FPGA as a RAM user, do the following in advance:
    -   [Create a RAM](../../../../intl.en-US/Quick Start/(Old Version) Quick Start/Create a RAM user.md) and [grant permissions](../../../../intl.en-US/Quick Start/(Old Version) Quick Start/Authorize RAM users.md).
    -   [Create a RAM](../../../../intl.en-US/User Guide/(Old Version) User Guide/Identities/RAM roles.md) and [grant permissions](../../../../intl.en-US/User Guide/(Old Version) User Guide/Authorization management/Permission granting in RAM.md).
    -   Use the AccessKey to complete the authentication.

## Procedure {#section_i5l_453_dfb .section}

To use RTL compiler on an f1 instance, follow these steps.

## Step 1. Connect to the f1 instance {#section_ccx_f53_dfb .section}

[Connect to your f1 instance](../../../../intl.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md).

## Step 2. Configure the basic environment {#section_dcx_f53_dfb .section}

Run the script to configure the basic environment.

``` {#codeblock_7pg_kq0_i4i}
source /opt/dcp1_1/script/f1_env_set.sh
```

## Step 3. Compile the project {#section_fcx_f53_dfb .section}

Run the following commands to compile the project.

``` {#codeblock_0oq_ukm_3x1}
cd /opt/dcp1_1/hw/samples/dma_afu
afu_synth_setup --source hw/rtl/filelist.txt build_synth
cd build_synth/
run.sh
```

**Note:** It takes a long time to compile the project.

## Step 4. Create an image {#section_hcx_f53_dfb .section}

To create an image, follow these steps:

1.  Run the following commands to initialize `faascmd`.

    ``` {#codeblock_85b_b01_x2v}
    # If needed, add the environment variable and grant permission to run the commands.
    export PATH=$PATH:/opt/dcp1_1/script/
    chmod +x /opt/dcp1_1/script/faascmd
    # Replace hereIsMySecretId with your AccessKey ID. Replace hereIsMySecretKey with your AccessKey Secret. 
    faascmd config --id=hereIsMySecretId --key=hereIsMySecretKey
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey
    # Replace hereIsYourBucket with the OSS bucket name in the China (Hangzhou) region.
    faascmd auth --bucket=hereIsYourBucket
    ```

2.  Make sure you are at the /opt/dcp1\_1/hw/samples/dma\_afu directory, and run the command to upload the gbs file.

    ``` {#codeblock_u73_98s_nqg}
    faascmd upload_object --object=dma_afu.gbs --file=dma_afu.gbs
    ```

3.  Run the command to create an image.

    ``` {#codeblock_0cm_1ym_yk1}
    #  Replace hereIsYourImageName with your image name.
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=hereIsYourImageName --tags=hereIsYourImageTag --encrypted=false --shell=V1.1
    ```


## Step 5. Download the image {#section_ocx_f53_dfb .section}

To download the image, follow these steps:

1.  Run the `faascmd list_images` command to check whether the image is created.

    If `"State":"success"` exists in the returned result, it means the image is created. Record the FpgaImageUUID. Record the **FpgaImageUUID**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/156678540612086_en-US.png)

2.  Run the command to obtain FPGA ID.

    ``` {#codeblock_hyi_bkc_n7m}
    # Replace hereIsYourInstanceId with your f1 instance ID.
    faascmd list_instances --instanceId=hereIsYourInstanceId
    ```

    Record FpgaUUID in the returned result.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/156678541212087_en-US.png)

3.  Run the command to download the image to your f1 instance.

    ``` {#codeblock_39q_erf_7jl}
    # Replace hereIsYourInstanceID with your f1 instance ID. Replace hereIsFpgaUUID with your FpgaUUID. Replace hereIsImageUUID with your FpgaImageUUID.
    faascmd download_image --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID --fpgatype=intel --imageuuid=hereIsImageUUID --imagetype=afu --shell=V0.11
    ```

4.  Run the command to check whether the image is downloaded.

    ``` {#codeblock_3ca_jm7_nps}
    # Replace hereIsYourInstanceID with your f1 instance ID. Replace hereIsFpgaUUID with your FpgaUUID.
    faascmd fpga_status --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID
    ```

    If `"TaskStatus":"operating"` exists in the returned result, and the displayed FpgaImageUUID is identical with your recorded FpgaImageUUID, the image is downloaded.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/156678541612088_en-US.png)


## Step 6. Test {#section_xcx_f53_dfb .section}

Run the commands one by one for test.

``` {#codeblock_3n8_f5v_g2u}
cd /opt/dcp1_1/hw/samples/dma_afu/sw
make
sudo LD_LIBRARY_PATH=/opt/dcp1_1/hw/samples/dma_afu/sw:$LD_LIBRARY_PATH ./fpga_dma_test 0
```

If the following result is returned, the test is completed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9828/156678541912089_en-US.png)

**Note:** If the Huge pages feature is not enabled, run the following command to enable it.

``` {#codeblock_lxa_kf9_cwg}
sudo bash -c "echo 20 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages"
```

