# SDK使用方法和具体代码编写步骤 {#concept_34930_zh .concept}

新版 SDK 的文件名通常以 aliyun-XXXX-sdk 开头，后面跟上产品名称如 ECS，组成如 aliyun-java-sdk-ecs 的包名。其中有一个核心包 aliyun-java-sdk-core，其中封装了所有产品的 SDK 都会用到的一些类，如 IClientProfile 类、 IAcsClient 类、异常类等。产品相关的类均以产品为单位打包成不同名称的 Jar 包。

您需要准备好您的 AccessKey，用于输出到 [创建 Profile](#) 中。

## Java SDK 使用方法示例 { .section}

以 ECS Java SDK 查询可用镜像资源的方法 [DescribeImages](../../../../intl.zh-CN/API参考/镜像/DescribeImages.md#) 为例，介绍 SDK 使用的完整流程，其中 IClientProfile 和 IAcsClient 两个类包含在 aliyun-java-sdk-core 包中，其他的类均包含在 aliyun-java-sdk-ecs 包中。

1.  创建 Profile。生成 IClientProfile 的对象 profile，该对象存放 AccessKeyID 和 AccessKeySecret 和默认的地域信息，如示例中的 cn-hangzhou，更多关于地域的信息，参阅 [地域和可用区](../../../../intl.zh-CN/通用参考/地域和可用区.md#)。

    ```
    IClientProfile profile = DefaultProfile.getProfile("cn-hangzhou", ak,  aks); #ak 是您的 AccessKey，aks 是您的 AccessKeySecret
    ```

2.  创建 Client。从 IClientProfile 类中再生成 IAcsClient 的对象 client，后续获得 response 都需要从 IClientProfile 中获得。

    ```
    IAcsClient client = new DefaultAcsClient(profile);
    ```

3.  创建 Request。创建一个对应方法的 Request，类的命名规则一般为 API 的方法名加上 Request，如获得镜像列表的 API 方法名为 [DescribeImages](../../../../intl.zh-CN/API参考/镜像/DescribeImages.md#)，那么对应的请求类名就是 DescribeImagesRequest，直接使用构造函数生成一个默认的类 describe。

    ```
    DescribeImagesRequest describe = new DescribeImagesRequest();
    ```

4.  设置 Request 的参数。请求类生成好之后需要通过 Request 类的 setXxx 方法设置必要的信息，即 API 参数中必须要提供的信息，[DescribeImages](../../../../intl.zh-CN/API参考/镜像/DescribeImages.md#) 的 API 方法必须要提供的参数为 RegionId，该值可以省略，因为 IClientProfile 中已经提供了地域信息，同样的也可以通过 setXxx 方法设置其他可选的参数，如这里设置要查询的镜像为自定义镜像，则设置 ImageOwnerAlias 的值为 self，表示查询您的自定义镜像。

    ```
    describe.setImageOwnerAlias("self");
    ```

5.  参数设置完毕后，通过 IAcsClient 对象获得对应 Request 的响应。

    ```
    DescribeImagesResponse response = client.getAcsResponse(describe);
    ```

6.  在 Response 中获得返回的参数值。接着可以调用 response 中对应的 getXxx 方法获得返回的参数值了，如获得某个镜像的名字。根据 API 方法的不同，返回的信息中可能会包含多层的信息，如获得镜像列表这个方法，返回的信息中镜像是以一个集合来表示的，集合中存放了每个镜像的信息，对于 Java SDK 而言，那么存放镜像信息的就是一个列表，需要先通过 getImages\(\) 获得 Image 对象的集合，然后再通过遍历等方法取得其中某个镜像的信息，之后调用 getXxx 方法获得具体的信息。

    ```
    for(Image image:response.getImages())
                {
                    System.out.println(image.getImageId());
                    System.out.println(image.getImageName());
                }
    ```


至此，一个完整的调用就完成了。

## PHP SDK 注意事项 { .section}

使用 PHP SDK 和 Java SDK 的类似，可以归纳为：

1.  创建 Profile。
2.  创建 Client。
3.  创建 Request。
4.  设置 Request的参数。
5.  使用 Client 对应的方法传入 Request，获得 Response。
6.  在 Response 中获得返回的参数值。

## Python SDK 注意事项 { .section}

使用 Python SDK 省略了创建 Profile 这一步，直接创建 Client，然后执行后面的步骤即可。

## 参考信息 { .section}

-   关于 ECS 的所有 API，请参阅 [API 概览](../../../../intl.zh-CN/API参考/API 概览.md#)。

-   关于如何创建 AccessKey，请参阅 [创建 AccessKey](https://www.alibabacloud.com/help/doc-detail/53045.htm)。


