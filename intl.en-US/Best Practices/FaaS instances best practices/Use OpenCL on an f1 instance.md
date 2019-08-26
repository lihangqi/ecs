# Use OpenCL on an f1 instance {#concept_61410_zh .concept}

This topic introduces how to use Open Computing Language \(OpenCL\) to create an image file, and then download the image to an FPGA chip.

**Note:** 

-   All the operations described in this topic must be performed by one account in the same region.
-   We strongly recommend that you use an f1 instance as a RAM user. To avoid unwanted operations, you must authorize the RAM user to perform required actions only. You must create a role for the RAM user and grant temporary permissions to the role to access the OSS buckets. If you want to encrypt the IP address, grant the RAM user to use Key Management Service \(KMS\). If you want the RAM user to check permissions, authorize the RAM user to view the resources of an account. Before you begin, complete the following:

## Prerequisites {#section_b44_gr3_dfb .section}

-   Create an f1 instance and add a security group rule to allow Internet access to SSH Port 22 of the instance.

    **Note:** Only the image we share with you can be used on an f1 instance. For more information, see [Create an f1 instance](../../../../reseller.en-US/Instances/Instance type families/Compute optimized type family with FPGA/Create an f1 instance.md).

-   Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to obtain the instance ID.
-   [Create an OSS bucket](../../../../reseller.en-US/Quick Start/Create a bucket.md) to upload your custom bitstream files. The OSS bucket and the f1 instance must be owned by one account and in the same region.
-   To encrypt your bitstream, activate Key Management Service \(KMS\).
-   To operate an f1 instance as a RAM user, you must do the following operations:
    -   [Create a RAM user](../../../../reseller.en-US/Quick Start/(Old Version) Quick Start/Create a RAM user.md) and [grant permissions](../../../../reseller.en-US/Quick Start/(Old Version) Quick Start/Authorize RAM users.md).
    -   [Create a RAM role](../../../../reseller.en-US/User Guide/(Old Version) User Guide/Identities/RAM roles.md) and [grant permissions](../../../../reseller.en-US/User Guide/(Old Version) User Guide/Authorization management/Permission granting in RAM.md).
    -   Create an AccessKey.

## Procedure {#section_xn8_vv7_h90 .section}

To configure the environment of FPGA Server Example, follow these steps.

## Step 1. Connect to your f1 instance {#section_gtn_u6n_tfu .section}

[Connect to the Linux instance](../../../../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md).

## Step 2. Install the basic environment {#section_rza_ct9_ori .section}

Run the following script to install the base environment.

``` {#codeblock_906_fye_b9z .language-shell}
source /opt/dcp1_1/script/f1_env_set.sh            
```

## Step 3. Download the OpenCL Example {#section_nma_nzp_cq9 .section}

Follow these steps to download the official opencl example.

1.  Create the /opt/tmp directory, and change the current directory to it.

    ``` {#codeblock_k4l_96w_xun .language-shell}
    mkdir -p /opt/tmp
    cd /opt/tmp                    
    ```

    Now, you are at the /opt/tmp directory.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/156677770411994_en-US.png)

2.  Run the commands one by one to download and decompress the OpenCL Example file.

    ``` {#codeblock_bj5_y93_tng .language-shell}
    wget https://www.altera.com/content/dam/altera-www/global/en_US/others/support/examples/download/exm_opencl_matrix_mult_x64_linux.tgz
    tar -zxvf exm_opencl_matrix_mult_x64_linux.tgz                    
    ```

    The following figure displays the directory after decompression.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/156677770411995_en-US.png)

3.  Change the current directory to the matrix\_mult directory and run the command for compilation.

    ``` {#codeblock_8hy_iso_54w .language-shell}
    cd matrix_mult
    aoc -v -g --report ./device/matrix_mult.cl                    
    ```

    The process of compilation takes several hours. You can open a new console, and run the `top` command to monitor processes and system resource usage on the instance and view the status of the compilation process.


## Step 4. Upload the configuration file to the OSS bucket {#section_py6_0cb_v87 .section}

Follow these steps to upload the configuration file.

1.  Run the commands to initialize the faascmd.

    ``` {#codeblock_6u6_2y8_b9i .language-shell}
    # If needed, add the environment variable and grant the permission to run the commands
    export PATH=$PATH:/opt/dcp1_1/script/
    chmod +x /opt/dcp1_1/script/faascmd
    # Replace hereIsYourSecretId with your AccessKey ID. Replace hereIsYourSecretKey with your AccessKey Secret
    faascmd config --id=hereIsYourSecretId --key=hereIsYourSecretKey
    # Replace hereIsYourBucket with the bucket name of your OSS in the Region China (Hangzhou).
    faascmd auth --bucket=hereIsYourBucket                    
    ```

2.  Change the current directory to the matrix\_mult/output\_files directory, and upload the configuration file.

    ``` {#codeblock_42r_m2e_2en .language-shell}
    cd matrix_mult/output_files # Now you are accessing/opt/tmp/matrix_mult/matrix_mult/output_files
    faascmd upload_object --object=afu_fit.gbs --file=afu_fit.gbs                    
    ```

3.  Use gbs to create an FPGA image.

    ``` {#codeblock_twi_7xv_a1l .language-shell}
    # Replace hereIsYourImageName with your image name. Replace hereIsYourImageTag with your image tag.
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=hereIsYourImageName --tags=hereIsYourImageTag --encrypted=false --shell=V1.1                    
    ```

4.  Run the `faascmd list_images` command to check whether the image is created. In the returned result, if `"State":"success"` is displayed, it means the image is created. Record the **FpgaImageUUID**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/156677770411996_en-US.png)


## Step 5. Download the image to your f1 instance {#section_otd_7fx_rwk .section}

To download the image to your f1 instance, follow these steps:

1.  Run the command to obtain FPGA ID.

    ``` {#codeblock_jf4_xfc_qkf .language-shell}
    # Replace hereIsYourInstanceId with your f1 instance ID.
    faascmd list_instances --instanceId=hereIsYourInstanceId                    
    ```

    Returned results sample: Record FpgaUUID in the returned result.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/156677770411997_en-US.png)

2.  Run the command to download the image to your f1 instance.

    ``` {#codeblock_oo8_95c_qmv .language-shell}
    # Replace hereIsYourInstanceID with your f1 instance ID. Replace hereIsFpgaUUID with your FPGA UUID. Replace hereIsImageUUID with your image UUID.
    faascmd download_image  --instanceId=hereIsYourInstanceID --fpgauuid=hereIsFpgaUUID --fpgatype=intel --imageuuid=hereIsImageUUID --imagetype=afu --shell=V0.11                    
    ```

3.  Run the command to check whether the image is downloaded.

    ``` {#codeblock_fqi_wnc_2dk .language-shell}
    # Replace hereIsYourInstanceID with your f1 instance ID. Replace hereIsFpgaUUID with your FPGA UUID.
    faascmd fpga_status --fpgauuid=hereIsFpgaUUID --instanceId=hereIsYourInstanceID                    
    ```

    If "TaskStatus": "operating" exists in the returned result, it means the image is downloaded.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9827/156677770411998_en-US.png)


## Step 6. Download the FPGA image to an FPGA chip {#section_6pr_jkf_8yb .section}

To download the FPGA image to an FPGA chip, follow these steps:

1.  Open the console in Step 1. If it is closed, repeat Step 1.
2.  Run the following command to configure the runtime environment for OpenCL.

    ``` {#codeblock_cj1_z3j_gfv .language-shell}
    sh /opt/dcp1_1/opencl/opencl_bsp/linux64/libexec/setup_permissions.sh                    
    ```

3.  Run the command to go back to the parent directory.

    ``` {#codeblock_bul_ze6_ika .language-shell}
    cd .. /.. # Now, you are at the /opt/tmp/matrix_mult directory                   
    ```

4.  Run the command to compile.

    ``` {#codeblock_4bv_kd1_7uf .language-shell}
    make
    # Output the environment configuration
    export CL_CONTEXT_COMPILER_MODE_ALTERA=3
    cp matrix_mult.aocx ./bin/matrix_mult.aocx
    cd bin
    host matrix_mult.aocx                    
    ```

    If the following result is returned, it means the configuration is successful. Note that the last line must be `Verification: PASS`.

    ``` {#codeblock_hz1_4rg_hdl .language-shell}
    [root@iZbpXXXXXZ bin]# ./host matrix_mult.aocx
    Matrix sizes:
      A: 2048 x 1024
      B: 1024 x 1024
      C: 2048 x 1024
    Initializing OpenCL
    Platform: Intel(R) FPGA SDK for OpenCL(TM)
    Using 1 device(s)
      skx_fpga_dcp_ddr : SKX DCP FPGA OpenCL BSP (acl0)
    Using AOCX: matrix_mult.aocx
    Generating input matrices
    Launching for device 0 (global size: 1024, 2048)
    Time: 40.415 ms
    Kernel time (device 0): 40.355 ms
    Throughput: 106.27 GFLOPS
    Computing reference output
    Verifying
    Verification: PASS
    ```


