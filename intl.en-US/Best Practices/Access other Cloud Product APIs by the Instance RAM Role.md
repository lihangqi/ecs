# Access other Cloud Product APIs by the Instance RAM Role {#concept_54579_zh .concept}

Previously, applications deployed on an ECS Instance usually needed to use AccessKey ID and AccessKey Secret \(AK\) to access APIs of other Alibaba Cloud products. AK is the key to accessing Alibaba Cloud APIs and has all of the permissions of the corresponding accounts. To help applications manage the AK, you have to save AK in the configuration files of the application or save it in an ECS instance by using other methods, which makes it more complicated to manage the AK and reduces its confidentiality. What’s more, if you need concurrent deployment across regions, the AK is diffused along with the images or instances created by the image, which makes you have to update and re-deploy the instances and images one by one when changing the AK.

Now with the help of the instance [RAM role](https://www.alibabacloud.com/help/doc-detail/28649.htm), you can assign a RAM role to an ECS instance. The applications on the instance can then access APIs of other cloud products with the STS credential. The STS credential is automatically generated and updated by the system, and the applications can use the specified [meta data](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md) URL to obtain the STS credential without special management. Meanwhile, you can modify the RAM role and the authorization policy to grant different or identical access permissions to an instance to different Alibaba Cloud products.

This article introduces how to create an ECS instance that plays a RAM role and how to enable applications on the ECS instance to access other Alibaba Cloud products with the STS credential.

**Note:** To make it easy for you to get started with the example in this article, all of the operations in the document are done in [OpenAPI Explorer](https://api.aliyun.com/) OpenAPI Explorer obtains the temporary AK of the current account through the logged user information, and initiates online resource operation to the current account. Please execute operations carefully. Creating an instance will incur charges. Please release the instance soon after completing the operation.

## Procedure { .section}

To enable python on an instance to access an OSS bucket under the same account by using the instance RAM role, follow these steps:

Step 1. Create a RAM role and attach it to an authorization policy.

Step 2. Create an ECS instance playing the RAM role to create.

Step 3. Within the instance, access the metadata URL to obtain the STS credential.

Step 4. Use Python to access OSS using the STS credential.

## Step 1. Create a RAM role and attach it to an authorization policy { .section}

Use the CreateRole API to

1.  create a RAM role. The required request parameters are:
    -    **RoleName**:Specify a name for the role. *EcsRamRoleTest*is used in this example.
    -    **AssumeRolePolicyDocument**:Specify a policy as follows, which indicates that the role to be created is a service role and an Alibaba Cloud product \(ECS in this example\) is assigned to play this role.

        ```
        {
        "Statement": [
        {
        "Action": "sts:AssumeRole",
        "Effect": "Allow",
        "Principal": {
        "Service ":[
          "ecs.aliyuncs.com"
        ]
        }
        }
        ],
        "Version": "1"
        }
        
        ```

2.  Use the CreatePolicy API to create an authorization policy. The required request parameters are:
    -    **PolicyName**: Specify a name for the authorization policy. *EcsRamRolePolicyTest* is used in this example.
    -    **PolicyDocument**: Specify a policy as follows, which indicates that the role has OSS read-only permission.

        ```
        {
        "Statement": [
        {
        "Action": [
        "oss:Get*",
        "oss:List*"
        ],
        "Effect": "Allow",
        "Resource ":"*"
        }
        ],
        "Version": "1"
        }
        
        ```

3.  Use the AttachPolicyToRole API to attach the authorization policy to the role. The required request parameters are:
    -    **PolicyType**: Set it to *Custom*.
    -    **PolicyName**: Use the policy name specified in step 2. Use. *EcsRamRolePolicyTest*in this example.
    -    **RoleName**: Use the role name specified in step 1. Use *EcsRamRoleTest*in this example.

## Step 2. You can use either method to create an ECS instance playing the RAM role: { .section}

Attach a RAM role to an existing VPC-Connected ECS instance.

-   Create a VPC-Connected ECS instance with the RAM role
-   Attach a RAM role to an existing VPC-Connected ECS instance

**Create a VPC-Connected ECS instance with the RAM role**

Use the AttachInstanceRamRole API to attach a RAM role to an existing VPC-Connected ECS instance. The parameters are as follows:

-    **RegionId**:The ID of the region where the instance is located.
-    **RamRoleName**:The name of a RAM role. In this example, EcsRamRoleTest is used. In this example, *EcsRamRoleTest*.
-    **InstanceIds**:The IDs of VPC-Connected ECS instances that you want to attach the RAM role to, in the format of \[“i-bXXXXXXXX”\] for one instance, or \[“i-bXXXXX”, “i-cXXXXX”, \["i-bXXXXXXXX"\]for multiple instances.

**Create a VPC-Connected ECS instance with the RAM role**

You must have a VPC network before creating an ECS instance with the RAM role.

1.  To create a VPC-Connected ECS instance with the RAM role, follow these steps: Use the CreateInstance API to create an ECS instance. The required request parameters are:

    -    **RegionId**:The region of the instance. In this example, cn-hangzhou is used. In this example, *cn-hangzhou*is used.
    -    **ImageId**:The image of the instance. In this example, centos\_7\_03\_64\_40G\_alibase\_20170503.vhd is used. In this example,*centos\_7\_03\_64\_40G\_alibase\_20170503.vhd*is used.
    -    **InstanceType**:The type of the instance. In this example, *ecs.xn4.small*is used.
    -    **VSwitchId**:The virtual switch of the VPC network where the instance is located. Because the instance RAM role only supports VPC network, VSwitchId is required.
    -    **RamRoleName**:The name of RAM Role. In this example, *EcsRamRoleTest*is used.
    If you want to authorize a sub account to create an ECS instance playing the specified RAM role, besides the permission to create an ECS instance, the sub account must have the PassRole permission. Therefore, you must customize an authorization policy as follows and attach it to the sub account. If the action is creating an ECS instance only, set \[ECS RAM Action\] to `ecs:CreateInstance`。 If you want to grant all ECS action permissions to the sub account, set \[ECS RAM Action\] to `ecs:*`.

    ```
    {
      "Statement": [
        {
          "ecs: [ECS RAM Action]", 
          "Resource": "*",
          "Effect": "Allow"
        },
    	{
          "Action": "ram:PassRole",
          "Resource": "*",
          "Effect": "Allow"
      ],
      "Version": "1"
    }
    
    ```

2.  Set the password and start the instance.
3.  Set the ECS instance to access the Internet by using API or in the ECS console.

## Step 3:  Access the metadata URL within the instance to obtain the STS credential { .section}

To obtain the STS credential of the instance, follow these steps:

**Note:** A new STS credential is generated 30 minutes before the current one expires. Both STS credentials can be used during this period of time.

1.  [Connect to the instance](../../../../intl.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md).
2.  Access the following URL to obtain the STS credential. `http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest` The last part of the URL is the RAM role name, which must be replaced with the one you create. The last part of the path is the RAM role name which should be replaced by one you create.

    **Note:** In this example, use the curly command to access the above `curl` In this example, we run the curl command to access the URL. If you are using a Windows ECS instance, see[Use metadata of an instance](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md)in ECS the User Guide to obtain the STS credential.

    The return parameters are as follows.

    ```language-shell
    [root@local ~]# curl http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest
    {
    "AccessKeyId" : "XXXXXXXXX",
    "AccessKeySecret" : "XXXXXXXXX",
    "Expiration" : "2017-06-09T09:17:19Z",
    "SecurityToken" : "CAIXXXXXXXXXXXwmBkleCTkyI+",
    "LastUpdated" : "2017-10-31T23:20:01Z",
    "Code" : "Success"
    }
    
    ```


## Step 4:  Use Python SDK to access OSS with the STS credential { .section}

In this example, with the STS credential, we use Python to list 10 files in an OSS bucket that is in the same region with the instance.

**Prerequisites**

You have remotely connected to the ECS instance.

Python has been installed on the ECS instance. If you are using a Linux ECS instance, pip must be installed.

A bucket has been created in the region of the instance, and the bucket name and the Endpoint have been acquired. In this example, the bucket name is `ramroletest`, and the endpoint is `oss-cn-hangzhou.aliyuncs.com`.

**Procedure**

To use Python to access the OSS bucket, follow these steps:

1.  Run the command `pip install oss2` to install OSS Python SDK.
2.  Run the following commands to test, of which:

    -    `The three parameters in oss2. StsAuth` correspond respectively to AccessKeyId, AccessKeySecret and SecurityToken returned by the above URL.
    -    `The last two parameters in oss2. Bucket`are the bucketcodeph name and the endpoint.
    ```
    	import oss2
    	from itertools import islice
    	auth = oss2. StsAuth(<AccessKeyId>, <AccessKeySecret>, <SecurityToken>)
    	bucket = oss2. bucket = oss2.Bucket(auth, <your Endpoint>, <your Bucket name>)
    	for b in islice(oss2. ObjectIterator(bucket), 10):
    	    print(b.key)
    
    ```

    Output results are as follows:

    ```language-python
    [root@local ~]# python
    Python 2.7.5 (default, Nov  6 2016, 00:28:07)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import oss2
    >>> from itertools import islice
    >>> auth = oss2. StsAuth("STS.J8XXXXXXXXXX4", "9PjfXXXXXXXXXBf2XAW", "CAIXXXXXXXXXXXwmBkleCTkyI+")
    >>> bucket = oss2. Bucket(auth, "oss-cn-hangzhou.aliyuncs.com", "ramroletest")
    >>> for b in islice(oss2. ObjectIterator(bucket), 10):
    ...     print(b.key)
    ...
    ramroletest.txt
    test.sh
    
    ```


