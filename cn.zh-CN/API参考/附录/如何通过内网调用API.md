# 如何通过内网调用API {#concept_226934 .concept}

本文通过配置云解析PrivateZone，为无公网访问能力的专有网络VPC类型ECS实例提供了通过阿里云内网调用API的方案。

## 背景信息 {#Context .section}

由于云服务器ECS提供的接入地址（Endpoint）为公网服务地址，当您的ECS实例没有分配公网带宽或者不存在公网IP地址时，无法使用阿里云CLI或者SDK等工具发起API请求。此时，您可以为ECS实例所在地域下的专有网络VPC关联云解析PrivateZone，即可实现在阿里云内网调用API。

## 使用说明 {#section_b26_sgt_s1a .section}

-   此方案仅适用于专有网络VPC类型ECS实例所在的地域，不支持跨地域配置云解析PrivateZone。
-   建议您使用已部署了阿里云CLI或者SDK的自定义镜像创建ECS实例，避免实例在无公网访问的条件下无法加载相关依赖。
-   目前，支持云解析PrivateZone的云服务器ECS接入地址（Endpoint）如下表所示，请确保您使用的Endpoint在列举范围内。

    |阿里云地域|地域ID|CNAME记录值|公网接入地址（Endpoint）|
    |-----|----|--------|----------------|
    |华北 2（北京）|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|ecs.cn-beijing.aliyuncs.com|
    |华东 1（杭州）|cn-hangzhou|popunify-vpc.cn-hangzhou.aliyuncs.com|ecs.cn-hangzhou.aliyuncs.com|
    |华东 2（上海）|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|ecs.cn-shanghai.aliyuncs.com|
    |华南 1（深圳）|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|ecs.cn-shenzhen.aliyuncs.com|
    |华北 5（呼和浩特）|cn-huhehaote|popunify-vpc.cn-huhehaote.aliyuncs.com|ecs.cn-huhehaote.aliyuncs.com|
    |华北 3（张家口）|cn-zhangjiakou|popunify-vpc.cn-zhangjiakou.aliyuncs.com|ecs.cn-zhangjiakou.aliyuncs.com|
    |中国（香港）|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|ecs.cn-hongkong.aliyuncs.com|
    |新加坡|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|ecs.ap-southeast-1.aliyuncs.com|
    |德国（法兰克福）|eu-central-1|popunify-vpc.eu-central-1.aliyuncs.com|ecs.eu-central-1.aliyuncs.com|


## 操作步骤 {#section_2ju_5zf_3md .section}

1.  登录[云解析控制台](https://dns.console.aliyun.com/#/dns/domainList)。
2.  在左侧导航栏中，单击**PrivateZone**。
3.  单击**添加Zone**。
4.  在添加 PrivateZone弹窗中，完成以下设置后，单击**确定**。

    -   **Zone名称**：设置一个已支持云解析PrivateZone的云服务器ECS接入地址，如ecs.cn-hangzhou.aliyuncs.com。
    -   **子域名递归解析代理**：勾选后，当DNS查询的域名以Zone名称为后缀，但是在Zone文件里未配置时，会以公网的权威解析为准。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618483246151_zh-CN.png)

5.  找到已创建的PrivateZone，在**操作**列，单击**解析设置**。
6.  在**解析设置**页面，单击**添加记录**。
7.  在添加记录弹窗中，完成以下设置后，单击**确定**。

    -   **记录类型**：选择CNAME。
    -   **主机记录**：填写@可以解析@.exmaple.com域名。
    -   **记录值**：设置为对应地域下的CNAME记录值。更多详情，请参见[使用说明章节](#)。
    -   **TTL值**：生存时间，本文选择了**1 分钟**。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618483246154_zh-CN.png)

8.  返回**云解析DNS** \> **PrivateZone**页面，找到已创建的PrivateZone，在**操作**列，单击**关联VPC**。
9.  在关联VPC弹窗中，选择与PrivateZone相同的地域，勾选实例所在的专有网络VPC，可多选，单击**确定**。

    **说明：** 请选择您的ECS实例所在的专有网络VPC。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618483246161_zh-CN.png)


## 执行结果 {#section_mzc_end_wml .section}

为专有网络VPC关联了云解析PrivateZone后，您可以通过[远程连接](../../../../intl.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)登录实例，在ECS实例内部测试是否能访问对应地域的接入地址。以ecs.cn-hangzhou.aliyuncs.com为例：

-   使用ping功能测试数据包收发状况。

    ``` {#codeblock_744_z6z_zhk}
    ping ecs.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618483346338_zh-CN.png)

-   使用阿里云CLI调用[DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#)，并通过--endpoint字段修改接入地址。

    ``` {#codeblock_g7i_i2p_t0q}
    aliyun ecs DescribeRegions --endpoint ecs.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618483346404_zh-CN.png)


