# 块存储FAQ {#concept_40551_zh .concept}

本文汇总了使用块存储时的常见问题。

-   ESSD云盘问题
    -   [什么是ESSD云盘？](#section_exq_8tt_oqw)
    -   [我什么时候可以购买ESSD云盘？](#section_hhd_okp_zlj)
    -   [相比于公测阶段，ESSD云盘商业化产品形态有什么不同？](#section_cw3_bmw_boh)
    -   [相比SSD云盘或者高效云盘，ESSD云盘有哪些异同？](#section_amv_05u_7k0)
    -   [ESSD云盘的性能指标与产品规格是如何计算的？](#section_tn9_l2d_g0h)
    -   [如何测试ESSD云盘的性能？如何测试出100万IOPS？](#section_guq_54c_14o)
    -   [ESSD云盘性能和实例性能有什么关系？](#section_l0c_cer_qu7)
    -   [ESSD云盘如何计费？](#section_6j1_ta3_nyy)
    -   [哪些地域或者可用区开放了ESSD云盘资源？](#section_yq8_9fo_zgu)
    -   [ESSD云盘能挂载到哪些实例规格族上？](#section_br8_0h3_7d6)
-   一般性问题
    -   [如何根据应用需求选择可用区？](#section_nks_1y2_gcr)
    -   [关于云盘的常用操作有哪些？](#section_xs4_pdh_fhb)
    -   [什么是I/O优化？我能将存量的ECS实例升级为I/O优化的实例吗？](#section_zxg_r7a_vdt)
-   性能测试问题
    -   [可以使用什么工具测试块存储性能？](#section_vyv_qlf_4rg)
    -   [为什么用FIO测试性能时，会导致实例宕机？](#section_gdt_ekx_3rp)
-   SSD云盘问题
    -   [SSD云盘具备怎样的I/O性能？](#section_f2w_rch_fhb)
    -   [SSD云盘适用于哪些应用场景？](#section_sf1_sch_fhb)
    -   [是否支持将原普通云盘更换成SSD云盘？](#section_z0c_kiu_c6o)
    -   [如何购买SSD云盘，I/O优化的实例及SSD云盘的价格是多少？](#section_gpx_xch_fhb)
    -   [购买SSD云盘后是否支持升级？](#section_n5t_cdh_fhb)
    -   [使用了I/O优化实例和SSD云盘之后，Linux系统在分区挂载的时候为什么报错？](#section_md2_ddh_fhb)
    -   [普通云盘和SSD云盘添加挂载信息时需要注意什么？](#section_vjf_tos_b2o)
-   共享块存储问题
    -   [什么是共享块存储？](#section_zjn_40o_nlh)
    -   [我什么时候可以购买共享块存储？](#section_idn_dlp_fhb)
    -   [共享块存储适用于哪些业务场景？](#section_xcn_dlp_fhb)
    -   [可以跨地域挂载共享块存储吗？](#section_adn_dlp_fhb)
    -   [一台实例上最多挂载多少块共享块存储？](#section_bdn_dlp_fhb)
    -   [共享块存储的产品规格和性能是什么？](#section_cdn_dlp_fhb)
    -   [如何测试共享块存储性能？](#section_frj_h4p_fhb)
-   挂载和卸载云盘问题
    -   [什么是设备名（挂载点）？](#section_c9t_aqp_8au)
    -   [什么是独立云盘？](#section_lth_2jp_fhb)
    -   [一块云盘可以挂载到多台ECS实例上吗？](#section_g5g_b2r_fhb)
    -   [购买了按量付费云盘并挂载到ECS实例后，还需要执行挂载分区的操作吗？](#section_gps_gpr_fhb)
    -   [为Linux实例购买了数据盘，但是系统中看不到怎么办？](#section_7hm_z6c_ttx)
    -   [一台实例能挂载多少块云盘？](#section_hl8_hn5_p3n)
    -   [为什么挂载云盘时找不到我想挂载的实例？](#section_ewk_3gr_fhb)
    -   [云盘和实例在不同的可用区，可以挂载吗？](#section_izt_uhb_fxk)
    -   [卸载云盘（数据盘）时，云盘数据会丢吗？](#section_xzy_pnk_by6)
    -   [系统盘能够卸载吗？](#section_2my_ijk_gy1)
-   独立云盘问题
    -   [单独购买的按量付费数据盘如何收费？](#section_v4m_b2r_fhb)
    -   [为什么我单独创建的云盘和我的实例一起释放了？](#section_bjw_8f4_ju1)
    -   [单独购买的按量付费数据盘能够挂载到预付费ECS实例上吗？](#section_xtp_b2r_fhb)
    -   [预付费ECS实例上的数据盘能卸载吗？](#section_tsb_3gr_fhb)
    -   [我已经操作过续费变配，在续费变配期内是否还能将预付费云盘转为按量付费云盘？](#section_nql_jnr_fhb)
-   云盘快照问题
    -   [删除云盘的时候，快照会被保留吗？](#section_a41_mgr_fhb)
    -   [为什么我的云盘没有自动快照了？](#section_jvf_shr_fhb)
    -   [可以使用快照单独创建云盘吗？](#section_tz3_jnr_fhb)
-   重新初始化云盘问题
    -   [数据盘挂载问题导致数据无法访问，应该如何排查？](#section_fz4_jnr_fhb)
    -   [重新初始化云盘时，我的快照会丢失吗？](#section_mx6_x6w_wn8)
    -   [重启Linux系统ECS实例或者重新初始化系统盘后数据盘不见了怎么办？](#section_eja_zx1_w6o)
    -   [Linux系统ECS实例重新初始化系统盘后如何重新挂载数据盘？](#section_vaw_x75_0rr)
-   扩容云盘问题
    -   [更换系统盘时，我的快照会丢失吗？](#section_2u6_pq5_q3f)
    -   [更换系统盘应该注意什么问题？](#section_pc0_x40_gh9)
    -   [如何扩容系统盘？](#section_wdn_d4r_fhb)
    -   [系统盘扩容之后是否支持再缩容？](#section_iiz_k8i_vkr)
    -   [所有块存储都支持系统盘扩容吗？有地域限制吗？](#section_cbz_pdh_fhb)
    -   [预付费和按量付费的ECS实例都支持扩容系统盘吗？](#section_tjd_xqr_fhb)
    -   [系统盘的容量范围是多少？最大能扩容到多少？](#section_nx3_xqr_fhb)
    -   [云服务器ECS续费变配后，不支持更换系统盘时指定系统盘容量吗？](#section_k1m_xqr_fhb)
    -   [如何利用快照创建云盘实现无损扩容数据盘？](#section_idx_soz_yoe)
    -   [为什么Linux系统ECS实例扩容云盘提示Bad magic number in super-block while trying to open /dev/xvdb1？](#section_td6_w72_q3x)
-   分区操作问题
    -   [数据盘能否再次划分出一个分区用作数据存储？](#section_ppz_43v_fhb)
    -   [划分了多个分区的云盘，创建的快照是针对单分区还是所有分区的的？](#section_q5b_p3v_fhb)
    -   [云盘二次分区有哪些注意事项？](#section_nx1_3mv_fhb)
    -   [写入数据与分区格式化有什么关系？](#section_rhr_eke_n2u)
-   回滚云盘问题
    -   [数据盘进行二次分区后，此时回滚快照后，数据盘是几个分区？](#section_nyd_3mv_fhb)
    -   [回滚云盘时为什么报错“执行回滚磁盘需要停止实例，并且确保当前磁盘没有创建中的快照和没有更换过操作系统。”？](#section_psz_3vy_ghb)
-   其他问题
    -   [如何跨ECS实例拷贝数据？](#section_i3j_nrv_fhb)
    -   [上一代云盘 - 本地SSD盘相关问题](#section_wfc_2jp_fhb)
    -   [如何压测ESSD云盘的性能？](#ESSDperfor)

## 什么是ESSD云盘？ {#section_exq_8tt_oqw .section}

ESSD云盘，又称增强型（Enhanced）SSD云盘，是阿里云推出的超高性能云盘产品。ESSD云盘结合25GE网络和RDMA技术，为您提供单盘高达100万的随机读写能力和更低的单路时延能力。更多详情，请参见[ESSD云盘](cn.zh-CN/块存储/云盘/ESSD云盘.md#)。

## 我什么时候可以购买ESSD云盘？ {#section_hhd_okp_zlj .section}

2018年7月14日，ESSD云盘开始公测，于2019年6月底正式商业化。您可以在[ECS管理控制台](https://ecs.console.aliyun.com)或者调用API [CreateDisk](../cn.zh-CN/API参考/块存储/CreateDisk.md#)创建ESSD云盘。

## 相比于公测阶段，ESSD云盘商业化产品形态有什么不同？ {#section_cw3_bmw_boh .section}

不同于公测期的产品形态，在正式商业化时，ESSD云盘按照性能上限不同，分为三种不同的规格。最新的ESSD云盘性能详情，请参见[ESSD云盘](cn.zh-CN/块存储/云盘/ESSD云盘.md#)。

对于存储设备而言，不同的容量能达到的性能不同，容量越大，存储设备的数据处理能力越强。所有ESSD云盘性能级别的单位容量的I/O性能均一致，但云盘性能随容量增长而线性增长，直至达到该性能级别的单盘性能上限。

|性能级别|ESSD云盘容量范围（GiB）|最大IOPS|最大吞吐量（MBps）|
|----|---------------|------|-----------|
|PL1|20~32,768|50,000|350|
|PL2|461~32,768|100,000|750|
|PL3|1,261~32,768|1,000,000|4,000|

## 相比SSD云盘或者高效云盘，ESSD云盘有哪些异同？ {#section_amv_05u_7k0 .section}

-   共同点：三种云盘都是基于分布式块存储架构的云盘类产品，具备高可靠和弹性扩容等特性，支持快照和加密等数据功能。
-   差异点：ESSD云盘的性能相比SSD云盘或者高效云盘都有大幅提升。详情请参见[ESSD云盘](cn.zh-CN/块存储/云盘/ESSD云盘.md#)和[块存储性能](cn.zh-CN/块存储/块存储性能.md#)。

## ESSD云盘的性能指标与产品规格是如何计算的？ {#section_tn9_l2d_g0h .section}

ESSD云盘的性能与容量线性相关，容量越大性能越高，相比SSD云盘有大幅的性能提升。更多详情，请参见[ESSD云盘](cn.zh-CN/块存储/云盘/ESSD云盘.md#)。

## 如何测试ESSD云盘的性能？如何测试出100万IOPS？ {#section_guq_54c_14o .section}

您可以通过FIO工具测试ESSD云盘性能，具体步骤请参见[如何压测ESSD云盘的性能](#)。

## ESSD云盘性能和实例性能有什么关系？ {#section_l0c_cer_qu7 .section}

部分实例维度的存储I/O性能和实例规格成正比线性关系。例如，云服务器ECS存储增强型实例g5se的存储I/O性能跟实例规格成线性关系，同一类型的实例规格等级越高可获得的存储IOPS和吞吐量越高。

当您创建某个规格的g5se实例并挂载ESSD云盘时：

-   如果ESSD云盘的性能总和不超过实例规格族所对应的存储I/O能力，实际存储性能以ESSD云盘性能为准。
-   如果ESSD云盘的性能总和超过了实例规格族所对应的存储I/O能力，实际存储性能以该实例规格对应的存储I/O能力为准。

    例如，当您创建了ecs.g5se.xlarge 16GiB规格实例后，该实例最大存储IOPS为6万。如果挂载了1块存储I/O能力为2TiB的ESSD云盘（单盘IOPS为101800），该实例最大存储IOPS只能为6万，而无法达到2TiB ESSD云盘的101800IOPS。


云服务器ECS存储增强型实例g5se的规格及性能见下表。

|实例规格|vCPU（核）|内存（GiB）|存储IOPS（万）|存储吞吐量（MBps）|
|:---|:------|:------|:--------|:----------|
|ecs.g5se.large|2|8|3|118|
|ecs.g5se.xlarge|4|16|6|235|
|ecs.g5se.2xlarge|8|32|12|470|
|ecs.g5se.4xlarge|16|64|23|900|
|ecs.g5se.6xlarge|24|96|34|1350|
|ecs.g5se.8xlarge|32|128|45|1800|
|ecs.g5se.16xlarge|64|256|90|3600|
|ecs.g5se.18xlarge|70|336|100|4000|

## ESSD云盘如何计费？ {#section_6j1_ta3_nyy .section}

支持预付费和按量付费。具体价格请参见[价格详情页](http://www.aliyun.com/price/product#/ecs/detail)。

## 哪些地域或者可用区开放了ESSD云盘资源？ {#section_yq8_9fo_zgu .section}

您可以在以下可用区申请购买ESSD云盘：

-   华东 1（杭州）可用区H、可用区I、可用区G
-   华东 2（上海）可用区E、可用区F、可用区G
-   华北 2（北京）可用区H、可用区G、可用区F
-   华北 3（张家口）可用区A、可用区B
-   华南 1（深圳）可用区E、可用区D
-   西南 1（成都）可用区A
-   香港可用区C
-   印度（孟买）可用区B
-   英国（伦敦）可用区B
-   澳大利亚（悉尼）可用区B

## ESSD云盘能挂载到哪些实例规格族上？ {#section_br8_0h3_7d6 .section}

ESSD云盘支持挂载到25GE网络的实例规格族（c5、ic5、g5、r5、g5se）、裸金属服务器实例规格族（ebmhfg5、ebmc4、ebmg5）和企业级异构计算规格族（vgn5i、gn6i、gn6v、gn5、gn5i、gn4、ga1、f1、f3），其他实例规格族暂不支持。

## 可以使用什么工具测试块存储性能？ {#section_vyv_qlf_4rg .section}

请参见[块存储性能](cn.zh-CN/块存储/块存储性能.md#)。

## 为什么用FIO测试性能时，会导致实例宕机？ {#section_gdt_ekx_3rp .section}

FIO测试工具支持裸盘分区、文件系统两种方式测试I/O性能。如果您直接测试裸盘分区，会破坏裸盘分区中的文件系统元数据，导致无法访问该裸盘分区中的文件，甚至导致实例宕机。使用FIO的文件系统测试性能方式时，不存在上述问题。

## 如何根据应用需求选择可用区？ {#section_nks_1y2_gcr .section}

按量付费的云盘只能挂载到同一可用区的ECS实例上。

-   针对高可用性应用，建议您在不同可用区中创建多块数据盘，并挂载到ECS实例上。
-   针对低网络延时应用，建议您在同一可用区中创建数据盘，并挂载到ECS实例上。

## 关于云盘的常用操作有哪些？ {#section_xs4_pdh_fhb .section}

关于云盘的常见操作，请参见以下文档：

-   [挂载云盘](cn.zh-CN/块存储/云盘/挂载云盘.md#)
-   [Linux格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)
-   [Windows格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Windows格式化数据盘.md#)
-   [卸载数据盘](cn.zh-CN/块存储/云盘/卸载数据盘.md#)
-   [重新初始化云盘](cn.zh-CN/块存储/云盘/重新初始化云盘/重新初始化系统盘.md#)
-   [更换系统盘（非公共镜像）](cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)
-   [更换系统盘（公共镜像）](cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（公共镜像）.md#)
-   [在线扩容云盘](cn.zh-CN/块存储/云盘/扩容云盘/在线扩容数据盘.md#)
-   [离线扩容云盘](cn.zh-CN/块存储/云盘/扩容云盘/离线扩容云盘.md#)
-   [扩展分区和文件系统\_Linux数据盘](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Linux数据盘.md#)
-   [扩展分区和文件系统\_Windows](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Windows.md#)

## 什么是I/O优化？我能将存量的ECS实例升级为I/O优化的实例吗？ {#section_zxg_r7a_vdt .section}

I/O优化为实例与云盘之间提供更好的网络能力，可保证SSD云盘存储性能的发挥。对于I/O优化的实例，挂载SSD云盘时能够获得SSD云盘的全部存储性能。

已购买的存量ECS实例支持通过[ModifyInstanceSpec](../cn.zh-CN/API参考/实例/ModifyInstanceSpec.md#)和[ModifyPrepayInstanceSpec](../cn.zh-CN/API参考/实例/ModifyPrepayInstanceSpec.md#)将非I/O优化的实例转换为I/O优化实例。

## SSD云盘具备怎样的I/O性能？ {#section_f2w_rch_fhb .section}

请参见[块存储性能](cn.zh-CN/块存储/块存储性能.md#)。

## SSD云盘适用于哪些应用场景？ {#section_sf1_sch_fhb .section}

SSD云盘具有高性能、高可靠性等特点，适合数据可靠性要求高的I/O密集型应用，如MySQL、SQL Server、Oracle、PostgreSQL等中小型关系数据库场景。同时适用对数据可靠性要求高的中小型开发测试环境。

## 是否支持将原普通云盘更换成SSD云盘？ {#section_z0c_kiu_c6o .section}

由于SSD云盘采用全SSD的存储介质实现，不支持将存量的普通云盘直接更换为SSD云盘。

## 如何购买SSD云盘，I/O优化的实例及SSD云盘的价格是多少？ {#section_gpx_xch_fhb .section}

请参见SSD云盘及I/O优化实例的[价格详情页](http://www.aliyun.com/price/product#/ecs/detail)。

## 购买SSD云盘后是否支持升级？ {#section_n5t_cdh_fhb .section}

支持升级和扩容。详情请参见[扩容概述](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)。

## 使用了I/O优化实例和SSD云盘之后，Linux系统在分区挂载的时候为什么报错？ {#section_md2_ddh_fhb .section}

SSD云盘在Linux系统内挂载点显示为/dev/vd\*，与常见的挂载点/dev/xvd\*有所区别。建议您按照/dev/vd\*挂载点格式填写挂载命令。

## 普通云盘和SSD云盘添加挂载信息时需要注意什么？ {#section_vjf_tos_b2o .section}

Linux系统添加数据盘时，在格式化数据盘编辑分区信息时，/dev/xvdb1是普通云盘的挂载点，如果您使用的是高效云盘、SSD云盘和ESSD云盘，挂载点为/dev/vdb1。如果添加了错误的信息，使用`mount -a`命令将无法挂载。解决方法如下：

1.  运行`fdisk -l`查看具体的数据盘信息。
2.  查看`/etc/fstab`里面添加的信息是否对应。

    **说明：** 不要重复添加挂载信息，否则会导致实例开机重复挂载，系统无法启动。

3.  使用vim修改`/etc/fstab`文件。
4.  将错误的信息注释或者删除，添加对应的挂载信息。
5.  运行`mount -a`测试是否能挂载成功。

常规的操作流程请参见[Linux格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)。

## 什么是共享块存储？ {#section_zjn_40o_nlh .section}

阿里云共享块存储是一种支持多台ECS实例并发读写访问的数据块级存储设备，具备多并发、高性能、高可靠等特性。更多详情，请参见[共享块存储](cn.zh-CN/块存储/共享块存储.md#)。

一块共享块存储可以同时挂载到同一地域中同一可用区的八台ECS实例。如果您需要同时挂载到更多ECS实例，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)申请。

## 我什么时候可以购买共享块存储？ {#section_idn_dlp_fhb .section}

共享块存储正处于免费邀测阶段。邀测期间，全地域均支持使用共享块存储。邀测结束后支持按量付费模式和预付费模式。

## 共享块存储适用于哪些业务场景？ {#section_xcn_dlp_fhb .section}

共享块存储专为企业级用户的核心业务而设计，打造高可用集群架构，适用于完全共享型（Shared-everything）数据库架构下对块存储设备的访问场景。例如，政府、企业和金融行业常用的高可用架构数据库集群Oracle RAC（Real Application Cluster）以及高可用架构服务器集群（High-availability cluster）。

## 可以跨地域挂载共享块存储吗？ {#section_adn_dlp_fhb .section}

不能。您只能将共享块存储挂载到同一地域、同一可用区的ECS实例上。

## 一台实例上最多挂载多少块共享块存储？ {#section_bdn_dlp_fhb .section}

作数据盘用时，共享块存储与云盘共享数据盘配额，即，一台实例上最多只能挂载16块数据盘。

## 共享块存储的产品规格和性能是什么？ {#section_cdn_dlp_fhb .section}

当前支持SSD共享块存储和高效共享块存储，具体规格和性能请参见[块存储性能](cn.zh-CN/块存储/块存储性能.md#)。

## 如何测试共享块存储性能？ {#section_frj_h4p_fhb .section}

您可以使用FIO工具进行性能压测。测试时，所有客户端的iodepth数值总计不能超过384。例如，四台ECS实例同时压测，建议每个客户端iodepth不能超过96。

-   两台ECS实例参与压测时：
    -   测试随机写IOPS

        ``` {#codeblock_di6_gcy_9vw}
        FIO -direct=1 -iodepth=128 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
        ```

    -   测试随机读IOPS

        ``` {#codeblock_75c_f9v_e9r}
        FIO -direct=1 -iodepth=128 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
        ```

    -   测试写吞吐量

        ``` {#codeblock_36h_qyz_h0p}
        FIO -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=64k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
        ```

    -   测试读吞吐量

        ``` {#codeblock_dlp_2bd_28t}
        FIO -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=64k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
        ```

-   四台ECS实例参与压测时：
    -   测试随机写IOPS

        ``` {#codeblock_oid_2cn_f0i}
        FIO -direct=1 -iodepth=96 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
        ```

    -   测试随机读IOPS

        ``` {#codeblock_lbc_tiv_l7e}
        FIO -direct=1 -iodepth=96 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
        ```

    -   测试写吞吐量

        ``` {#codeblock_fyz_ar7_4wq}
        FIO -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=64k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
        ```

    -   测试读吞吐量

        ``` {#codeblock_o2r_hh2_13m}
        FIO -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=64k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
        ```


## 什么是设备名（挂载点）？ {#section_c9t_aqp_8au .section}

设备名（挂载点）是云服务器ECS上云盘在磁盘控制器总线上的位置。所选配的设备名，在Linux操作系统下与磁盘设备号对应，在Windows操作系统下与磁盘管理器中的磁盘顺序一致。

## 什么是独立云盘？ {#section_lth_2jp_fhb .section}

独立云盘，即单独购买的按量付费数据盘，而不是随实例创建的数据盘。它可以在同一个可用区内的不同ECS实例之间自由挂载和卸载，但不能跨地域、跨可用区挂载。独立云盘必须挂载到实例上，并分区格式化，才能使用。详情请参见[创建按量付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)。

## 一块云盘可以挂载到多台ECS实例上吗？ {#section_g5g_b2r_fhb .section}

不能。一块数据盘只能挂载到同一可用区的一台实例，不支持跨可用区挂载。

## 购买了按量付费云盘并挂载到ECS实例后，还需要执行挂载分区的操作吗？ {#section_gps_gpr_fhb .section}

单独购买了按量付费数据盘之后，你需要将该数据盘挂载到实例上，并分区格式化。详情请参见[Linux格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)和[Windows格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Windows格式化数据盘.md#)。

## 为Linux实例购买了数据盘，但是系统中看不到怎么办？ {#section_7hm_z6c_ttx .section}

如果是单独购买的按量付费数据盘，您需要分区格式化、挂载后才能使用和看到空间。详情请参见[Linux格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)和[挂载云盘](cn.zh-CN/块存储/云盘/挂载云盘.md#)。

## 一台实例能挂载多少块云盘？ {#section_hl8_hn5_p3n .section}

作数据盘用时，云盘与共享块存储共享数据盘配额，即一台实例最多挂载16块数据盘。

## 为什么挂载云盘时找不到我想挂载的实例？ {#section_ewk_3gr_fhb .section}

请确保确保您的实例没有被释放，并且实例和云盘处于同一个地域的同一个可用区。

## 云盘和实例在不同的可用区，可以挂载吗？ {#section_izt_uhb_fxk .section}

不可以。您只能在同一可用区内的不同ECS实例间自由挂载和卸载按量付费云盘。

## 卸载云盘（数据盘）时，云盘数据会丢吗？ {#section_xzy_pnk_by6 .section}

-   在Windows操作系统下，为了保证数据完整性，强烈建议您暂停对该云盘的所有文件系统的读写操作，否则未完成读写的数据会丢失。
-   在Linux操作系统下，您需要登录实例中对该云盘执行umount命令，命令执行成功后再进入控制台卸载云盘。

## 系统盘能够卸载吗？ {#section_2my_ijk_gy1 .section}

不能卸载系统盘，但您可以更换系统盘。详情请参见[更换系统盘（非公共镜像）](cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

## 单独购买的按量付费数据盘如何收费？ {#section_v4m_b2r_fhb .section}

按量付费数据盘按小时为计费单位出账，如果您的账号余额不足，按量付费数据盘的服务会被停止。

## 为什么我单独创建的云盘和我的实例一起释放了？ {#section_bjw_8f4_ju1 .section}

单独创建了数据盘后，在挂载时可以选择该云盘是否随实例释放。您可以随时通过控制台或API更改这个选项。详情请参见[挂载云盘](cn.zh-CN/块存储/云盘/挂载云盘.md#)。

## 单独购买的按量付费数据盘能够挂载到预付费ECS实例上吗？ {#section_xtp_b2r_fhb .section}

可以。

## 预付费ECS实例上的数据盘能卸载吗？ {#section_tsb_3gr_fhb .section}

预付费ECS实例不支持直接卸载数据盘。数据盘到期时间和实例一致，随实例一起释放。如果想要释放数据盘，您可以先将预付费数据盘转换为按量付费数据盘，再卸载并释放数据盘。如何转换云盘的计费方式，请参见[转换云盘的计费方式](cn.zh-CN/块存储/云盘/转换云盘的计费方式.md#)。

## 我已经操作过续费变配，在续费变配期内是否还能将预付费云盘转为按量付费云盘？ {#section_nql_jnr_fhb .section}

不能。您可以等到续费变配期结束后，再选择续费变配，转化为按量付费云盘。

## 删除云盘的时候，快照会被保留吗？ {#section_a41_mgr_fhb .section}

手动快照不会被删除。自动快照是否会被删除，取决于您是否设置了**自动快照随磁盘释放**。详情请参见[设置自动快照随云盘释放](../cn.zh-CN/快照/使用自动快照策略/设置自动快照随云盘释放.md#)。

## 为什么我的云盘没有自动快照了？ {#section_jvf_shr_fhb .section}

快照数量达到快照额度上限后，系统会自动删除最早创建的自动快照，手动快照不受影响。

**说明：** 云盘只有挂载到实例时才会执行自动快照策略。

## 可以使用快照单独创建云盘吗？ {#section_tz3_jnr_fhb .section}

可以。在单独创建按量付费云盘时，选择已有的快照创建即可。详情请参见[使用快照创建云盘](cn.zh-CN/块存储/云盘/创建云盘/使用快照创建云盘.md#)。

## 数据盘挂载问题导致数据无法访问，应该如何排查？ {#section_fz4_jnr_fhb .section}

如果无法访问Linux数据盘的数据，您可以参考以下排查思路。

1.  找到数据所在的云盘，并确认数据盘是否挂载在对应的ECS实例。
    -   在控制台查看。详情请参见[查看云盘监控信息](cn.zh-CN/块存储/云盘/查看云盘监控信息.md#)。
    -   在实例内部，使用`fdisk -l`命令查看数据盘的分区信息是否正常，并使用`df -h`和`mount | grep "<devpath>"`命令查看挂载情况。
2.  用cat命令查看/etc/fstab文件，是否将两块云盘挂载到同一目录。
    -   如果挂载在同一目录，先挂载的云盘会被后挂载的云盘替换，导致数据无法访问。建议将其中一块云盘挂载到另外一个目录下。
    -   如果没有挂载在同一个目录下，但挂载信息仍显示在同一目录，使用ll命令查看挂载的两个目录是否存在连接。如果存在连接，建议用mkdir命令新建一个目录挂载，并测试能否访问数据。

## 重启Linux系统ECS实例后数据丢失怎么办？ {#section_xyy_bb8_gma .section}

-   问题现象： 重启实例后发现某一目录（例如/alidata）所有数据丢失。
-   问题原因： 运行`df -h`查看，发现没有挂载数据盘分区。
-   解决方法： 本方法以I/O优化实例为例。如果是非I/O优化实例，云盘分区格式为/dev/xvd\*1，请您根据实际情况操作。
    1.  运行`fdisk -l`命令查看未挂载的数据盘分区。
    2.  运行`mount /dev/vdb1 /alidata`挂载数据盘分区。
    3.  运行`df -h`查看是否成功挂载数据盘分区。
    4.  （可选）在/etc/fstab中设置开机自动挂载，避免下次出现同样问题。

## 重新初始化云盘时，我的快照会丢失吗？ {#section_mx6_x6w_wn8 .section}

不会，手动快照和自动快照都不会丢失。

## 重启Linux系统ECS实例或者重新初始化系统盘后数据盘不见了怎么办？ {#section_eja_zx1_w6o .section}

-   问题现象：Linux实例重启或初始化系统之后，再登录实例运行`df -h`查看云盘挂载，发现数据不见了。
-   问题原因：
    -   重启实例：如果重启实例前，您没有将挂载信息写入到/etc/fstab中，重启实例之后实例不会自动挂载数据盘。
    -   重新初始化系统盘：初始化系统盘会重置/etc/fstab文件，重新初始化系统盘后实例不会自动挂载数据盘。
-   解决方案：
    1.  运行`mount /dev/xvdb1`命令重新挂载数据盘。
    2.  运行mount命令查看数据盘分区/dev/xvdb1的文件格式。
    3.  假设您查看到/dev/xvdb1分区使用的是ext3文件系统，执行以下命令将数据盘挂载信息写入到/etc/fstab文件中。

        ``` {#codeblock_vhi_ujh_2b9}
        echo '/dev/xvdb1 /data ext3 defaults 0 0' >> /etc/fstab
        ```

    4.  在控制台重启ECS实例。

## Linux系统ECS实例重新初始化系统盘后如何重新挂载数据盘？ {#section_vaw_x75_0rr .section}

在Linux实例中，重新初始化系统盘不会改变数据盘里的内容，但是数据盘的挂载信息会丢失。假设重新初始化系统盘之前，实例上挂载的数据盘分区名称为/dev/vdb1，挂载点名称为/InitTest。重启Linux实例后，请参见以下步骤创建新的挂载点信息并挂载数据盘分区。

1.  运行`mount`查看数据盘挂载信息。

    返回结果中没有/dev/vdb1的信息。

2.  运行`fdisk -l`查看数据盘分区信息。
3.  运行`cat /etc/fstab`查看数据盘分区/dev/vdb1原有的挂载点名称。
4.  运行`mkdir /InitTest`重新创建数据盘分区的挂载点。

    新建的挂载点名称必须与重新初始化系统盘之前/dev/vdb1的挂载点名称保持一致。

5.  运行`mount /dev/vdb1 /InitTest`重新挂载数据盘分区。
6.  运行`df -h`查看挂载结果。
7.  按以下步骤检测数据盘/dev/vdb1是否能自动挂载。
    1.  运行`umount /dev/vdb1`卸载/dev/vdb1。
    2.  运行`mount`查看挂载信息。

        如果卸载成功，返回结果中不会有/dev/vdb1的信息。

    3.  运行`mount -a`自动挂载/dev/vdb1。
    4.  运行`mount`查看挂载信息。

        如果自动挂载成功，返回结果中会有/dev/vdb1的信息。


## 更换系统盘时，我的快照会丢失吗？ {#section_2u6_pq5_q3f .section}

历史系统盘的手动快照仍旧保留，如果自动快照设置了自动快照随磁盘释放则会被删除。

**说明：** 更换系统盘后云盘ID会发生变化，历史系统盘的快照将不能用于回滚新的系统盘。

## 更换系统盘应该注意什么问题？ {#section_pc0_x40_gh9 .section}

更换系统盘之前建议您创建快照备份数据，并且您需要确保系统盘有1GiB以上的预留空间。否则更换系统盘后，实例可能无法正常启动。

系统盘价格请参见[云服务器ECS详细价格总览](https://www.aliyun.com/price/product#/ecs/detail)。

## 如何扩容系统盘？ {#section_wdn_d4r_fhb .section}

您可以通过控制台或者调用[ResizeDisk](../cn.zh-CN/API参考/块存储/ResizeDisk.md#)扩容系统盘。

## 系统盘扩容之后是否支持再缩容？ {#section_iiz_k8i_vkr .section}

不支持。建议您合理选择扩容范围。

## 所有块存储都支持系统盘扩容吗？有地域限制吗？ {#section_cbz_pdh_fhb .section}

高效云盘、SSD云盘、ESSD云盘支持系统盘扩容。所有的地域都支持扩容系统盘。

## 预付费和按量付费的ECS实例都支持扩容系统盘吗？ {#section_tjd_xqr_fhb .section}

预付费和按量付费的ECS实例都支持扩容系统盘。

## 系统盘的容量范围是多少？最大能扩容到多少？ {#section_nx3_xqr_fhb .section}

容量范围随实例使用的镜像变化。详情请参见[扩容概述](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)。

## 云服务器ECS续费变配后，不支持更换系统盘时指定系统盘容量吗？ {#section_k1m_xqr_fhb .section}

预付费ECS实例完成[续费降配](../cn.zh-CN/产品定价/续费实例/续费降配.md#)操作后，只有进入新计费周期后才能扩容系统盘，当前计费周期内不支持扩容系统盘。

## 如何利用快照创建云盘实现无损扩容数据盘？ {#section_idx_soz_yoe .section}

在扩容数据盘时，若遇到云盘原因导致无法无损地扩容时，您可以临时新建一块按量付费云盘存放数据，然后彻底格式化数据盘。请参见以下步骤。

1.  为当源数据盘创建快照。详情请参见[创建快照](../cn.zh-CN/快照/使用快照/创建快照.md#)。
2.  前往[云盘购买页](https://ecs-buy.aliyun.com/#/clouddisk)，选择和ECS实例相同的地域及可用区，并选择**用快照创建磁盘**，选择上一步生成的快照。
3.  在ECS控制台，将新建数据盘挂载到同一台ECS实例上。
4.  登录ECS实例，运行mount命令挂载新建云盘。有关如何挂载根据快照创建的云盘，请参见[使用快照创建云盘](cn.zh-CN/块存储/云盘/创建云盘/使用快照创建云盘.md#)。
5.  抽检查看新建数据盘中的文件是否和源数据盘一致。
6.  确认数据一致后，使用fdisk删除原有的分区表，然后再使用fdisk、mkfs.ext3等命令重新对数据盘执行分区格式化操作，使新建数据盘的可用空间变为扩容之后的大小。详情请参见[扩展分区和文件系统\_Linux数据盘](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Linux数据盘.md#)。
7.  运行cp -R命令将新建数据盘中的数据全部拷回源数据盘。

    您可以加上--preserve=all参数，保留文件的属性。

8.  运行umount命令卸载新建数据盘。
9.  在ECS控制台从实例上卸载并释放新建数据盘。

## 为什么Linux系统ECS实例扩容云盘提示Bad magic number in super-block while trying to open /dev/xvdb1？ {#section_td6_w72_q3x .section}

-   问题现象：`e2fsck -f /dev/xvdb`扩容格式化云盘时提示报错Bad magic number in super-block while trying to open /dev/xvdb1
-   问题原因：可能是由于没有云盘分区导致。
-   解决方案：分别运行`e2fsck -f /dev/xvdb`和`resize2fs /dev/xvdb`实现扩容。然后使用mount命令挂载云盘。

## 数据盘能否再次划分出一个分区用作数据存储？ {#section_ppz_43v_fhb .section}

支持。您可以根据需求对数据盘划分多个分区，建议您使用系统自带的工具进行分区操作。

## 划分了多个分区的云盘，创建的快照是针对单分区还是所有分区的的？ {#section_q5b_p3v_fhb .section}

所有分区。快照备份了整块云盘的数据，而不是该云盘的某几个分区。

## 云盘二次分区有哪些注意事项？ {#section_nx1_3mv_fhb .section}

出于数据安全考虑，您需要提前创建快照备份云盘数据，发生操作失误时可以及时回滚云盘。详情请参见[创建快照](../cn.zh-CN/快照/使用快照/创建快照.md#)和[使用快照回滚云盘](../cn.zh-CN/快照/使用快照/使用快照回滚云盘.md#)。

## 写入数据与分区格式化有什么关系？ {#section_rhr_eke_n2u .section}

一块新云盘或新云盘分区在正常使用前，必须经过初始化，并将数据结构记录到云盘上。格式化的目的是建立文件系统。因此，在云盘上建立文件系统意味着对云盘有写入数据操作。不同的文件系统在格式化时写入的文件大小不同：

-   Windows系统格式化（分为快速和正常格式化）：
    -   快速格式化：只是为分区分配文件系统，并重写目录表。快速格式化占用的实际空间相对较少。
    -   正常格式化：不但完成快速格式化工作，还逐扇区扫描分区以确定和标记坏扇区，填充云盘空块，相当于写了云盘全盘的数据量。此时，第一份全量快照会近似于云盘容量。
-   Linux系统格式化：格式化云盘后，在实例没有写入业务数据前，第一份快照的容量大小与云盘文件系统格式有关。

## 数据盘进行二次分区后，此时回滚快照后，数据盘是几个分区？ {#section_nyd_3mv_fhb .section}

快照回滚是回滚到快照时间点，如果该时间点尚未进行二次分区，则没有多个分区。

## 回滚云盘时为什么报错“执行回滚磁盘需要停止实例，并且确保当前磁盘没有创建中的快照和没有更换过操作系统。”？ {#section_psz_3vy_ghb .section}

-   问题现象：回滚云盘时，报错“执行回滚云盘需要停止实例，并且确保当前云盘没有创建中的快照和没有更换过操作系统。”
-   问题原因：通常是由于云盘属性或云盘状态不符等原因导致。
-   解决方案：您可以根据实例状态和相关快照任务排查故障。
    -   检查实例是否已经正常停止。

        只有已停止的实例才能进行云盘回滚操作。您可以在控制台的实例列表页查看实例状态。

    -   检查相关快照所关联的实例是否更换过系统盘。

        如果更换了操作系统，实例的系统盘会随新镜像自动重新创建，系统盘ID会改变。所以，实例原有的快照将无法再用于回滚。但您可以基于相关快照创建自定义镜像，然后再通过更换系统盘方式指定该自定义镜像，将实例切换到相应的快照状态。详情请参见[使用快照创建自定义镜像](../cn.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)和[更换系统盘（非公共镜像）](cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

    -   检查相关快照归属的云盘是否有正在创建快照。

        为保障数据一致性，如果快照归属云盘有正在进行的快照任务，将不允许进行回滚操作。您可以在实例详情页的**本实例快照**中，查看是否存在**进度**不是**100%**，**状态**处于**未完成**的快照任务。

        如果您需要强制终止相关快照任务以便尽快进行云盘回滚操作，可以勾选相应快照，并单击**删除快照**终止快照任务。


## 如何跨ECS实例拷贝数据？ {#section_i3j_nrv_fhb .section}

根据不同的操作系统，您可以参考以下方法跨ECS实例拷贝数据：

-   Linux实例之间数据拷贝
    -   lrzsz方式

        登录实例，安装lrzsz，然后执行rz上传，sz下载。

        您也可以先用sz下载到本地，再rz上传到另一台实例上。

    -   FTP方式

        使用sftp工具，建议用root账号登录进行下载和上传。

    -   wget命令

        把文件或者文件夹压缩后，放在web目录下生成一个下载URL，在另一台实例上用wget命令进行下载 。

-   Linux与Windows之间数据拷贝

    建议在Linux实例上使用sftp，先下载到本地，然后使用FTP上传到Windows实例。

-   Windows之间数据拷贝
    -   使用FTP的方式

        Windows安装FTP服务的教程请[点此查看](https://help.aliyun.com/knowledge_detail/7600192.html)。

    -   两台实例都登录阿里旺旺进行传输

## 上一代云盘 - 本地SSD盘相关问题 {#section_wfc_2jp_fhb .section}

本地SSD盘已经停止售卖。如果您仍在使用本地SSD盘，请参见[本地SSD盘介绍](https://help.aliyun.com/knowledge_detail/35241.html)和[本地SSD盘FAQ](https://help.aliyun.com/knowledge_detail/40547.html)。

## 如何压测ESSD云盘的性能？ {#ESSDperfor .section}

由于压测云盘的性能时，云盘本身以及压测条件都起着重要的作用，因此本文提供了如何配置合适的条件压测ESSD云盘性能的示例，并测试出100万IOPS。为了充分发挥出多核多并发的系统性能，压测出100万IOPS性能指标，您可以参考以下建议测试ESSD云盘的性能。

**警告：** 测试裸盘可以获得真实的块存储盘性能，但直接测试裸盘会破坏文件系统结构，请在测试前提前[创建快照](../cn.zh-CN/快照/使用快照/创建快照.md#)做好数据备份。建议您只在新购无数据的ECS实例上使用工具测试块存储性能，避免造成数据丢失。

镜像：您可以使用阿里云官方镜像中高版本的Linux镜像版本。例如，CentOS 7.4/7.3/7.2 64位和AliyunLinux 17.1 64位操作系统。由于对应的驱动还不够完善，不推荐使用其他低版本的Linux镜像和Windows镜像。

工具：您可以使用[FIO](https://linux.die.net/man/1/fio)作为云盘性能标准的测试工具。

以实例规格ecs.g5se.18xlarge为例，同时ESSD云盘的设备名为/dev/vdb，示范通过随机写（randwrite）测试ESSD云盘的性能。

1.  远程连接Linux实例。
2.  运行以下命令安装libaio和FIO。

    ``` {#codeblock_244_8wb_x30}
    sudo yum install libaio –y
    sudo yum install libaio-devel –y
    sudo yum install fio -y
    ```

3.  运行`cd /tmp`切换路径。
4.  运行`vim test100w.sh`新建脚本文件，并粘贴以下内容，脚本为随机写randwrite IOPS性能测试示例。

    ``` {#test100w.sh}
    function RunFio
    {
     numjobs=$1  # 实例中的测试线程数，如示例中的8
     iodepth=$2  # 同时发出I/O数的上限，如示例中的64
     bs=$3       # 单次I/O的块文件大小，如示例中的4K
     rw=$4       # 测试时的读写策略，如示例中的randwrite
     filename=$5 # 指定测试文件的名称，如示例中的/dev/vdb
     nr_cpus=`cat /proc/cpuinfo |grep "processor" |wc -l`
     if [ $nr_cpus -lt $numjobs ];then
         echo “Numjobs is more than cpu cores, exit!”
         exit -1
     fi
     let nu=$numjobs+1
     cpulist=""
     for ((i=1;i<10;i++))
     do
         list=`cat /sys/block/vdb/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','`
         if [ -z $list ];then
             break
         fi
         cpulist=${cpulist}${list}
     done
     spincpu=`echo $cpulist | cut -d ',' -f 2-${nu}`
     echo $spincpu
     fio --ioengine=libaio --runtime=30s --numjobs=${numjobs} --iodepth=${iodepth} --bs=${bs} --rw=${rw} --filename=${filename} --time_based=1 --direct=1 --name=test --group_reporting --cpus_allowed=$spincpu --cpus_allowed_policy=split
    }
    echo 2 > /sys/block/vdb/queue/rq_affinity
    sleep 5
    RunFio 8 64 4k randwrite /dev/vdb
    ```

    **说明：** 

    -   因测试环境而异，脚本中您需要修改的命令行有：
        -   命令行`list=`cat /sys/block/vdb/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','``中的vdb。
        -   命令行`RunFio 8 64 4k randwrite /dev/vdb`中的8、64、4k、randwrite和/dev/vdb。
    -   直接测试裸盘会破坏文件系统结构。如果云盘上的数据丢失不影响业务，可以设置`filename=[设备名，如本示例中的/dev/vdb]`。否则，请设置为`filename=[具体的文件路径，比如/mnt/test.image]`。
5.  运行`sh test100w.sh`开始测试ESSD云盘性能。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10111/156575839842181_zh-CN.png)


脚本解读：

-   块设备参数

    测试实例时，[脚本](#)中的命令`echo 2 > /sys/block/vdb/queue/rq_affinity`是将ECS实例中的块设备中的参数`rq_affinity`值修改为2：

    -   参数`rq_affinity`的值为1时，表示块设备收到I/O完成（I/O Completion）的事件时，这个I/O被发送回处理这个I/O下发流程的vCPU所在Group上处理。在多线程并发的情况下，I/O Completion就可能集中在某一个vCPU上执行，这样会造成瓶颈，导致性能无法提升。
    -   参数`rq_affinity`的值为2时，表示块设备收到I/O Completion的事件时，这个I/O会在当初下发的vCPU上执行。在多线程并发的情况下，就可以完全充分发挥各个vCPU的性能。
-   绑定对应的vCPU
    -   普通模式下，一个设备（Device）只有一个请求列表（Request-Queue）。在多线程并发处理I/O的情况下，这个唯一的Request-Queue就是一个性能瓶颈点。
    -   最新的多队列（Multi-Queue）模式下，一个设备（Device）可以拥有多个处理I/O的Request-Queue，可以充分发挥后端存储的性能。如果您有4个I/O线程，您需要将4个线程分别绑定在不同的Request-Queue对应的CPU Core上，这样就可以充分利用Multi-Queue提升性能。

为了充分发挥设备（Device）的性能，需要将I/O线程分发到不同的Request-Queue上处理。[脚本](#)中通过以下命令，分别将几个`jobs`绑定不同的CPU Core上，其中`vd`为您的云盘设备名，例如，/dev/vdb。

``` {#codeblock_ftc_f8g_hwu}
fio —ioengine=libaio —runtime=30s —numjobs=${numjobs} —iodepth=${iodepth} —bs=${bs} —rw=${rw} —filename=${filename} —time_based=1 —direct=1 —name=test —group_reporting —cpus_allowed=$spincpu —cpus_allowed_policy=split
```

FIO提供了参数`cpusallowed`以及`cpus_allowed_policy`来绑定vCPU。以上命令一共运行了几个`jobs`，分别绑定在几个CPU Core上，分别对应着不同的Queue\_Id。

关于如何查看Queue\_Id绑定的cpu\_core\_id，您可以：

-   运行`ls /sys/block/vd/mq/`查看设备名为vd云盘的Queue\_Id，例如vdb。
-   运行`cat /sys/block/vd/mq//cpu_list`查看对应设备名为vd\*云盘的Queue\*绑定到的cpu\_core\_id。

