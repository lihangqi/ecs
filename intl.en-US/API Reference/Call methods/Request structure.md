# Request structure {#RequestUrlStructure .concept}

GET requests by sending a URL over the HTTP or HTTPS protocol are allowed. The request parameters must be included in the request URL.

See the following unencoded URL of  [CreateSnapshot](intl.en-US/API Reference/Snapshots/CreateSnapshot.md#) as a request example.

```
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=1033-60053321
&<Common Request Parameters>
```

-   `https` specifies the communication protocol.

-   `ecs.aliyuncs.com` is one of the ECS service endpoints.

-   `Action=CreateSnapshot` specifies the target API, and `DiskId=1033-60053321`  is one of the [CreateSnapshot](intl.en-US/API Reference/Snapshots/CreateSnapshot.md#)  parameters.

-   `<Common Request Parameters>` are the headers, common parameters, and authentication parameters.


## Communication protocol {#section_ltp_xvb_wdb .section}

Request over HTTP or HTTPS is supported. We recommend that you send requests over HTTPS to enhance security.

Especially, when you invoke the SSH key pairs APIs, or password exists in your request, such as the parameter `Password` in the [CreateInstance](intl.en-US/API Reference/Instances/CreateInstance.md#)  operation, we recommend that you choose the HTTPS protocol.

## Service endpoints {#section_mtp_xvb_wdb .section}

See the following table for the API service access endpoints of ECS.

|Region \(Location\)|Endpoint|
|:------------------|:-------|
|Default|ecs.aliyuncs.com|
|China North 3 \(Zhangjiakou\)|ecs.cn-zhangjiakou.aliyuncs.com|
|China North 5 \(Hohhot\)|ecs.cn-huhehaote.aliyuncs.com|
|Asia Pacific NE 1 \(Tokyo\)|ecs.ap-northeast-1.aliyuncs.com|
|Asia Pacific SE 2 \(Sydney\)|ecs.ap-southeast-2.aliyuncs.com|
|Asia Pacific SE 3 \(Kuala Lumpur\)|ecs.ap-southeast-3.aliyuncs.com|
|Asia Pacific SE 5 \(Jakarta\)|ecs.ap-southeast-5.aliyuncs.com|
|Asia Pacific SOU 1 \(Mumbai\) |ecs.ap-south-1.aliyuncs.com|
|Middle East 1 \(Dubai\)|ecs.me-east-1.aliyuncs.com|
|Germany 1 \(Frankfurt\)|ecs.eu-central-1.aliyuncs.com|

Specifically, if you are from international regions, we recommend that you use the following central endpoints to avoid latency.

|Region \(Location\)|Endpoint|
|:------------------|:-------|
|Default \(**US West 1** Silicon Valley\)|ecs.us-west-1.aliyuncs.com|
|Default \(US East 1 Virginia\)|ecs.us-east-1.aliyuncs.com|
|Default \(Hong Kong\)|ecs.cn-hongkong.aliyuncs.com|
|Default \(Asia Pacific SE 1 Singapore\)|ecs.ap-southeast-1.aliyuncs.com|

## Request Parameters {#section_rtp_xvb_wdb .section}

You must specify the target API for each request by passing in the `Action` parameter. For example, [Action=StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#). Each URL must contain the [common request parameters](intl.en-US/API Reference/Call methods/Common parameters.md#commonRequestParameters) and the specific request parameters of the target operation.

## Character encoding {#section_stp_xvb_wdb .section}

Request parameters and response results are encoded by using the`UTF-8` character set.

