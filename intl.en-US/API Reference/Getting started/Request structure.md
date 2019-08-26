# Request structure {#RequestUrlStructure .concept}

This topic describes the request structure in GET requests and provides the endpoints of ECS. Alibaba Cloud ECS APIs allow you to initiate GET requests by sending a URL over the HTTP or HTTPS protocol. The request parameters must be included in the URL.

## Structure example {#section_htp_xvb_wdb .section}

The following example is an unencoded URL request of [CreateSnapshot](intl.en-US/API Reference/Snapshots/CreateSnapshot.md#).

``` {#codeblock_arf_c6f_sxr}
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-28m5zbua0
&<Common request parameters>
```

-   `https` indicates the communication protocol.

-   `ecs.aliyuncs.com` is an ECS service endpoint.

-   `Action=CreateSnapshot` indicates the target API, and `DiskId=`d-28m5zbua0`` is one of the [CreateSnapshot](intl.en-US/API Reference/Snapshots/CreateSnapshot.md#) parameters.

-   `<Common request parameters>` are the common parameters of the system.


## Communication protocol {#section_ltp_xvb_wdb .section}

Requests over HTTP or HTTPS are supported. We recommend that you send requests over HTTPS for a higher level of security.

If such sensitive information as an SSH key pair or a password exists in your request, we recommend that you choose HTTPS.

## Service endpoints {#section_mtp_xvb_wdb .section}

The following table describes the API service access endpoints of ECS. To reduce network latency, we recommend that you configure endpoints based on the source from which you call the service.

|Region \(Location\)|Endpoint|
|:------------------|:-------|
|Default|ecs.aliyuncs.com|
|China \(Zhangjiakou\)|ecs.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|ecs.cn-huhehaote.aliyuncs.com|
|Japan \(Tokyo\)|ecs.ap-northeast-1.aliyuncs.com|
|Australia \(Sydney\)|ecs.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ecs.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ecs.ap-southeast-5.aliyuncs.com|
|India \(Mumbai\)|ecs.ap-south-1.aliyuncs.com|
|UAE \(Dubai\)|ecs.me-east-1.aliyuncs.com|
|Germany \(Frankfurt\)|ecs.eu-central-1.aliyuncs.com|
|UK \(London\)|ecs.eu-west-1.aliyuncs.com|

The endpoints in the following table are accelerated through the virtual network and Express Connect. This reduces network latency that results from communication across different countries or regions.

|Region \(Location\)|Endpoint|
|:------------------|:-------|
|Default \(US Silicon Valley\)|ecs.us-west-1.aliyuncs.com|
|Default \(US Virginia\)|ecs.us-east-1.aliyuncs.com|
|Default \(China Hong Kong\)|ecs.cn-hongkong.aliyuncs.com|
|Default \(Singapore\)|ecs.ap-southeast-1.aliyuncs.com|

**Note:** The endpoints provided by Alibaba Cloud ECS can be used to send API calls over the Internet through HTTP or HTTPS. However, if your ECS instance is not assigned an Internet bandwidth package or a public IP address, the instance cannot initiate an API action request by using the Alibaba Cloud CLI or corresponding SDK. To resolve this issue, you can use PrivateZone to associate the VPC with the region to which your ECS instance belongs. For information about how to call API actions through an intranet for ECS instances in a VPC that cannot access the Internet, see [Call API actions from within an intranet environment](intl.en-US/API Reference/Appendix/Call API actions from within an intranet environment.md#).

## Request Parameters {#section_rtp_xvb_wdb .section}

You must specify the target operation \(for example, [Action=StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#)\) by using the `Action` parameter. Additionally, you must set other API parameters and [Common request parameters](intl.en-US/API Reference/Getting started/Common parameters.md#commonRequestParameters).

## Character encoding {#section_stp_xvb_wdb .section}

Request parameters and response parameters are encoded by using the`UTF-8` character set.

