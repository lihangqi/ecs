# ESSD云盘 {#concept_727754 .concept}

阿里云ESSD（Enhanced SSD，增强型SSD）云盘结合25 GE网络和RDMA技术，为您提供单盘高达100万的随机读写能力和单路低时延性能。本文介绍了ESSD云盘的性能级别、适用场景及性能上限，提供了选择不同ESSD云盘性能级别时的参考信息。

## 应用场景 {#section_vvz_p9x_lkz .section}

ESSD云盘具备低时延、快速响应、强大的数据吞吐量的特点，适用于时延敏感的应用或者I/O密集型业务场景。例如：

-   典型的联机事务处理（Online Transaction Processing，OLTP）关系型数据库，如MySQL、PostgreSQL、Oracle、SQL Server等。
-   NoSQL非关系型数据库，如MongoDB、HBase、Cassandra等。
-   实时分析应用，如Elasticsearch分布式日志和ELK（Elasticsearch、Logstash、Kibana）日志分析等。

## 产品规格 {#section_bes_28i_nge .section}

ESSD云盘的API取值为cloud\_essd，提供了三个性能级别的云盘规格。有关如何压测ESSD云盘，请参见 *块存储FAQ* [如何压测ESSD云盘的性能](cn.zh-CN/块存储/块存储FAQ.md#ESSDperfor)。

|ESSD云盘属性|性能级别III|性能级别II|性能级别I|
|:-------|:------|:-----|:----|
|性能级别（Performance Level，简称PL）|PL3|PL2|PL1|
|云盘容量范围（GiB）|1,261~32,768|461~32,768|20~32,768|
|数据可靠性|99.9999999%|99.9999999%|99.9999999%|
|单盘最大IOPS（Input/Output Operations Per Second）|1,000,000|100,000|50,000|
|单盘最大吞吐量（MBps）|4,000|750|350|
|单盘性能计算公式|IOPS = min\{1800 + 50 \* 容量, 1000000\}|IOPS = min\{1800 + 50 \* 容量, 100000\}|IOPS = min\{1800 + 50 \* 容量, 50000\}|
|吞吐量 = min\{120 + 0.5 \* 容量, 4000\} MBps|吞吐量 = min\{120 + 0.5 \* 容量, 750\} MBps|吞吐量 = min\{120 + 0.5 \* 容量, 350\} MBps|

## 计费详情 {#section_fuh_hxa_vrh .section}

云服务器ECS支持创建按量付费和预付费两种计费方式的ESSD云盘。详情请参见[创建按量付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)和[创建预付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建预付费云盘.md#)。

有关不同ESSD云盘性能级别的定价详情，请参见[块存储定价](https://www.aliyun.com/price/product#/disk/detail)。

## 如何选择ESSD云盘性能级别 {#section_f4w_ye8_r2w .section}

三种性能级别的ESSD云盘单盘容量范围相同，均支持20 GiB-32,768 GiB的容量范围。三种性能级别核心差异在于单盘性能上限的不同。ESSD云盘可以作为系统盘和数据盘使用，以下建议适用于ESSD云盘作为数据盘的场景。

-   ESSD PL1适合对并发极限I/O性能要求中等，读写时延较为稳定的业务场景。

    适用于中小型MySQL和SQLServer等数据库场景，中小规模ELK日志集群，SAP和Oracle等企业级商用软件，容器应用。如果您一直使用的是SSD云盘或者高效云盘，可以优先选择ESSD PL1作为数据盘，承载类似的业务系统数据。

-   ESSD PL2适合对并发极限I/O性能要求较高，读写时延稳定的业务场景。

    适用于中等规模关系型数据库及NoSQL数据库，中等规模ELK日志集群，SAP和Oracle等企业级商用软件。如果您一直使用的是SSD云盘或者本地SSD实例规格（i1、i2、i2g），可以优先选择ESSD PL2作为数据盘，承载类似的业务系统数据。

-   ESSD PL3适合对并发极限I/O性能极高，读写时延极稳定的业务场景。

    适用于中大型核心业务关系型数据库及NoSQL数据库，大型SAP和Oracle系统等。如果您一直使用的是中高级规格（16核vCPU以上）本地SSD实例规格（i1、i2、i2g），可以优先选择ESSD PL3作为数据盘，承载类似的业务系统数据。


## 容量范围与性能级别的关系 {#singledisk .section}

对于存储设备而言，不同的容量能达到的性能不同，容量越大，存储设备的数据处理能力越强。所有ESSD云盘性能级别的单位容量的I/O性能均一致，但云盘性能随容量增长而线性增长，直至达到该性能级别的单盘性能上限。

|性能级别|ESSD云盘容量范围（GiB）|最大IOPS|最大吞吐量（MBps）|
|----|---------------|------|-----------|
|PL1|20~32,768|50,000|350|
|PL2|461~32,768|100,000|750|
|PL3|1,261~32,768|1,000,000|4,000|

-   示例一：张先生在ECS管理控制台上创建ESSD云盘时，选择了20 GiB。则张先生只能选购PL1性能级别的ESSD云盘，对应的IOPS上限为50,000。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/583241/156196366249959_zh-CN.png)

-   示例二：张先生在ECS管理控制台上创建ESSD云盘时，选择了32,000 GiB。则张先生能选购PL1至PL3性能级别的ESSD云盘，对应的IOPS上限分别为50,000、100,000和1,000,000。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/583241/156196366249960_zh-CN.png)


当您创建了ESSD云盘后，如果需要更高的云盘性能，可以通过扩容ESSD云盘实现。更多详情，请参见[扩容概述](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)。

## 实例规格与云盘性能的关系 {#section_oig_q2c_r56 .section}

部分ECS实例的存储I/O性能和实例规格成正比线性关系。云服务器ECS存储增强型实例g5se的存储I/O性能和实例规格成线性关系，实例规格越高可获得的存储IOPS和吞吐量越高。有关ECS实例的存储I/O性能数据，请参见[实例规格族](../../../../cn.zh-CN/实例/实例规格族.md#)。

实例规格与ESSD云盘性能的关系规则如下所示：

-   如果ESSD云盘的性能总和不超过实例规格族所对应的存储I/O能力，实际存储性能以ESSD云盘性能为准。
-   如果ESSD云盘的性能总和超过了实例规格族所对应的存储I/O能力，实际存储性能以该实例规格对应的存储I/O能力为准。

以下为两个示例：

-   示例一：张先生选择了ecs.g5se.xlarge 16 GiB规格实例，该实例规格最大存储I/O性能为60,000 IOPS。ECS实例仅挂载了一块1,800 GiB的ESSD云盘，单盘IOPS最大为100,000。则该ECS实例最大存储IOPS为60,000，无法达到100,000。
-   示例二：张先生选择了ecs.g5se.4xlarge 64 GiB规格实例，该实例规格最大存储I/O性能为230,000 IOPS。ECS实例仅挂载了一块1,800 GiB的ESSD云盘，单盘IOPS最大为100,000。则该ECS实例最大存储IOPS为100,000。

## 相关操作 {#section_po0_0oa_h77 .section}

-   [创建按量付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)
-   [创建预付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建预付费云盘.md#)
-   [使用快照创建云盘](cn.zh-CN/块存储/云盘/创建云盘/使用快照创建云盘.md#)
-   [挂载云盘](cn.zh-CN/块存储/云盘/挂载云盘.md#)
-   [转换云盘的计费方式](cn.zh-CN/块存储/云盘/转换云盘的计费方式.md#)
-   [扩容概述](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)

