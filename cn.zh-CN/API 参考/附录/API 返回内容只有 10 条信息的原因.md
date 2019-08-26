# API 返回内容只有 10 条信息的原因 {#EcsApiSeveralPageResults .reference}

在一些可能会返回许多信息的 API 方法中，为了更好地展示信息，通常都会将需要返回的信息进行分页，如查询可用镜像，返回40条数据，默认情况下会将结果分为10条一页，总共会有4页，一次只会返回1页的信息，所以造成返回的数据不全，使用时可以通过 PageSize 和 PageNumber 来控制，这两个参数的说明如下：

|参数|类型|必需|描述|
|:-|:-|:-|:-|
|PageNumber|Integer|否|实例状态列表的页码，起始值为 1，默认值为 1|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值 100 行，默认值为 10|

例如查询镜像，查询杭州地域目前可用的官方公共镜像，查询结果中 TotalCount 显示有39条，那么结果将默认分成四页，若希望一次获取完，可以在请求中加入 PageSize，设置为大于39的数（若使用 Java SDK，可以在 Request 对象中通过 setPageSize 方法将 PageSize 设置为大于39的数值），这样请求后就可以一次返回39个镜像的数据了。

## 以下是 Java SDK 的演示： {#section_kmc_crg_ydb_2 .section}

默认情况下，PageSize 值为10（因为 Java SDK 若不设置 PageSize 的值，使用 getPageSize 返回的会是 null，API 服务器会默认将 PageSize 设置为10）：

代码片段如下：

```
DescribeImagesRequest describe = **new** DescribeImagesRequest();
        //describe.setPageSize(50);//默认情况下不设置的话PageSize就是10
        describe.setRegionId("cn-hangzhou");
        describe.setImageOwnerAlias("system");
        System.out.println("当前请求的PageSize大小："+describe.getPageSize());
        DescribeImagesResponse response
                = client.getAcsResponse(describe);

        System.out.println("镜像总数："+response.getTotalCount());
        System.out.println("返回的响应中镜像数量="+response.getImages().size());

```

使用 setPageSize 将 PageSize 值设置为50后，就可以一次性的返回所有镜像了：

代码片段如下：

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

**说明：** PageSize 的最大值为100，若查询的结果大于100，需要借助 PageNumber 来实现获取后几页的数据，即多次提交请求，每次设置 PageNumber 为1、2、3…，以获取所有的返回信息。可以在请求中通过 `setPageNumber()` 这个方法指定需要返回的页数。

