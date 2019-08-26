# 为什么API、SDK和阿里云CLI只返回十条信息 {#EcsApiSeveralPageResults .reference}

在一些可能会返回许多响应信息的 API 中，为了更友好地展示信息，我们通常分页返回响应信息。当您忽略了隐藏信息时，会认为返回的数据不全。

## 原因分析 {#section_izy_qrg_ydb .section}

以查询镜像 API [DescribeImages](intl.zh-CN/API 参考/镜像/DescribeImages.md#) 为例，假设您查询华东 1（杭州）地域下可用的公共镜像。响应信息中 TotalCount 显示有 39 条，一般情况下，默认分 4 页展示响应信息。

若您希望一次性获取所有响应信息，可以在请求中加入 PageSize，设置为大于 39 的数。若您使用的是 Java SDK，可以在 Request 对象中通过 setPageSize 方法将 PageSize 设置为大于 39 的数值，一次性返回 39 个镜像的响应信息。

PageSize 和 PageNumber 的参数说明如下表所示：

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|PageNumber|Integer|否|查询接口返回资源信息列表的页码。ECS API 均以 `Describe` 作为查询接口前缀，更多详情，请参阅 [API 概览](intl.zh-CN/API 参考/API 概览.md#)。起始值：1。

默认值：1。

|
|PageSize|Integer|否|分页展示响应信息时设置的每页行数，单位：行。最大值：100。

默认值：10。

**说明：** PageSize 的最大值为 100，若查询的结果大于 100，您需要借助 PageNumber 获取后几页响应信息，即多次提交请求。每次设置 PageNumber 为1、2 和 3 等，以获取所有的响应信息。如果您使用的是 Java SDK，可以在请求中通过 setPageNumber\(\) 方法指定需要返回的页数。

|

## 默认显示状态的 Java SDK 示例 {#section_kmc_crg_ydb_2 .section}

以查询镜像 API [DescribeImages](intl.zh-CN/API 参考/镜像/DescribeImages.md#) 为例，PageSize 的默认值为 10。Java SDK 中若不设置 PageSize 的值，使用 getPageSize 返回的是 null，API 服务器会默认将 PageSize 设置为 10。以下为请求代码示例：

```
DescribeImagesRequest describe = **new** DescribeImagesRequest();
        //describe.setPageSize();//默认情况下不设置的话PageSize就是10
        describe.setRegionId("cn-hangzhou");
        describe.setImageOwnerAlias("system");
        System.out.println("当前请求的PageSize大小："+describe.getPageSize());
        DescribeImagesResponse response
                = client.getAcsResponse(describe);

        System.out.println("镜像总数："+response.getTotalCount());
        System.out.println("返回的响应中镜像数量="+response.getImages().size());

```

## 自定义显示状态的 Java SDK 示例 {#section_vs3_hzs_sfb .section}

以查询镜像 API [DescribeImages](intl.zh-CN/API 参考/镜像/DescribeImages.md#) 为例，假设会有 39 条返回信息。您可以使用 setPageSize 将 PageSize 设置为 50，一次性的返回所有镜像信息。以下为请求代码示例：

```
DescribeImagesRequest describe = **new** DescribeImagesRequest();
        describe.setPageSize(50);//这里在Request中通过setPageSize()方法将每页显示的数量设置为50
        describe.setRegionId("cn-hangzhou");
        describe.setImageOwnerAlias("system");
        System.out.println("当前请求的PageSize大小："+describe.getPageSize());
        **try** {
            DescribeImagesResponse response
                = client.getAcsResponse(describe);

            System.out.println("镜像总数："+response.getTotalCount());
            System.out.println("返回的响应中镜像数量="+response.getImages().size());

```

