# 借助于实例RAM角色访问其他云产品 {#concept_54579_zh .concept}

以往部署在 ECS 实例中的应用程序如果需要访问阿里云其他云产品，您通常需要借助AccessKeyID 和 AccessKeySecret（下文简称 AK）来实现。AK 是您访问阿里云 API 的密钥，具有相应账号的完整权限。为了方便应用程序对 AK 的管理，您通常需要将 AK 保存在应用程序的配置文件中或以其他方式保存在 ECS 实例中，这在一定程度上增加了 AK 管理的复杂性，并且降低了 AK 的保密性。甚至，如果您需要实现多地域一致性部署，AK 会随着镜像以及使用镜像创建的实例扩散出去。这种情况下，当您需要更换 AK 时，您就需要逐台更新和重新部署实例和镜像。

现在借助于 ECS 实例 RAM 角色，您可以将[RAM角色](https://www.alibabacloud.com/help/doc-detail/28649.htm?spm=a2c63.p38356.b99.242.266a64123yY8qA#top)和 ECS 实例关联起来，实例内部的应用程序可以通过 STS 临时凭证访问其他云产品。其中 STS 临时凭证由系统自动生成和更新，应用程序可以使用指定的[实例元数据](../../../../intl.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md)URL 获取 STS 临时凭证，无需特别管理。同时借助于 RAM，通过对角色和授权策略的管理，您可以达到不同实例对不同云产品或相同云产品具有各自访问权限的目的。

本文以部署在 ECS 实例上的 Python 访问 OSS 为例，详细介绍了如何借助 ECS 实例 RAM 角色，使实例内部的应用程序可以使用 STS 临时凭证访问其他云产品。

**说明：** 为了方便您随本文样例快速入门，文档里所有操作均在[OpenAPI Explorer](https://api.aliyun.com/?spm=a2c4g.11186623.2.16.21a418efIOhoV6)完成。OpenAPI Explorer 通过已登录用户信息获取当前账号临时 AK，对当前账号发起线上资源操作，请谨慎操作。创建实例操作会产生费用。操作完成后请及时释放实例。

## 操作步骤 { .section}

为了使 ECS 借助实例 RAM 角色，实现内部 Python 可以使用 STS 临时凭证访问 OSS，您需要完成以下步骤：

步骤 1. 创建 RAM 角色并配置授权策略

步骤 2. 指定 RAM 角色创建并设置 ECS 实例

步骤 3. 在实例内部访问实例元数据 URL 获取 STS 临时凭证

步骤 4. 基于临时凭证，使用 Python SDK 访问 OSS

## 步骤 1. 创建 RAM 角色并配置授权策略 { .section}

按以下步骤创建 RAM 角色并配置授权策略。

1.  创建 RAM 角色。找到 OpenAPI Explorer RAM 产品下 CreateRole API。其中：
    -   RoleName：设置角色的名称。根据自己的需要填写，本示例中为 EcsRamRoleTest。
    -   AssumeRolePolicyDocument： 填写如下内容，表示该角色为一个服务角色，受信云服务（本示例中为 ECS）可以扮演该角色。

        ```
        {
        "Statement": [
        {
        "Action": "sts:AssumeRole",
        "Effect": "Allow",
        "Principal": {
          "Service": [
            "ecs.aliyuncs.com"
          ]
        }
        }
        ],
        "Version": "1"
        }
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9825/155748259112522_zh-CN.png)

2.  创建授权策略。找到 OpenAPI Explorer RAM 产品下的 CreatePolicy API。其中：
    -   PolicyName：设置授权策略的名称。本示例中为 EcsRamRolePolicyTest。
    -   PolicyDocument：输入授权策略内容。本示例中填写如下内容，表示该角色具有 OSS 只读权限。

        ```
        {
        "Statement": [
        {
        "Action": [
          "oss:Get*",
          "oss:List*"
        ],
        "Effect": "Allow",
        "Resource": "*"
        }
        ],
        "Version": "1"
        }
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9825/155748259212523_zh-CN.png)

3.  为角色附加授权。找到 OpenAPI Explorer RAM 产品下 AttachPolicyToRole API。其中：
    -   PolicyType：填写 Custom。
    -   PolicyName：填写第 2 步创建的策略名称，如本示例中的 EcsRamRolePolicyTest。
    -   RoleName：填写第 1 步创建的角色名称，如本示例中的 EcsRamRoleTest。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9825/155748259212524_zh-CN.png)


## 步骤 2. 为 ECS 实例指定 RAM 角色 { .section}

您可以通过以下任一种方式为 ECS 实例指定 RAM 角色：

-   将实例 RAM 角色附加到一个已有的 VPC 类型ECS实例上
-   指定 RAM 角色创建并设置 ECS 实例

 **将实例 RAM 角色附加到一个已有的 VPC 类型ECS实例上** 

您可以使用 ECS 的 AttachInstanceRamRole API 附加实例 RAM 角色到已有的 VPC 类型 ECS 实例授权访问，设置信息如下：

-   RegionId：为实例所在的地域 ID。
-   RamRoleName：RAM 角色的名称。本示例中为 EcsRamRoleTest。
-   InstanceIds：需要附加实例 RAM 角色的 VPC 类型 ECS 实例 ID。本示例中为 \["i-bXXXXXXXX"\]。

 **指定 RAM 角色创建并设置 ECS 实例** 

按以下步骤指定 RAM 角色创建并设置 ECS 实例。

1.  创建实例。找到 OpenAPI Explorer ECS 产品下的 CreateInstance API，根据实际情况填写请求参数。必须填写的参数包括：

    -   RegionId：实例所在地域。本示例中为 cn-hangzhou。
    -   ImageId：实例的镜像。本示例中为 centos\_7\_03\_64\_40G\_alibase\_20170503.vhd。
    -   InstanceType：实例的规格。本示例中为 ecs.xn4.small。
    -   VSwitchId：实例所在的 VPC 虚拟交换机。因为 ECS 实例 RAM 角色目前只支持 VPC 类型 ECS 实例，所以 VSwitchId 是必需的。
    -   RamRoleName：RAM 角色的名称。本示例中为 EcsRamRoleTest。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9825/155748259212525_zh-CN.png)

    如果您希望授权子账号创建指定 RAM 角色的 ECS 实例，那么子账号除了拥有创建 ECS 实例的权限之外，还需要增加 PassRole 权限。所以，您需要创建一个如下所示的自定义授权策略并绑定到子账号上。如果是创建 ECS 实例，\[ECS RAM Action\] 可以是 `ecs:CreateInstance`，您也可以根据实际情况添加更多的权限。如果您需要为子账号授予所有 ECS 操作权限，\[ECS RAM Action\] 应该替换为 `ecs:*`。

    ```
    {
    "Statement": [
    {
    "Action": "[ECS RAM Action]", 
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

2.  设置密码并启动实例。
3.  使用 API 或在控制台设置 ECS 实例能访问公网。

## 步骤 3. 在实例内部访问实例元数据 URL 获取 STS 临时凭证 { .section}

按以下步骤获取实例的 STS 临时凭证。

**说明：** STS 临时凭证失效前半小时会生成新的 STS 临时凭证，在这半小时内，新旧 STS 临时凭证均可使用。

1.  远程连接实例。
2.  访问 `http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest` 获取 STS 临时凭证。路径最后一部分是 RAM 角色名称，您应替换为自己的创建的 RAM 角色名称。

    **说明：** 本示例中使用 `curl` 命令访问上述 URL。如果您使用的是 Windows ECS 实例，请参见[实例元数据](../../../../intl.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md)。

    示例输出结果如下。

    ```language-shell
    [root@local ~]# curl http://100.100.100.200/latest/meta-data/ram/security-credentials/EcsRamRoleTest
    {
    "AccessKeyId" : "STS.J8XXXXXXXXXX4",
    "AccessKeySecret" : "9PjfXXXXXXXXXBf2XAW",
    "Expiration" : "2017-06-09T09:17:19Z",
    "SecurityToken" : "CAIXXXXXXXXXXXwmBkleCTkyI+",
    "LastUpdated" : "2017-06-09T03:17:18Z",
    "Code" : "Success"
    }cess"
    }
    ```


## 步骤 4. 基于临时凭证，使用 Python SDK 访问 OSS { .section}

本示例中，我们基于 STS 临时凭证使用 Python SDK 列举实例所在地域的某个 OSS 存储空间（Bucket）里的 10 个文件。

 **前提条件** 

您已经远程连接到 ECS 实例。

您的 ECS 实例已经安装了 Python。如果您用的是 Linux ECS 实例，必须安装 pip。

您在实例所在的地域已经创建了存储空间（Bucket），并已经获取 Bucket 的名称和 Endpoint。本示例中，Bucket 名称为 `ramroletest`，Endpoint 为 `oss-cn-hangzhou.aliyuncs.com`。

 **操作步骤** 

按以下步骤使用 Python SDK 访问 OSS。

1.  运行命令 `pip install oss2`，安装 OSS Python SDK。
2.  执行下述命令进行测试，其中：

    -   `oss2.StsAuth` 中的 3 个参数分别对应于上述 URL 返回的 AccessKeyId、AccessKeySecret 和 SecurityToken。
    -   `oss2.Bucket` 中后 2 个参数是 Bucket 的名称和 Endpoint。
    ```
    import oss2
    from itertools import islice
    auth = oss2.StsAuth(<AccessKeyId>, <AccessKeySecret>, <SecurityToken>)
    bucket = oss2.Bucket(auth, <您的 Endpoint>, <您的 Bucket 名称>)
    for b in islice(oss2.ObjectIterator(bucket), 10):
      print(b.key).key)
    ```

    示例输出结果如下。

    ```
    [root@local ~]# python
    Python 2.7.5 (default, Nov  6 2016, 00:28:07)
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import oss2
    >>> from itertools import islice
    >>> auth = oss2.StsAuth("STS.J8XXXXXXXXXX4", "9PjfXXXXXXXXXBf2XAW", "CAIXXXXXXXXXXXwmBkleCTkyI+")
    >>> bucket = oss2.Bucket(auth, "oss-cn-hangzhou.aliyuncs.com", "ramroletest")
    >>> for b in islice(oss2.ObjectIterator(bucket), 10):
    ...     print(b.key)
    ...
    ramroletest.txt
    test.shh
    ```


