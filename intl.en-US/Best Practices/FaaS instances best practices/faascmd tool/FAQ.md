# FAQ {#concept_ifw_1sc_5fb .concept}

This topic lists common FAQs relating to the faascmd tool and provides corresponding solutions.

## FAQ {#section_rfg_gxs_5fb .section}

-   **What do I do if an error indicating "Name Error:global name'ID' is not defined." is reported?**

    **Cause**: faascmd cannot obtain your AccessKeyId or AccessKeySecret.

    **Solution**: Run the `faascmd config` command. Then, the information about the AccessKeyId and AccessKeySecret you have entered will be saved in the `/root/.faascredentials` file.

-   **What do I do if an error indicating "HTTP Status:403 Error:RoleAccessError. You have no right to assume this role." is reported?**

    **Cause**: faascmd cannot obtain information about the role ARN or the obtained ARN does not belong to the same account as the existing AccessKeyId and AccessKeySecret.

    **Solution**: Check whether the following information is contained in the `/root/.faascredentials` file:

    ```
    [FaaSCredentials]
    accessid=xxxxxxxxxx
    accesskey=xxxxxxxxxxxxxxxxxxxxxxx
    [Role]
    role=acs:ram::1234567890123456:role/xxxxxx
    [OSS]
    bucket=xxxx
    ```

    **Note:** 

    -   If the preceding information already exists, check whether the role ARN and the AccessKeyId/AccessKeySecret belong to the same account.
    -   If the preceding information does not exist, run `faascmd auth bucket=xxxx` to grant permissions.
-   **What do I do if an error indicating "HTTP Status: 404 Error: EntityNotExist. Role Error. The specified Role not exists." is reported?**

    **Cause**: There is no faasrole role in your account.

    **Solution**: Log on to the RAM console to check whether a faasrole role exists.

    -   If no faasrole role exists, run the `faascmd config` and `faascmd auth` commands to create such a role and grant permissions to it.
    -   If a faasrole role already exists, open a ticket.
-   **What do I do if an error indicating "SDK.InvalidRegionId. Can not find endpoint to access." is reported?**

    **Cause**: faascmd cannot obtain the endpoint address of FaaS.

    **Solution**: Perform the following steps check whether faascmd configurations meet the specified requirements:

    -   Run the `python -V` command to check whether the Python version is 2.7.x.
    -   Run the `which python` command to check whether the default installation path of Python is `/usr/bin/python`.
    -   Run the `cat /usr/lib/python2.7/site-packages/aliyunsdkcore/__init__.py` command to check whether the aliyunsdkcore version is 2.11.0 or later.

        **Note:** If the aliyunsdkcore version is earlier than 2.11.0, you need to run the `pip install --upgrade aliyun-python-sdk-core` command to upgrade the aliyunsdkcore to the latest version.

-   **What do I do if an error indicating "HTTP Status:404 Error:SHELL NOT MATCH The image Shell is not match with fpga Shell! Request ID:D7D1AB1E-8682-4091-8129-C17D54FD10D4" is returned when I download an image?**

    **Cause**: The shell versions of the target FPGA image and the specified FPGA do not match.

    **Solution**: Perform the following steps:

    -   Run the `faascmd list_instances --instance=xxx` command to check the shell version of the current FPGA.

    -   Run the `faascmd list_images` command to check the shell version of the specified FPGA image.

        **Note:** 

        -   If the two shell versions are different, you need to create an FPGA image whose shell version is the same as that of the FPGA, and then download the image.
        -   If the two shell versions are consistent, open a ticket.
-   **What do I do if an error indicating "HTTP Status:503 Error:ANOTHER TASK RUNNING. Another task is running,user is allowed to take this task half an hour Request ID: 5FCB6F75-8572-4840-9BDC-87C57174F26D" is returned when I download an image?**

    **Cause**: The FPGA is stuck in operating state due to unexpected failure or interruption of the download request you have submitted.

    **Solution**: Wait for 10 minutes until the download task ends, and then resubmit an image download request.

    **Note:** If the problem persists, open a ticket.

-   **What do I do if the image status is failed when I run the faascmd list\_images command?**

    **Solution**: Obtain the compilation logs for troubleshooting by running the following command:

    ```
    faascmd list_objects|grep vivado
    faascmd get_object --obejct=<yourObjectName> --file=<your_local_path>/vivado.log  #The path is optional. The compilation logs are downloaded to the current folder by default.
    ```


## Common error codes {#section_tzt_drr_5fb .section}

|faascmd command|API name|Error message|Error description|Error code|
|:--------------|:-------|:------------|:----------------|:---------|
|Applicable to all commands|Applicable to all APIs|PARAMETER INVALIDATE|The input parameter is incorrect.|400|
|Applicable to all commands|Applicable to all APIs|InternalError|There is an internal error. Please open a ticket.|500|
|auth|auth|NoPermisson|You do not have the permission to access a specific open API.|403|
|create\_image|CreateFpgaImage|IMAGE NUMBER EXCEED|There cannot be more than 10 images in the image list. Please delete unnecessary images and try again.|401|
|FREQUENCY ERROR|The interval for submitting image requests is 30 minutes.|503|
|SHELL NOT SUPPORT|The input shell version is not supported. Please verify that the shell version is correct.|404|
|EntityNotExist.RoleError|The current account has no faasrole role.|404|
|RoleAccessError|The role ARN is empty, or the role ARN and the AccessKeyId/AccessKeySecret do not belong to the same account.|403|
|InvalidAccessKeyIdError|The AccessKeyId/AccessKeySecret is invalid.|401|
|Forbidden.KeyNotFoundError|The specified KMS key cannot be found. Please log on to the KMS console and check whether the input KeyId exists.|503|
|AccessDeniedError|The faas admin account is not authorized to access the current bucket.| |
|OSS OBJECT NOT FOUND|The specified OSS bucket/object does not exist or is inaccessible.|404|
|delete\_image|DeleteFpgaImage|IMAGE NOT FOUND|The specified FPGA image cannot be found.|400|
|list\_instances|DescribeFpgaInstances|NOT AUTHORIZED|The specified instance does not exist or does not belong to the current account.|401|
|RoleAccessError|The role ARN is empty, or the role ARN and the AccessKeyId/AccessKeySecret do not belong to the same account.|403|
|INSTANCE INVALIDATE|The specified instance is not an FPGA instance. If the specified instance is an FPGA instance, please open a ticket.|404|
|fpga\_status|DescribeLoadTaskStatus|NOT AUTHORIZED|The specified instanceId cannot be found. Please check the input parameter.|401|
|FPGA NOT FOUND|The specified fpgauuid cannot be found. Please check the input parameter.|404|
|download\_image|LoadFpgaImage|ANOTHER TASK RUNNING|The image download task you submitted is still in operating state.|503|
|IMAGE ACCESS ERROR|The specified image does not belong to the current account.|401|
|YOU HAVE NO ACCESS TO THIS INSTANCE|The specified instance does not belong to the current account.|401|
|IMAGE NOT FOUND|The specified FPGA image cannot be found.|404|
|FPGA NOT FOUND|The specified FPGA cannot be found.|404|
|SHELL NOT MATCH|The image and the specified FPGA do not match in shell version.|404|
|RoleAccessError|The role ARN is empty, or the role ARN and the AccessKeyId/AccessKeySecret do not belong to the same cloud account.|403|
|Image not in success state|The specified image is not in success state. Only images in success state can be downloaded.|404|
|publish\_image|PublishFpgaImage|FPGA IMAGE STATE ERROR|The specified image is not in success state.|404|
|FPGA IMAGE NOT FOUND|The specified image cannot be found or does not belong to the current account.|404|

