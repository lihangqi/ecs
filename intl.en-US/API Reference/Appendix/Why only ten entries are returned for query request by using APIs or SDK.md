# Why only ten entries are returned for query request by using APIs or SDK {#EcsApiSeveralPageResults .reference}

For some APIs query request, where returns a large amount of information, the returned data is usually displayed in pages for readability. Take the DescribeImages as an example, if 39 entries are returned, the result is displayed on four pages by default, with 10 entries on each page. Thus, the returned data looks incomplete.

## Cause analysis {#section_izy_qrg_ydb .section}

For example, when you query the available official public images in the region of Asia Pacific SE 1 \(Singapore\) by [DescribeImages](intl.en-US/API Reference/Images/DescribeImages.md#), if 39 entries of data is returned, the result in TotalCount is split into four pages by default. You can add the parameter PageSize in your request, and set it to a value greater than 39. If Java SDK is used, PageSize can be set to a value greater than 39 by the setPageSize method in the Request object. Then the data about 39 images is returned once.

To display more data, you can add the PageSize and PageNumber parameters in your query request according to the following table.

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|PageNumber|Integer|No|Page number of the resource status list. Initial value: 1.Default value: 1.

|
|PageSize|Integer|No|Number of query entries on each page, configured during pagination query. Maximum value: 100.Default value: 10.

|

## Default display setting sample in Java SDK {#section_kmc_crg_ydb_2 .section}

By default, the value of PageSize is 10. If the value of PageSize is not added in a request, null is returned by getPageSize. The API server sets PageSize to 10 by default.

See the following Java SDK snippet for example:

```
DescribeImagesRequest describe = new DescribeImagesRequest();
        //describe.setPageSize(50);//By default value of PageSize is 10.
        describe.setRegionId("cn-hangzhou");
        describe.setImageOwnerAlias("system");
        System.out.println("PageSize of the current request:"+describe.getPageSize());
        DescribeImagesResponse response
                = client.getAcsResponse(describe);

        System.out.println("Total number of images:"+response.getTotalCount());
        System.out.println("Number of images in the returned response="+response.getImages().size());

```

## Customize the display setting in Java SDK {#section_hkf_f5s_sfb .section}

In this sample, we use the setPageSize\(\) method in Java SDK to PageSize to 50. Then, all images are returned at a time. 

See the following Java SDK snippet for example:

```
DescribeImagesRequest describe = new DescribeImagesRequest();
        describe.setPageSize(50);//Here in the Request, the value of PageSize is set to 50 by the setPageSize() method.
        describe.setRegionId("cn-hangzhou");
        describe.setImageOwnerAlias("system");
        System.out.println("PageSize of the current request:"+describe.getPageSize());
        try {
            DescribeImagesResponse response
                = client.getAcsResponse(describe);

            System.out.println("Total number of images:"+response.getTotalCount());
            System.out.println("Number of images in the returned response="+response.getImages().size());

```

**Note:** The maximum value of PageSize is 100. If the query result includes more than 100 entries of data, the data on the last few pages must be obtained by PageNumber, namely, multiple requests are submitted to obtain all the returned data, with PageNumber setting to 1, 2, 3…respectively. You can also specify the value of PageNumber in your request by setPageNumber\(\).

