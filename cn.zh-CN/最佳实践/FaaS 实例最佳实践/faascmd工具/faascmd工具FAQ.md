# faascmd工具FAQ {#concept_ifw_1sc_5fb .concept}

本文介绍使用faascmd工具时常见的问题与解决办法。

## 常见问题 {#section_rfg_gxs_5fb .section}

-   **Name Error:global name'ID' is not defined.**

    **原因**：faascmd没有获取到您的AccessKeyID或AccessKeySecret信息。

    **解决办法**：执行`faascmd config`命令，此命令执行后，会将您输入的AccessKeyID和AccessKeySecret信息保存在文件`/root/.faascredentials` 中。

-   **HTTP Status:403 Error:RoleAccessError. You have no right to assume this role.**

    **原因**：faascmd没有获取到roleArn信息，或者roleArn信息与当前的AccessKeyID和AccessKeySecret信息不属于同一个账户。

    **解决办法**：检查`/root/.faascredentials`文件是否包含以下信息。

    ```
    [FaaSCredentials]
    accessid=xxxxxxxxxx
    accesskey=xxxxxxxxxxxxxxxxxxxxxxx
    [Role]
    role=acs:ram::1234567890123456:role/xxxxxx
    [OSS]
    bucket=xxxx
    ```

    **说明：** 

    -   如果上述信息存在，确认该role信息与AccessKeyID/AccessKeySecret的云ID是否一致。
    -   如果上述信息不存在，执行 `faascmd auth bucket=xxxx` 命令授权。
-   **HTTP Status: 404 Error: EntityNotExist. Role Error. The specified Role not exists .**

    **原因**：您的云账户下的faasrole角色不存在。

    **解决办法**： 登陆RAM控制台查看faasrole角色是否存在。

    -   如果faasrole角色不存在，您需要执行 `faascmd config` 和 `faascmd auth` 命令创建该角色并为其授权。
    -   如果faasrole角色存在，请提交工单处理。
-   **SDK.InvalidRegionId. Can not find endpoint to access.**

    **原因**：获取不到faas服务的endpoint地址。

    **解决办法**：您需要逐项检查是否满足以下配置。

    -   运行`python -V`命令检查python版本是否为2.7.x。
    -   运行`which python`命令检查python的默认安装路径是否为 `/usr/bin/python` 。
    -   运行`cat /usr/lib/python2.7/site-packages/aliyunsdkcore/__init__.py`命令检查aliyunsdkcore版本是否为2.11.0及以上。

        **说明：** 如果aliyunsdkcore版本号低于2.11.0，您需要运行`pip install --upgrade aliyun-python-sdk-core`命令升级至最新版本。

-   **下载镜像时返回 HTTP Status:404 Error:SHELL NOT MATCH. The image Shell is not match with fpga Shell!Request ID:D7D1AB1E-8682-4091-8129-C17D54FD10D4**

    **原因**：要下载的fpgaImage和指定fpga上的shell版本不匹配。

    **解决办法**：您需要按下列步骤逐项检查。

    -   运行`faascmd list_instances --instance=xxx`命令检查当前fpga的shell版本号。

    -   运行`faascmd list_images`命令检查指定的fpgaImage的shell版本号。

        **说明：** 

        -   如果以上两个shell版本号不同，您需要重新制作一个与fpga的shell版本号相同的fpgaImage，然后下载。
        -   如果确定两个shell版本一致，请提交工单。
-   **下载镜像时返回HTTP Status:503 Error:ANOTHER TASK RUNNING . Another task is running,user is allowed to take this task half an hour Request ID: 5FCB6F75-8572-4840-9BDC-87C57174F26D**

    **原因**：您之前提交的下载请求异常失败或中断导致fpga的状态还停留在operating状态。

    **解决办法**：建议您等待10分钟，直至下载任务自动结束，然后再次提交下载镜像请求。

    **说明：** 如果问题仍旧没有解决，请提交工单。

-   **运行faascmd list\_images命令时，发现镜像状态是failed。**

    **解决方法**：您可以通过以下方式获取编译日志，以定位相关错误。

    ```
    faascmd list_objects|grep vivado
    faascmd get_object --obejct=<yourObjectName> --file=<your_local_path>/vivado.log  #路径选填，默认下载到当前文件夹。
    ```


## 常见错误码 {#section_tzt_drr_5fb .section}

|faascmd命令|API名字|错误信息|错误描述|错误码|
|:--------|:----|:---|:---|:--|
|适用所有命令|适用所有API|PARAMETER INVALIDATE|输入参数有误。|400|
|适用所有命令|适用所有API|InternalError|未知错误，提交工单。|500|
|auth|auth|NoPermisson|没有访问某个openAPI的权限。|403|
|create\_image|CreateFpgaImage|IMAGE NUMBER EXCEED|镜像列表不能超过10个镜像，删除不需要的镜像即可。|401|
|FREQUENCY ERROR|目前提交镜像请求的时间间隔为30min一次。|503|
|SHELL NOT SUPPORT|输入的shell版本不支持，请检查shell版本是否正确。|404|
|EntityNotExist.RoleError|用户账户没有创建faasRole。|404|
|RoleAccessError|用户输入的roleArn为空，或者roleArn信息与AccessKey ID/AccessKey Secret不属于同一个云账号。|403|
|InvalidAccessKeyIdError|AccessKey ID/AccessKey Secret不合法。|401|
|Forbidden.KeyNotFoundError|找不到指定的KMS key，请登陆KMS控制台检查输入的keyId是否存在。|503|
|AccessDeniedError|faas admin 账户没有访问当前bucket的权限。| |
|OSS OBJECT NOT FOUND|指定的oss bucket/object不存在，或者不具备访问权限。|404|
|delete\_image|DeleteFpgaImage|IMAGE NOT FOUND|指定的fpgaImage找不到。|400|
|list\_instances|DescribeFpgaInstances|NOT AUTHORIZED|指定的instance不存在或者不属于当前的云账户。|401|
|RoleAccessError|用户输入的roleArn为空，或者roleArn信息与AccessKey ID/AccessKey Secret不属于同一个云账号。|403|
|INSTANCE INVALIDATE|指定的instance不属于fpga实例。如果确定是fpga实例，请提交工单。|404|
|fpga\_status|DescribeLoadTaskStatus|NOT AUTHORIZED|找不到指定的instanceId，请检查输入参数。|401|
|FPGA NOT FOUND|找不到指定fpgauuid，请检查输入参数。|404|
|download\_image|LoadFpgaImage|ANOTHER TASK RUNNING|之前提交的下载镜像任务还在operating状态。|503|
|IMAGE ACCESS ERROR|指定的image不属于当前云账户。|401|
|YOU HAVE NO ACCESS TO THIS INSTANCE|指定的instance不属于当前的云账户。|401|
|IMAGE NOT FOUND|指定的fpgaImage找不到。|404|
|FPGA NOT FOUND|指定的fpga找不到。|404|
|SHELL NOT MATCH|镜像的shell版本和指定的fpga上的shell版本不匹配。|404|
|RoleAccessError|用户输入的roleArn为空，或者roleArn信息与AccessKey ID/AccessKey Secret不属于同一个云账号。|403|
|Image not in success state|指定的image不是success状态，只有状态为success的image才可以下载。|404|
|publish\_image|PublishFpgaImage|FPGA IMAGE STATE ERROR|指定的image不是success状态。|404|
|FPGA IMAGE NOT FOUND|指定的image没有找到或者不属于当前用户。|404|

