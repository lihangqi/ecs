# 迁云工具FAQ {#ServerMigrationFAQ .reference}

-   [我在什么场景下可以使用迁云工具？](#section_7j4_nma_nch)
-   [在一台物理主机数据库服务器上有单实例Oracle数据库，向阿里云迁移时，请问是选择整台服务器（包含操作系统、数据库）迁移，还是选择数据库迁移（仅迁移数据库）？两种方式都有哪些利弊？](#section_1eh_f8c_wlg)
-   [迁云工具的迁移过程是什么？](#section_qiw_m1f_xdp)
-   [迁云工具是否支持断点续传？](#section_g9d_fes_ce2)
-   [迁云工具是否支持迁移增量数据？](#section_tnn_o2a_tlb)
-   [迁云完成后的结果是什么？](#section_5xc_zw8_7gm)
-   [迁云完成得到自定义镜像后该如何操作？](#section_zsp_xpw_iz0)
-   [如何处理迁云中断或提示失败？](#section_dlu_chq_06w)
-   [关于中转实例，我需要注意什么？](#section_oiv_v6j_ao0)
-   [关于user\_config.json，我需要注意什么？](#section_pa9_5oa_kds)
-   [什么时候需要过滤目录或文件？](#section_s2c_y14_kmw)
-   [关于client\_data文件，我需要注意什么？](#section_1pm_6qa_aee)
-   [什么时候需要清理client\_data文件？如何清理？](#section_8f1_njh_kw9)
-   [迁云完成后再次迁云该如何操作？](#section_p7d_7bp_ei9)
-   [误释放了中转实例怎么办？](#section_enc_kpa_hth)
-   [为什么提示账号余额不足NotEnoughBalance？](#section_ryc_icm_s7k)
-   [为什么提示RAM权限不足Forbidden.RAM？](#section_2s1_63x_nwh)
-   [为什么提示子账号权限不足Forbidden.SubUser？](#section_8ls_me5_uby)
-   [我的服务器在出方向需要访问哪些公网地址和端口？](#section_otl_h4h_97h)
-   [迁移Windows服务器后怎么检查系统？](#section_2v8_cdh_1oj)
-   [阿里云支持激活哪些Windows Server？](#section_eed_s6s_yl5)
-   [迁移Linux服务器前如何检查是否满足迁云条件？](#section_f8p_iif_638)
-   [迁移Linux服务器后怎么检查系统？](#section_s6m_8av_60f)

## 我在什么场景下可以使用迁云工具？ {#section_7j4_nma_nch .section}

迁云工具可以将物理服务器、虚拟机以及其他云平台云主机一站式地迁移到阿里云ECS，支持迁移主流Windows和Linux操作系统。详情请参见[什么是迁云工具与P2V](cn.zh-CN/迁移服务/P2V 迁云工具/什么是迁云工具.md#)。

## 在一台物理主机数据库服务器上有单实例Oracle数据库，向阿里云迁移时，请问是选择整台服务器（包含操作系统、数据库）迁移，还是选择数据库迁移（仅迁移数据库）？两种方式都有哪些利弊？ {#section_1eh_f8c_wlg .section}

请根据您的实际需要，选择迁移方式。两种迁移方式的利弊如下：

-   如果您只需要Oracle数据库应用，则仅迁移Oracle应用更为轻量合适。缺点是迁移后您需要重新考虑Oracle应用的部署接入方式。
-   如果您既需要Oracle应用，又依赖操作系统的应用环境，则整体迁移服务器至阿里云更为方便。缺点是如果服务器整体量大，迁移周期较长。

## 迁云工具的迁移过程是什么？ {#section_qiw_m1f_xdp .section}

迁云工具的迁移过程如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/156283243813350_zh-CN.png)

1.  检查源服务器是否满足迁移条件。
2.  在您的云账号下创建一台临时中转实例，将源服务器系统数据传输到中转实例。
3.  从中转实例打快照制作自定义镜像。

## 迁云工具是否支持断点续传？ {#section_g9d_fes_ce2 .section}

支持。数据传输中断后，重新运行迁云工具即可继续迁云。

## 迁云工具是否支持迁移增量数据？ {#section_tnn_o2a_tlb .section}

不支持。建议在迁云前先暂停如数据库或容器服务之类的应用，或者先过滤相关数据目录，迁云完成后再同步数据。过滤目录，请参见[什么时候需要过滤目录或文件？](#section_s2c_y14_kmw)

## 迁云完成后的结果是什么？ {#section_5xc_zw8_7gm .section}

迁云完成后，会生成一份源服务器操作系统的自定义镜像，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)，在相应地域的镜像列表中查看。

## 迁云完成得到自定义镜像后该如何操作？ {#section_zsp_xpw_iz0 .section}

建议您先使用该镜像创建一台按量付费的实例，检查系统是否正常。确认镜像可用后，选择合适您业务的实例规格并创建一台或多台ECS实例。实例规格详情，请参见[实例规格族](../cn.zh-CN/实例/实例规格族.md#)。创建ECS实例，请参见[使用向导创建实例](../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。

## 如何处理迁云中断或提示失败？ {#section_dlu_chq_06w .section}

不同情况的处理方式如下。

-   当迁云工具程序异常退出或者迁云进度卡顿时，可以尝试重新运行迁云工具恢复迁云。
-   如果迁云失败并提示Not Finished，您可以查看Logs目录下的日志文件，查看报错原因并排查问题。常见问题及解决方案，请参见[问题排查](cn.zh-CN/迁移服务/P2V 迁云工具/问题排查.md#)。错误码详情，请参见[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

    如果问题仍未解决，建议您添加[迁云工具支持钉钉群](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.x8X0fd&code=ca190154ff)。更多联系方式，请参见[联系我们](cn.zh-CN/迁移服务/P2V 迁云工具/联系我们.md#)。


## 关于中转实例，我需要注意什么？ {#section_oiv_v6j_ao0 .section}

关于中转实例，您需要注意以下几点：

-   迁云工具自动创建、启动、停止和释放中转实例`INSTANCE_FOR_GOTOALIYUN`。为保证迁云顺利完成，请勿人为干预中转实例的运行状态。
-   中转实例的默认安全组在入方向开放了8080和8703端口，这是中转实例的迁云服务端口，请勿修改或删除该安全组配置。
-   迁云完成后，中转实例会被自动释放。如果迁云失败，需要您手动释放中转实例，详情请参见[释放实例](../cn.zh-CN/实例/管理实例/释放实例.md#)。

## 关于user\_config.json，我需要注意什么？ {#section_pa9_5oa_kds .section}

如果已经开始迁云，并且中转实例已经创建，请勿修改user\_config.json里的系统盘大小或数据盘大小配置。如果仍然需要修改，必须清理client\_data文件后重新迁云。

## 什么时候需要过滤目录或文件？ {#section_s2c_y14_kmw .section}

源服务器中有不需要上传的数据目录或文件，可以通过配置Excludes文件过滤，提高迁云效率。

特别地，您可以过滤无法暂停的数据库、Docker容器或者处于活动状态的数据目录或文件，以提高数据传输的稳定性。

## 关于client\_data文件，我需要注意什么？ {#section_1pm_6qa_aee .section}

client\_data文件记录了迁云过程数据，包含中转实例信息、迁云进度等。一般情况下请不要手动修改或删除client\_data文件，否则可能会导致迁云失败。

## 什么时候需要清理client\_data文件？如何清理？ {#section_8f1_njh_kw9 .section}

以下情况需要清理client\_data文件：

-   迁云已经开始后如果想重新迁云，可以清理现有的client\_data文件或者使用原始的client\_data文件覆盖后再运行。
-   同时在某些迁云失败的情况下，如误释放中转实例、VPC、虚拟交换机或者安全组不存在等，可以尝试清理client\_data操作来解决。

清理client\_data文件的方式如下：

-   迁云工具提供的CLI参数`--cleardata`，详情请参见[CLI参数](cn.zh-CN/迁移服务/P2V 迁云工具/CLI参数.md#)。
-   （仅适用于Windows系统）迁云工具Windows GUI版本**配置** \> **清理工具数据**菜单项，详情请参见[迁云工具Windows GUI版本介绍](cn.zh-CN/迁移服务/P2V 迁云工具/迁云工具 Windows GUI 版本介绍.md#)。

## 迁云完成后再次迁云该如何操作？ {#section_p7d_7bp_ei9 .section}

清理client\_data数据文件，然后运行迁云工具重新迁云。

## 误释放了中转实例怎么办？ {#section_enc_kpa_hth .section}

清理client\_data数据文件，然后运行迁云工具重新迁云。

## 为什么提示账号余额不足NotEnoughBalance？ {#section_ryc_icm_s7k .section}

迁云工具本身是免费的，但迁云时默认创建按量付费中转实例。根据阿里云收费服务标准，创建按量付费实例需要您的云账号余额不低于100元人民币。按量付费实例的计费详情，请参见[按量付费](../cn.zh-CN/产品定价/按量付费.md#)。

## 为什么提示RAM权限不足Forbidden.RAM？ {#section_2s1_63x_nwh .section}

您的RAM账号创建的AccessKey没有管理ECS和VPC资源的权限。建议您联系主账号授权[`AliyunECSFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunECSFullAccess/info)和[`AliyunVPCFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunVPCFullAccess/info)角色策略。

## 为什么提示子账号权限不足Forbidden.SubUser？ {#section_8ls_me5_uby .section}

迁云工具需要使用账号AccessKeyID和AccesKeySecret调用ECS API创建中转实例和云盘等资源，该操作属于下单操作。某些服务商账号可能不具备该权限，如果有迁移需求，可以[联系阿里云](cn.zh-CN/迁移服务/P2V 迁云工具/联系我们.md#)。

## 我的服务器在出方向需要访问哪些公网地址和端口？ {#section_otl_h4h_97h .section}

确认源服务器能访问以下服务地址及端口。

-   云服务器ECS：`https://ecs.aliyuncs.com` 443端口。有关其他地域ECS服务地址，请参见[接入地址](../cn.zh-CN/API参考/快速入门/请求结构.md#)。
-   专有网络VPC：`http://vpc.aliyuncs.com` 443端口。
-   安全凭证STS：`https://sts.aliyuncs.com` 443端口。
-   中转实例：公网IP地址8080和8703端口。使用VPC内网迁移方案时，访问私有IP地址。VPC内网迁移详情，请参见[VPC内网迁移](../cn.zh-CN/迁移服务/P2V 迁云工具/VPC内网迁云.md#)。

**说明：** 源服务器不需要开放任何入方向的端口，但是需要在出方向访问上述公网地址和端口。

## 迁移Windows服务器后怎么检查系统？ {#section_2v8_cdh_1oj .section}

迁移Windows系统后初次启动实例时，您需要进行以下检查：

1.  检查系统盘数据是否完整。
2.  如果有数据盘缺失，进入磁盘管理检查盘符是否丢失。
3.  等待文件系统权限修复过程完成后，选择是否重启实例：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/156283243813956_zh-CN.png)

    **说明：** 初次启动ECS实例后，如果文件系统权限修复程序未自启动，您可以运行C:\\go2aliyun\_prepare\\go2aliyun\_restore.exe手动修复。执行前要确保实例上的磁盘数量和盘符路径跟源系统保持一致。

4.  检查网络服务是否正常。
5.  检查其他系统应用服务是否正常。

## 阿里云支持激活哪些Windows Server？ {#section_eed_s6s_yl5 .section}

支持自动激活Windows Server 2003、2008、2012和2016。其他Windows版本如果迁移至ECS，需要申请许可移动性证，详情请参见[申请许可移动性证](https://help.aliyun.com/document_detail/84749.html)。

## 迁移Linux服务器前如何检查是否满足迁云条件？ {#section_f8p_iif_638 .section}

您可以使用迁云工具中自带的client\_check工具检测。运行./client\_check --check命令即可，如果所有检测项均提示`OK`，则表示满足迁云条件。

## 迁移Linux服务器后怎么检查系统？ {#section_s6m_8av_60f .section}

迁移Linux系统后初次启动实例时，您需要进行以下检查：

1.  检查系统盘数据是否完整。
2.  如果有数据盘，您需要自行挂载数据盘，详情请参见[挂载数据盘](../cn.zh-CN/块存储/云盘/挂载云盘.md#)。
3.  检查网络服务是否正常。
4.  然后检查其他系统服务是否正常。

