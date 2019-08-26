# Use faascmd {#concept_vrl_rn1_tfb .concept}

This topic describes how to use faascmd commands.

## Prerequisite {#section_v5y_n51_tfb .section}

You have [configured faascmd](intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Configure faascmd.md#) before using it.

## Syntax description {#section_k5j_b2v_vfb .section}

-   All commands and parameters provided by faascmd are case-sensitive.

-   There must be no space before and after equal signs \(=\) in the parameters of faascmd commands.


## Authorize users {#section_wgv_4f5_tfb .section}

The `faascmd auth` command is used to authorize the faas admin user to access the users' OSS buckets.

**Prerequisites**

1.  You have created an OSS bucket for FaaS to upload the originally compiled DCP file.

2.  You have created a folder named compiling\_logs in the FaaS OSS bucket.


**Command format**

```
faascmd auth --bucket=<yourFaasOSSBucketName>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431129_en-US.png)

**Note:** If an Alibaba Cloud account has multiple RAM user accounts, we recommend that the RAM user accounts share an OSS bucket to prevent authorization policies from being repeatedly modified or overwritten.

## View authorization policies {#section_xbt_srr_5fb .section}

The `faascmd list_policy` command is used to view whether the specified OSS bucket has been added to the corresponding authorization policy \(faasPolicy\).

**Command format**

```
faascmd list_policy
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431130_en-US.png)

**Note:** You need to check whether your OSS bucket and OSS bucket/compiling\_logs appear in the policy information.

## Delete authorization policies {#section_pnl_xrr_5fb .section}

The `faascmd delete_policy` command is used to delete authorization policies \(faasPolicy\).

**Command format**

```
faascmd delete_policy
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431131_en-US.png)

**Note:** If an Alibaba Cloud account has multiple RAM user accounts, we recommend that you delete the target policy in the RAM console to prevent incorrect authorization policy deletion.

## View all objects under an OSS bucket {#section_t1s_1sr_5fb .section}

The `faascmd list_objects` command is used to view all objects under your OSS bucket.

**Command format**

```
faascmd list_objects
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431132_en-US.png)

**Note:** You can use this command with the grep command to filter for the files you want, for example, `faascmd list_objects | grep "xxx"`.

## Upload original compilation files {#section_k45_dsr_5fb .section}

The `faascmd upload_object` command is used to upload the original files that are compiled on your local PC to a specified OSS bucket.

**Command format**

```
faascmd upload_object --object=<newFileNameinOSSBucket> --file= <your_file_path>/fileNameYouWantToUpload 

```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431112_en-US.png)

**Note:** 

-   No path is needed if the target files are stored in the current directory.

-   Locally compiled original files provided by Intel FPGA are in .gbs format and those provided by Xilinx FPGA are compressed as packages in .tar format after script processing.


## Download objects from an OSS bucket {#section_b4q_gsr_5fb .section}

The `faascmd get_object` command is used to download a specified object from an OSS bucket.

**Command format**

```
faascmd get_object --obejct=<yourObjectName> --file=<your_local_path>/<yourFileName>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431115_en-US.png)

**Note:** If no path is provided, the objects are downloaded to the current folder by default.

## Create FPGA images {#section_rbl_ksr_5fb .section}

The `faascmd create_image` command is used to submit FPGA image creation requests. If the request succeeds, fpga imageuuid is returned.

**Command format**

```
faascmd create_image --object=<yourObjectName> 
--fpgatype=<intel/xilinx>  --encrypted=<true/false> 
--kmskey=<key/mandatory if encrypted is true> 
--shell=<Shell Version/mandatory> --name=<name/optional> 
--description=<description/optional> --tags=<tags/optional>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431117_en-US.png)

## View FPGA images {#section_msw_nsr_5fb .section}

The `faascmd list_images` command is used to view information about all the FPGA images you have created.

**Command format**

```
faascmd list_images
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431118_en-US.png)

**Note:** A maximum of 10 FPGA images can be reserved for each RAM user account.

## Delete FPGA images {#section_pkw_qsr_5fb .section}

The `faascmd delete_image` command is used to delete FPGA images.

**Command format**

```
faascmd delete_image --imageuuid=<yourImageuuid>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726431120_en-US.png)

## Download FPGA images {#section_cmr_tsr_5fb .section}

The `faascmd download_image` command is used to submit FPGA image download requests.

**Command format**

```
faascmd download_image  --instanceId=<yourInstanceId> 
--fpgauuid=<yourfpgauuid> --fpgatype=<intel/xilinx> 
--imageuuid=<yourImageuuid> --imagetype=<afu> 
--shell=<yourImageShellVersion>
```

**Code example**

```
faascmd download_image --instanceId=XXXXX --fpgauuid=XXXX --fpgatype=intel --imageuuid=XXXX
```

## View the FPGA image download status {#section_dhj_wsr_5fb .section}

The `faascmd fpga_status` command is used to view the status of the current FPGA board card and the FPGA image download status.

**Command format**

```
faascmd fpga_status --fpgauuid=<fpgauuid> --instanceId=<instanceId>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726531125_en-US.png)

## Publish FPGA images {#section_snv_ysr_5fb .section}

The `faascmd publish_image` command is used to submit FPGA image publishing requests.

**Command format**

```
faascmd publish_image --imageuuid=<yourImageuuid> --imageid=<yourFPGAImageid>
```

**Note:** 

-   imageuuid is the ID of the image you are going to publish to the cloud marketplace. You can view the image ID by running the `faascmd list_images` command.
-   imageid is the FPGA image ID. You can view the ID on the instance details page in the ECS console.

## View FPGA instance information {#section_vhb_btr_5fb .section}

The `faascmd list_instances` command is used to obtain basic information about an FPGA instance, including the instance ID, FPGA board card information, and shell version.

**Command format**

```
faascmd list_instances --instanceId=<yourInstanceId>
```

**Code example**

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61626/154398726531126_en-US.png)

