# 镜像FAQ {#concept_q1j_bty_dhb .concept}

本文介绍镜像相关的常见问题及解决方案。

-   Aliyun Linux 2 FAQ
    -   [Aliyun Linux 2与Aliyun Linux有何不同？](#section_zxs_xnv_fhb)
    -   [如何开始在阿里云上使用Aliyun Linux 2？](#section_hwh_g4v_fhb)
    -   [在阿里云ECS中运行Aliyun Linux 2是否有任何相关成本？](#section_fnh_h4v_fhb)
    -   [Aliyun Linux 2支持哪些阿里云ECS实例类型？](#section_eys_j4v_fhb)
    -   [Aliyun Linux 2是否支持32位应用程序和库？](#section_c2h_44v_fhb)
    -   [Aliyun Linux 2是否附带图形用户界面（GUI）桌面？](#section_ybf_r4v_fhb)
    -   [是否可以查看Aliyun Linux 2组件的源代码？](#section_vd3_t4v_fhb)
    -   [Aliyun Linux 2是否与现有版本的Aliyun Linux向后兼容？](#section_rjq_v4v_fhb)
    -   [是否可以在本地使用Aliyun Linux 2？](#section_nwf_z4v_fhb)
    -   [Aliyun Linux 2上支持运行哪些第三方应用程序？](#section_lkv_cpv_fhb)
    -   [相比其他Linux操作系统，Aliyun Linux 2有哪些优势？](#section_fmy_jpv_fhb)
    -   [Aliyun Linux 2怎样保证数据安全？](#section_vsv_spv_fhb)
    -   [Aliyun Linux 2是否支持数据加密？](#section_mcz_fqv_fhb)
    -   [怎样设置Aliyun Linux 2的有关权限？](#section_f41_jqv_fhb)
-   一般性FAQ
    -   [选择了镜像后能更换吗？](#section_ovb_trx_fhb)
    -   [ECS系统盘是否支持KMS加密，通过Terraform或Packer如何使用？](#section_bjd_h5l_93s)
-   快照与镜像相关FAQ
    -   [快照和镜像有什么不同？有什么关系？](#section_bmh_2xf_3ds)
    -   [如何将A账号下面的ECS快照数据迁移到B账号下？](#section_ed5_k10_dzu)
    -   [数据盘的快照不能创建自定义镜像吗？那如何将A账号下的数据盘快照迁移到B账号？](#section_lyx_6pb_932)
    -   [因为删除了创建快照的实例，而导致使用快照回滚不成功，该如何解决？](#section_5p6_ip2_7g0)
    -   [ECS实例系统快照能否下载到本地？](#section_1ff_9s6_3i5)
    -   [实例释放后，快照是否还存在？](#section_ocf_oay_z1e)
    -   [我想删除华北2快照链列表内的某一快照，但提示我关联了“RequestId: xxx”，这个是什么？](#section_72i_6dy_wdp)
    -   [之前实例的地域为华东1（杭州），对数据盘做了快照。实例到期释放我在华东1（杭州）地域又新购了一个实例，能否把之前实例的快照回滚？](#section_c7y_3ij_f53)
-   自定义镜像FAQ
    -   [如何查看数据盘？](#section_hrq_fgx_fhb)
    -   [如何卸载（umount）和删除disk table里的数据？](#section_lzy_rgx_fhb)
    -   [如何确认已经卸载数据盘，并可以新建自定义镜像？](#section_wdy_3ty_dhb)
    -   [实例释放后，自定义镜像是否还存在？](#section_qbd_ghx_fhb)
    -   [用于创建自定义镜像的实例到期或释放数据后，创建的自定义镜像是否受影响？使用自定义镜像开通的实例是否受影响？](#section_zc5_shx_fhb)
    -   [使用自定义镜像创建的实例是否可以更换操作系统？更换系统后原来的自定义镜像是否还可以使用？](#section_j1z_thx_fhb)
    -   [更换系统盘时另选操作系统，是否可以使用自定义镜像？](#section_b21_zhx_fhb)
    -   [已创建的自定义镜像，是否可以用于更换另一台云服务器ECS的系统盘数据？](#section_cv1_g3x_fhb)
    -   [是否可以升级自定义镜像开通的云服务器ECS的CPU、内存、带宽、硬盘等？](#section_y35_m3x_fhb)
    -   [是否可以跨地域使用自定义镜像？](#section_twm_n3x_fhb)
    -   [包年包月实例的自定义镜像，是否可以用于创建按量付费的云服务器ECS？](#section_t5m_cjx_fhb)
    -   [使用自定义镜像创建的实例，系统磁盘自动扩容失败的原因是什么？怎么办？](#section_oqc_u0t_5ri)
    -   [创建自定义镜像、ECS实例时为何需要注释挂载项？](#section_uar_ern_zbt)
    -   [如何配置并使用Docker私有镜像库？](#section_4wu_r5p_bi1)
    -   [如何克隆ECS服务器？](#section_wnw_26f_axp)
    -   [有些自定义镜像不支持创建I/O优化的实例，我该如何操作？](#section_nvl_tpi_ffj)
    -   [在哪里查看导入镜像的进度？导入镜像需要多少时间？](#section_o5a_k1v_smp)
    -   [在哪里查看镜像创建进度？创建镜像需要多少时间？](#section_ioj_atj_1te)
-   复制镜像FAQ
    -   [什么情况下需要复制镜像？](#section_pbs_h4c_ghb)
    -   [可以复制哪些镜像？](#section_j4j_n4c_ghb)
    -   [当前有哪些支持复制镜像功能的地域？](#section_jcb_44c_ghb)
    -   [复制一个镜像大概需要多久？](#section_wzx_44c_ghb)
    -   [复制镜像怎么收费的？](#section_nbz_q4c_ghb)
    -   [在复制镜像过程中，源镜像和目标镜像有什么限制？](#section_inj_s4c_ghb)
    -   [怎么复制我的云账号的镜像资源到其他阿里云账号的其他地域？](#section_kyv_54c_ghb)
    -   [复制镜像有镜像容量限制吗？](#section_k14_x4c_ghb)
    -   [从其他地域复制过来的镜像，镜像页面显示状态为可用。但通过此镜像创建实例时，提示“您指定的镜像被禁用或者已被删除”，为什么？](#section_lxo_ujw_fm3)
    -   [国际站数据迁移到国内有什么方法？](#section_oqq_9z9_t00)
-   共享镜像FAQ
    -   [我最多可以获得多少个共享镜像？](#section_xry_y4c_ghb)
    -   [每个镜像最多可以共享给多少个用户？](#section_pwp_ypc_ghb)
    -   [我有多个站点的账号，能否互相共享镜像？](#section_jeb_xr5_8wn)
    -   [使用共享镜像是否占用我的镜像名额？](#section_agd_2qc_ghb)
    -   [使用共享镜像创建实例的时候存不存在地域限制？](#section_mls_2qc_ghb)
    -   [使用共享镜像创建实例存在什么样的风险？](#section_p4w_lqc_ghb)
    -   [我把自定义镜像共享给其他账号，存在什么风险？](#section_r4q_nqc_ghb)
    -   [我能把别人共享给我的镜像再共享给其他人吗？](#section_abm_4qc_ghb)
    -   [我把镜像共享给他人，还能使用该镜像创建实例吗？](#section_xny_pqc_ghb)
    -   [华北地域服务器A制作的镜像能共享给华东地域的服务器B吗？](#section_b5i_fn9_i06)
-   导出镜像FAQ
    -   [为何没有导出镜像的入口？](#section_j80_1pu_tv2)
    -   [我想将镜像导出到本地进行测试，具体要怎么操作呢？](#section_9dl_9cs_oba)
-   删除镜像FAQ
    -   [如果使用自定义镜像创建了ECS实例，我可以删除这个镜像吗？](#section_lvj_dht_8a4)
    -   [我曾把自己账号中的某个自定义镜像共享给其他账号，现在我可以删除这个镜像吗？](#section_fqt_49s_s3v)
    -   [我把某个自定义镜像（M）的共享账号（A）给删除了，会有什么影响？](#section_qn6_1dm_1tn)
    -   [删除镜像的时候提示“指定的镜像Id还存在保有实例，不能删除该镜像”，为什么？](#section_qe9_38d_hvk)
-   更换镜像（操作系统）FAQ
    -   [更换系统盘时，选择的镜像中包含数据盘的话，能通过更换系统盘实现更换镜像吗？](#section_053_0tw_h6a)
    -   [我目前有一台ECS服务器，想用现有的镜像来更换这台ECS的操作系统，怎么操作？](#section_69i_52e_jfd)
    -   [账号A的服务器制作镜像后，能给账号B更换磁盘用吗？](#section_oww_crp_0j9)
-   镜像费用FAQ
    -   [为什么创建实例时自定义镜像的配置费用高于公共镜像？](#section_k04_yg7_uoa)
-   镜像商业化FAQ
    -   [镜像市场的镜像有哪些功能？](#section_8wl_8ju_9pi)
    -   [镜像市场的镜像能带来哪些便利？](#section_c0p_y2e_36h)
    -   [目前镜像市场的镜像支持哪些服务器环境和应用场景？](#section_4aa_s13_huj)
    -   [镜像市场的镜像是否安全？](#section_hng_971_32q)
    -   [镜像市场的镜像安装使用过程中出问题了怎么办？](#section_jyl_7r1_85r)
    -   [如何购买镜像市场镜像？](#section_hxc_rqc_ghb)
    -   [按次购买的镜像的使用期限是多久？](#section_hqw_prc_ghb)
    -   [镜像市场的镜像支持退款吗？](#section_gzm_qrc_ghb)
    -   [镜像市场商业化后，还有免费的镜像市场镜像吗？](#section_okl_src_ghb)
    -   [在杭州买了一个镜像市场的镜像，能否在北京创建ECS实例或者更换系统盘？](#section_ndz_src_ghb)
    -   [ECS实例使用镜像市场的镜像，升级和续费ECS实例，需要为镜像继续付费吗？](#section_jwc_fsx_fhb)
    -   [ECS实例使用镜像市场的镜像，实例释放后，继续购买ECS实例还可以免费使用该镜像吗？](#section_yqb_wrc_ghb)
    -   [使用镜像市场镜像创建ECS实例，该实例创建一个自定义镜像，使用该自定义镜像创建ECS实例需要为该镜像付费吗？](#section_pnn_yrc_ghb)
    -   [来源于镜像市场的镜像复制到其他地域创建ECS实例，是否需要为该镜像付费？](#section_bqm_zrc_ghb)
    -   [如果把来源于镜像市场的自定义镜像共享给其他账号（B）创建ECS实例，账号B是否需要为该镜像付费？](#section_ymk_1sc_ghb)
    -   [如果使用镜像市场的镜像或者来源于镜像市场的镜像进行更换系统盘，需要付费吗？](#section_uj5_1sc_ghb)
    -   [ECS实例正在使用镜像市场的镜像，进行重置系统盘需要收费吗？](#section_nj4_bsc_ghb)
    -   [怎么调用ECS API，使用镜像市场镜像或者来源镜像市场的自定义镜像或者共享镜像，创建ECS实例和更换系统盘？](#section_xl1_csc_ghb)
    -   [如果没有购买镜像市场的镜像或者来源于镜像市场的镜像，在调用ECS API使用该镜像创建ECS实例和更换系统盘，会报错吗？](#section_sxt_hsc_ghb)
    -   [我的ESS是自动创建机器的，并且量是不固定，设置最小值为10台，最大值为100台，那么使用镜像市场的镜像如何保证我的的需求实例能正常弹出来？](#section_nfx_5sc_ghb)
    -   [镜像市场的镜像是否支持批量购买？](#section_clp_ysc_ghb)
    -   [如果之前使用的镜像市场的镜像，已不存在该商品（如：jxsc000010、jxsc000019），怎能保证已经设置的弹性伸缩组的机器能正常弹出？](#section_stt_zsc_ghb)
    -   [1个product code能否支持不同region的镜像？](#section_os3_btc_ghb)
    -   [我买了100 product code同样值的镜像，是否可以支持在所有的地域可用？](#section_uzj_ctc_ghb)
    -   [勾选“I/O优化实例”选项导致购买ECS实例时无法选择镜像市场的镜像，为什么？怎么解决？](#section_tch_39p_cv5)
-   镜像市场预付费镜像FAQ
    -   [什么是镜像市场的包年包月和按周付费镜像？](#section_zxy_n5c_ghb)
    -   [预付费镜像能与哪种ECS实例搭配使用？](#section_fts_45c_ghb)
    -   [怎么购买预付费镜像？可以单独购买吗？](#section_rfp_s5c_ghb)
    -   [预付费镜像怎么付费？](#section_xhj_w5c_ghb)
    -   [预付费镜像到期了就不能用了吗？怎么继续使用？](#section_cc4_x5c_ghb)
    -   [购买预付费镜像后，如果我不想再使用这个镜像，能要求退款吗？](#section_gwb_z5c_ghb)
    -   [退款时，费用怎么结算？](#section_hvt_z5c_ghb)
    -   [预付费镜像能转换为按量付费镜像吗？](#section_hpg_1vc_ghb)
    -   [预付费镜像与其它镜像之间能互换吗？更换后费用怎么计算？](#section_sqw_1vc_ghb)
    -   [在哪里查看并管理我购买的预付费镜像？](#section_fmx_fvc_ghb)
    -   [使用预付费镜像制作的自定义镜像会收费吗？预付费镜像过期对于自定义镜像有什么影响？](#section_klq_gvc_ghb)
-   ECS实例与操作系统镜像FAQ
    -   [为什么有的ECS实例无法选择Windows操作系统？](#section_ajg_qwc_ghb)
    -   [ECS实例使用操作系统需要付费吗？](#section_ttw_qwc_ghb)
    -   [我能自己安装或者升级操作系统吗？](#section_zhs_twc_ghb)
    -   [操作系统是否有图形界面？](#section_ulp_xwc_ghb)
    -   [如何选择操作系统？](#section_wqy_zwc_ghb)
    -   [公共镜像自带FTP上传吗？](#section_jtv_dxc_ghb)
    -   [阿里云支持哪些SUSE版本？](#section_mgc_fxc_ghb)
    -   [SUSE操作系统提供哪些服务支持？](#section_jpr_fxc_ghb)
    -   [ECS实例到期释放后，如果这个实例之前手动制作了镜像快照，能不能找回之前实例的数据？](#section_uj1_il5_0xb)
    -   [我先有一台ECS实例，想再买一台ECS实例并使用现有这台ECS实例的镜像部署，应该如何操作？](#section_d2a_pl9_3vq)
    -   [我已经购买了新的ECS服务器，如何把我的共享镜像恢复到这台新购ECS服务器上？](#section_54f_mg4_r2p)
    -   [实例的操作系统为Windows Server 2008 R2企业版，现在说Windows副本不是正版怎么办？](#section_dcb_fs7_ljf)
    -   [我在阿里云有多个账号，想把账号A的一台服务器转移到账号B，或者用账号B购买一台服务器，通过镜像把服务器运行环境、所有安装应用迁移到账号B的服务器。怎么操作？](#section_cvk_0gm_ods)
    -   [阿里云ECS实例之间如何迁移？](#section_pkf_2xq_13z)
    -   [两个不同专有网络下的ECS服务器能否实现网络互通？](#section_lqt_tci_xa6)
    -   [如何处理CentOS DNS解析超时？](#section_x8y_les_u5u)
    -   [为什么ECS默认没有启用虚拟内存或Swap说明？](#section_m02_5j5_qf2)
    -   [如何在阿里云公共镜像中开启kdump？](#section_kwb_4l4_a16)
    -   [Linux镜像如何开启或关闭Meltdown与Spectre安全漏洞补丁？](#section_mf9_75m_jnp)
    -   [如何检查与修复CentOS 7实例和Windows实例IP地址缺失问题？](#section_29l_kc7_8hw)

## Aliyun Linux 2与Aliyun Linux有何不同？ {#section_zxs_xnv_fhb .section}

Aliyun Linux 2和Aliyun Linux之间的主要区别是：

-   Aliyun Linux 2针对容器场景优化，更好支持云原生应用。
-   Aliyun Linux 2附带了更新的Linux内核、及用户态软件包版本。

## 如何开始在阿里云上使用Aliyun Linux 2？ {#section_hwh_g4v_fhb .section}

阿里云为Aliyun Linux 2提供了官方镜像，您可以在购买时选择使用该镜像创建阿里云ECS实例。

## 在阿里云ECS中运行Aliyun Linux 2是否有任何相关成本？ {#section_fnh_h4v_fhb .section}

没有。运行Aliyun Linux 2是免费的，您只需支付ECS实例运行的费用。

## Aliyun Linux 2支持哪些阿里云ECS实例类型？ {#section_eys_j4v_fhb .section}

Aliyun Linux 2支持大部分阿里云ECS实例类型，包括弹性裸金属服务器。

**说明：** Aliyun Linux 2不支持使用Xen虚拟机平台和使用经典网络类型的实例，目前对此类型实例不开放Aliyun Linux 2的购买选项。

## Aliyun Linux 2是否支持32位应用程序和库？ {#section_c2h_44v_fhb .section}

暂不支持。

## Aliyun Linux 2是否附带图形用户界面（GUI）桌面？ {#section_ybf_r4v_fhb .section}

暂不提供官方支持。

## 是否可以查看Aliyun Linux 2组件的源代码？ {#section_vd3_t4v_fhb .section}

Aliyun Linux 2遵循开源协议。您可以通过yumdownloader工具或者在阿里云开源站点下载源代码包，也可以从Github站点下载Aliyun Linux内核源代码树。

## Aliyun Linux 2是否与现有版本的Aliyun Linux向后兼容？ {#section_rjq_v4v_fhb .section}

Aliyun Linux 2完全兼容Aliyun Linux 17.01。

**说明：** 如果您使用了自行编译的内核模块，可能需要在Aliyun Linux 2上重新编译才能正常使用。

## 是否可以在本地使用Aliyun Linux 2？ {#section_nwf_z4v_fhb .section}

Aliyun Linux 2目前只支持阿里云云服务器ECS，暂不支持其它第三方虚拟化平台。

## Aliyun Linux 2上支持运行哪些第三方应用程序？ {#section_lkv_cpv_fhb .section}

当前Aliyun Linux 2与CentOS 7.6.1810版本二进制兼容，因此所有可以运行在CentOS上的应用程序，均可在Aliyun Linux 2上流畅运行。

## 相比其他Linux操作系统，Aliyun Linux 2有哪些优势？ {#section_fmy_jpv_fhb .section}

Aliyun Linux 2与CentOS 7.6.1810发行版保持二进制兼容，在此基础上提供差异化的操作系统功能。

与CentOS及RHEL相比，Aliyun Linux 2的优势体现在：

-   满足您的操作系统新特性诉求，更快的发布节奏，更新的Linux内核、用户态软件及工具包。
-   开箱即用，最简用户配置，最短时间服务就绪。
-   最大化用户性能收益，与云基础设施联动优化。
-   与RHEL相比没有运行时计费，与CentOS相比有商业支持。

## Aliyun Linux 2怎样保证数据安全？ {#section_vsv_spv_fhb .section}

Aliyun Linux 2二进制兼容CentOS 7.6.1810/RHEL 7.6，遵从RHEL的安全规范。具体体现在以下几个方面：

-   使用业内标准的漏洞扫描及安全测试工具，定期做安全扫描。
-   定期评估CentOS 7的CVE补丁，修补OS安全漏洞。
-   与安全团队合作，支持阿里云现有的OS安全加固方案。
-   使用CentOS 7相同的机制，发布用户安全警告及补丁更新。

## Aliyun Linux 2是否支持数据加密？ {#section_mcz_fqv_fhb .section}

Aliyun Linux 2保留CentOS 7的数据加密工具包，并确保CentOS 7与KMS协同工作的加密方案可以在Aliyun Linux 2得到支持。

## 怎样设置Aliyun Linux 2的有关权限？ {#section_f41_jqv_fhb .section}

Aliyun Linux 2属于与CentOS 7同源的操作系统。CentOS 7的管理员可以无缝地使用完全一致的管理命令做相关的权限设置，Aliyun Linux 2的缺省权限设置与阿里云CentOS 7镜像完全一致。

## 选择了镜像后能更换吗？ {#section_ovb_trx_fhb .section}

可以更换。在ECS控制台，选择更换系统盘，即可选择所需的镜像进行更换。请注意，更换镜像会导致系统盘数据丢失，请在确认更换前做好数据备份。

## ECS系统盘是否支持KMS加密，通过Terraform或Packer如何使用？ {#section_bjd_h5l_93s .section}

目前，ECS系统盘支持KMS的默认key加密，即选择加密后，ECS系统会为您在KMS中的使用地域自动创建一个专为ECS使用的CMK。详情请参见[ECS云盘加密](../intl.zh-CN/块存储/云盘/ECS云盘加密.md#)。

BYOK加密方式和Packer加密功能即将支持。

Terraform中通过参数encrypted指定，详情请参见[alicloud\_disks](https://www.terraform.io/docs/providers/alicloud/d/disks.html)。

## 快照和镜像有什么不同？有什么关系？ {#section_bmh_2xf_3ds .section}

快照和镜像的不同如下：

-   镜像可直接用来创建ECS实例，而快照不可以。
-   快照可以是ECS实例系统盘或数据盘的数据备份，而镜像一定包含ECS实例系统盘的数据。
-   快照只能用于当前ECS实例磁盘的数据恢复，而镜像可用于当前ECS实例及其他实例更换系统盘或创建新的ECS实例。
-   快照不可以跨地域使用。若您需要在其他地域恢复实例数据，可使用自定义镜像，详情请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)。
-   应用场景不同。由于您只能使用自定义镜像备份数据，这里仅列举快照和自定义镜像的一些应用场景。

    快照适用场景：

    -   定期数据备份，按照设定的周期，每日、每周或每月自动执行快照策略对数据进行备份。
    -   临时数据备份，例如：
        -   系统更新、应用发布等系统临时变更，为防止操作错误，在执行变更前手工创建快照对系统进行备份。
        -   系统盘扩容前，创建快照备份数据。
        -   磁盘数据迁移，为磁盘创建快照，将磁盘作为另一块磁盘的基础数据。
    自定义镜像适用场景：

    -   备份短期内不会更改的系统，如已经完成发布或更新的应用系统。
    -   使用已经完成安装和配置的系统为模板，创建新的ECS实例，如批量部署应用。
    -   系统及数据迁移，如将经典网络的ECS实例迁移到VPC下。
    -   跨可用区和地域还原系统。

快照和镜像的关系如下：

使用实例创建自定义镜像时，ECS会为实例的每块磁盘创建快照，即自定义镜像包含ECS实例所有磁盘的快照。具体步骤，请参见[使用实例创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。

使用系统盘快照，也可以创建自定义镜像。具体步骤，请参见[使用快照创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)。

## 如何将A账号下面的ECS快照数据迁移到B账号下？ {#section_ed5_k10_dzu .section}

快照不支持迁移。如果您有需要，可将快照制作成镜像，然后共享到其他账号下。详情请参见[使用快照创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)和[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。

## 数据盘的快照不能创建自定义镜像吗？那如何将A账号下的数据盘快照迁移到B账号？ {#section_lyx_6pb_932 .section}

创建自定义镜像的快照磁盘属性必须是系统盘，数据盘不能用于创建自定义镜像。

如果您需要将A账号数据盘快照迁移到B账号，可按以下步骤操作。

1.  为数据盘快照的原实例创建镜像。具体步骤，请参见[使用实例创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。
2.  共享镜像给B账号。具体步骤，请参见[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。
3.  在B账号中，使用该镜像新购一台按量付费实例。具体步骤，请参见[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。
4.  为新购实例的数据盘创建快照。具体步骤，请参见[创建快照](../intl.zh-CN/快照/使用快照/创建快照.md#)。
5.  释放该新购实例。具体步骤，请参见[释放实例](../intl.zh-CN/实例/管理实例/释放实例.md#)。

## 因为删除了创建快照的实例，而导致使用快照回滚不成功，该如何解决？ {#section_5p6_ip2_7g0 .section}

您可以按照以下步骤操作。

1.  使用快照创建自定义镜像。具体步骤，请参见[使用快照创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)。
2.  更换系统盘，更换时选择该自定义镜像。具体步骤，请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

## ECS实例系统快照能否下载到本地？ {#section_1ff_9s6_3i5 .section}

快照不能下载到本地。您可以利用快照创建镜像，再申请导出镜像。具体步骤，请参见[使用快照创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)和[导出镜像](intl.zh-CN/镜像/自定义镜像/导出镜像.md#)。

## 实例释放后，快照是否还存在？ {#section_ocf_oay_z1e .section}

保留手动快照，自动快照会随着实例释放而被清除。更多详情，请参见[快照FAQ](../intl.zh-CN/快照/快照FAQ.md#)。

## 我想删除华北2快照链列表内的某一快照，但提示我关联了“RequestId: xxx”，这个是什么？ {#section_72i_6dy_wdp .section}

您的快照创建过自定义镜像，需要先删除这个自定义镜像才可以删除快照。

## 之前实例的地域为华东1（杭州），对数据盘做了快照。实例到期释放我在华东1（杭州）地域又新购了一个实例，能否把之前实例的快照回滚？ {#section_c7y_3ij_f53 .section}

快照回滚是回滚到原来的实例。您可以利用之前数据盘的快照创建云盘，将云盘挂载到新的实例上。具体步骤，请参见[用快照创建云盘](../intl.zh-CN/块存储/云盘/创建云盘/使用快照创建云盘.md#)和[挂载云盘](../intl.zh-CN/块存储/云盘/挂载云盘.md#)。

## 如何查看数据盘？ {#section_hrq_fgx_fhb .section}

您可以通过df命令查看数据盘的使用情况，以及文件系统被挂载的位置。例如：df –lh。

您可以通过fdisk命令获取数据盘的分区情况。例如：fdisk -l。

## 如何卸载（umount）和删除disk table里的数据？ {#section_lzy_rgx_fhb .section}

假设/dev/hda5已经挂载在/mnt/hda5上，您可以使用下列任一命令卸载已挂载的文件系统。

``` {#codeblock_i3l_6kl_9q7}
umount /dev/hda5
```

``` {#codeblock_qtj_lg8_95v}
umount /mnt/hda5
```

``` {#codeblock_eey_tfr_uy1}
umount /dev/hda5 /mnt/hda5
```

 /etc/fstab是Linux系统下比较重要的配置文件，其包含了系统在启动时挂载的文件系统和存储设备的详细信息。

当您不想在启动实例时挂载指定分区，需要删除当前文件中对应的语句行。例如，删除下面的语句可以在启动的时候断开xvdb1。

``` {#codeblock_gvn_3u3_ojc}
/dev/xvdb1 /leejd ext4 defaults 0 0
```

Linux其他较重要的配置文件如下：

|配置文件|配置说明|修改该配置文件的风险|
|:---|:---|:---------|
|/etc/issue\*, /etc/\*-release, /etc/\*\_version|系统发行版信息配置文件|修改/etc/issue\*会导致系统发行版无法被正常识别，导致系统创建失败。|
|/boot/grub/menu.lst, /boot/grub/grub.conf|系统引导启动配置文件|修改/boot/grub/menu.lst会导致内核无法正确加载，导致系统无法启动。|
|/etc/fstab|系统启动挂载分区配置文件|修改该文件会导致分区无法被加载，导致系统无法启动。|
|/etc/shadow|系统密码相关配置文件|修改该文件为只读会导致无法修改密码文件，导致系统创建失败。|
|/etc/selinux/config|系统安全策略配置文件|修改/etc/selinux/config开启SELinux导致系统无法启动。|

## 如何确认已经卸载数据盘，并可以新建自定义镜像？ {#section_wdy_3ty_dhb .section}

具体步骤如下：

1.  确认/etc/fstab文件中对应的自动挂载数据盘分区语句行已被删除。
2.  使用mount命令查看所有设备的挂载信息，请确认执行结果中不包含对应的数据盘分区信息。

## 实例释放后，自定义镜像是否还存在？ {#section_qbd_ghx_fhb .section}

存在。

## 用于创建自定义镜像的实例到期或释放数据后，创建的自定义镜像是否受影响？使用自定义镜像开通的实例是否受影响？ {#section_zc5_shx_fhb .section}

均不受影响。

## 使用自定义镜像创建的实例是否可以更换操作系统？更换系统后原来的自定义镜像是否还可以使用？ {#section_j1z_thx_fhb .section}

可以。更换后原来的自定义镜像还可以继续使用。

## 更换系统盘时另选操作系统，是否可以使用自定义镜像？ {#section_b21_zhx_fhb .section}

可以。详情请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

**说明：** 系统盘更换为自定义镜像后，原来的数据将被全覆盖。

## 已创建的自定义镜像，是否可以用于更换另一台云服务器ECS的系统盘数据？ {#section_cv1_g3x_fhb .section}

可以。详情请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

**说明：** 自定义镜像将全部覆盖该服务器系统盘的所有数据。

## 是否可以升级自定义镜像开通的云服务器ECS的CPU、内存、带宽、硬盘等？ {#section_y35_m3x_fhb .section}

均可以升级。

## 是否可以跨地域使用自定义镜像？ {#section_twm_n3x_fhb .section}

不可以。自定义镜像只能在同一个地域使用。例如：使用华东1地域的实例创建的自定义镜像，不可以直接用来开通华东2地域的云服务器ECS。

如果您需要跨地域使用自定义镜像，可以先复制镜像到目标地域，请参见[复制镜像](../DNA0011894323/intl.zh-CN/镜像/自定义镜像/复制镜像.md#)。

## 包年包月实例的自定义镜像，是否可以用于创建按量付费的云服务器ECS？ {#section_t5m_cjx_fhb .section}

可以。自定义镜像功能不区分实例的付费方式，即不区分是否包年包月或按量付费。

## 使用自定义镜像创建的实例，系统磁盘自动扩容失败的原因是什么？怎么办？ {#section_oqc_u0t_5ri .section}

使用自定义镜像创建的实例，系统盘自动扩容失败的原因可能是没有安装cloud-init服务、cloud-init服务运行失败或文件系统不支持等。

系统盘自动扩容失败时，您可以手动扩容。

## 创建自定义镜像、ECS实例时为何需要注释挂载项？ {#section_uar_ern_zbt .section}

使用自定义镜像创建ECS实例时，以下原因会导致挂载磁盘失败。

-   创建的ECS实例没有数据盘。
-   数据盘是新磁盘，还没有进行分区格式化。
-   创建的自定义镜像中，未注释掉/etc/fstab文件中的磁盘挂载条目。

下面以ECS实例数据盘未分区，且创建该实例的自定义镜像中未注释掉/etc/fstab中的磁盘挂载条目为例，介绍数据盘挂载失败的原因。

1.  ECS实例数据盘未分区，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592664549584_zh-CN.png)

2.  使用自定义镜像创建的ECS实例中，未注释掉/etc/fstab中的磁盘挂载条目，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592664549589_zh-CN.png)

3.  实例启动时，会按照/etc/fstab文件中的配置挂载磁盘，但由于数据盘未分区导致挂载失败，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592664549591_zh-CN.png)


不用注释磁盘挂载条目的情况：一般只有在创建ECS实例时，选择了数据盘且数据盘是通过已分区、已格式化的数据盘快照生成。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 如何配置并使用Docker私有镜像库？ {#section_4wu_r5p_bi1 .section}

镜像管理是Docker的核心，为了满足企业或组织内部分享镜像，Docker官方在Github上建立了一个开源项目docker-registry，专门用于自建Docker的私有镜像库。

快速启动支持阿里云对象存储OSS的docker-registry：您可以从[GitHub](https://github.com/docker/docker-registry)下载并安装docker-registry，运行pip install docker-registry-driver-alioss命令，通过pip安装OSS driver。

1.  运行docker registry。

    ``` {#codeblock_028_yze_uie}
     docker run -e OSS_BUCKET=-e STORAGE_PATH=/docker/ -e OSS_KEY=-e OSS_SECRET=-p 5000:5000 -d chrisjin/registry:ali_oss
    ```

2.  配置config.yml。

    ``` {#codeblock_rvn_x7o_ncu}
     ```local: &local
     <<: *common
     storage: alioss
     storage_path: _env:STORAGE_PATH:/devregistry/
     oss_bucket: _env:OSS_BUCKET[:default_value]
     oss_accessid: _env:OSS_KEY[:your_access_id]
     oss_accesskey: _env:OSS_SECRET[:your_access_key]```
    ```

3.  启动docker-registry。

    ``` {#codeblock_2np_mne_mlf}
     DOCKER_REGISTRY_CONFIG=［your_config_path］ gunicorn -k gevent -b 0.0.0.0:5000 -w 1 docker_registry.wi:application
    ```


如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)联系阿里云。

## 如何克隆ECS服务器？ {#section_wnw_26f_axp .section}

同一账号地域下，新购ECS服务器时可以克隆现有ECS服务器的环境和数据，快速创建相同环境和配置的新ECS实例。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  选择需要克隆的ECS实例，对系统盘和数据盘分别创建快照。具体请参见[创建快照](../intl.zh-CN/快照/使用快照/创建快照.md#)。

    **说明：** 为保证数据一致性，请在实例状态为**已停止**时创建快照。

3.  使用系统盘快照创建自定义镜像。创建过程中请选中**添加数据盘快照**，并单击**增加**选择并添加已创建的数据盘快照。具体请参见[使用快照创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用快照创建自定义镜像.md#)。
4.  按[使用向导创建实例](../intl.zh-CN/实例/创建实例/使用向导创建实例.md#)创建新的ECS实例。在创建过程中，需要注意以下配置：
    -   地域：必须选择与克隆实例相同的地域。
    -   镜像：**镜像类型**选择**自定义镜像**，并选择使用系统盘创建的自定义镜像。

        **说明：** 如果您选择的自定义镜像中包含了一个或多个数据盘快照，系统会自动根据这些快照创建相同数量的云盘作为数据盘，每个云盘大小与对应的快照相同。您可以增加云盘容量，但不能缩小。


## 有些自定义镜像不支持创建I/O优化的实例，我该如何操作？ {#section_nvl_tpi_ffj .section}

部分自定义镜像不支持创建I/O优化的实例。如果想要使用这类自定义镜来创建I/O优化的实例，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请（提交工单时，需指定镜像名称）。

## 在哪里查看导入镜像的进度？导入镜像需要多少时间？ {#section_o5a_k1v_smp .section}

在ECS管理控制台的镜像列表页查看导入进度。导入自定义镜像是相对耗时的任务，完成的时间取决于镜像文件的大小和当前导入任务并发数，需要您耐心等待。

## 在哪里查看镜像创建进度？创建镜像需要多少时间？ {#section_ioj_atj_1te .section}

在ECS管理控制台的镜像列表页查看。 镜像制作时间取决于实例磁盘的大小。

## 什么情况下需要复制镜像？ {#section_pbs_h4c_ghb .section}

自定义镜像只能在同一个地域使用，不能直接跨地域使用。如果您需要：

-   将云服务器ECS上的应用部署在多个地域。
-   将云服务器ECS迁移到其他地域。
-   跨地域使用自定义镜像。

可以通过复制镜像解决。您可以复制当前地域的自定义镜像到其他地域的同账号中，在其他地域使用自定义镜像实现一致性部署应用环境。

## 可以复制哪些镜像？ {#section_j4j_n4c_ghb .section}

复制镜像只支持自定义镜像。不支持公共镜像，镜像市场镜像和别人共享给您的镜像。

## 当前有哪些支持复制镜像功能的地域？ {#section_jcb_44c_ghb .section}

阿里云所有地域均支持复制镜像功能。

## 复制一个镜像大概需要多久？ {#section_wzx_44c_ghb .section}

复制镜像的时间取决于网络传输速度和任务队列的排队数量。复制镜像需要通过网络把一个地域的可用区中的镜像文件传输到目标地域的可用区，需要您耐心等待。

## 复制镜像怎么收费的？ {#section_nbz_q4c_ghb .section}

复制镜像过程包括以下操作：

1.  从源地域将生成自定义镜像的快照复制到目标地域。
2.  在目标地域根据快照自动生成自定义镜像。

上述过程可能涉及以下费用：

-   不同地域之间的数据传输流量费。阿里云目前暂未对这部分流量收费，具体收费时间请以官网公告为准。
-   复制过来的快照会占用快照容量。阿里云目前暂未对快照收费，具体收费时间请以官网公告为准 。

## 在复制镜像过程中，源镜像和目标镜像有什么限制？ {#section_inj_s4c_ghb .section}

在复制过程中，源镜像禁止删除，目标镜像可以取消复制，不能用于更换系统盘和创建ECS实例。

## 怎么复制我的云账号的镜像资源到其他阿里云账号的其他地域？ {#section_kyv_54c_ghb .section}

您需要复制自己的镜像到目标地域，并将该镜像共享给对方的云账号。对方云账号的共享镜像列表中会显示该镜像。

## 复制镜像有镜像容量限制吗？ {#section_k14_x4c_ghb .section}

没有限制。但是，复制容量超过500GiB时需要提交工单申请，当您在控制台单击**复制镜像**时，控制台会提示您提交工单申请。

## 从其他地域复制过来的镜像，镜像页面显示状态为可用。但通过此镜像创建实例时，提示“您指定的镜像被禁用或者已被删除”，为什么？ {#section_lxo_ujw_fm3 .section}

如果自定义镜像基于镜像市场的镜像创建， 然后复制到其他地域，是不可以创建ECS实例的。镜像市场的镜像是无法通过创建自定义镜像，复制到其它地域之后创建ECS实例的。

## 国际站数据迁移到国内有什么方法？ {#section_oqq_9z9_t00 .section}

您可以通过复制镜像实现。具体步骤，请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)。

## 我最多可以获得多少个共享镜像？ {#section_xry_y4c_ghb .section}

100个。

## 每个镜像最多可以共享给多少个用户？ {#section_pwp_ypc_ghb .section}

50个。

## 我有多个站点的账号，能否互相共享镜像？ {#section_jeb_xr5_8wn .section}

可以。支持中国站、国际站、日本站的账号之间共享镜像，但是基于镜像市场镜像创建的自定义镜像除外。

## 使用共享镜像是否占用我的镜像名额？ {#section_agd_2qc_ghb .section}

不占用。

## 使用共享镜像创建实例的时候存不存在地域限制？ {#section_mls_2qc_ghb .section}

有地域限制。同一个共享源，地域也应该相同。

## 使用共享镜像创建实例存在什么样的风险？ {#section_p4w_lqc_ghb .section}

镜像拥有者可以查看该镜像的共享关系，也可以删除该镜像。共享镜像被拥有者删除后，会导致使用共享镜像的ECS实例不能重新初始化系统盘。

阿里云不保证其他账号共享镜像的完整性和安全性，使用共享镜像时您需要自行承担风险，请您选择信任的账号共享的镜像。使用共享镜像创建ECS实例时，您需要登录该ECS实例检查一下共享镜像的安全性和完整性。

## 我把自定义镜像共享给其他账号，存在什么风险？ {#section_r4q_nqc_ghb .section}

有数据泄露和软件泄露的风险。在共享给其他账号之前，请确认该镜像上是否存在敏感的和安全的重要数据和软件。得到您的共享镜像的账号，可以用这个共享镜像创建ECS实例，还可以用这个ECS实例创建更多自定义镜像，其中的数据会不停传播，造成泄露风险。

## 我能把别人共享给我的镜像再共享给其他人吗？ {#section_abm_4qc_ghb .section}

不能。只有镜像的拥有者才能共享给其他账号。

## 我把镜像共享给他人，还能使用该镜像创建实例吗？ {#section_xny_pqc_ghb .section}

可以。您将镜像共享给其他账号后，还可以用该镜像创建ECS实例，在该ECS实例的基础上也可以继续创建自定义镜像。

## 华北地域服务器A制作的镜像能共享给华东地域的服务器B吗？ {#section_b5i_fn9_i06 .section}

-   如果服务器A与B属于同一账号，可直接复制镜像到华东地域给服务器B使用。详情请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)。
-   如果服务器A与B属于不同的账号，可先复制镜像到华东地域再共享给服务器B的账号。详情请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)和[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。

## 为何没有导出镜像的入口？ {#section_j80_1pu_tv2 .section}

您需要提交工单申请导出镜像的权限，详情请参见[导出镜像](intl.zh-CN/镜像/自定义镜像/导出镜像.md#)。

## 我想将镜像导出到本地进行测试，具体要怎么操作呢？ {#section_9dl_9cs_oba .section}

目前镜像文件的导出格式默认为.raw.tar.gz，解压后为.raw格式，您可以搜索下该格式镜像的相关使用资料来使用，阿里云并未做特殊限制。

## 如果使用自定义镜像创建了ECS实例，我可以删除这个镜像吗？ {#section_lvj_dht_8a4 .section}

您可以**强制删除**这个镜像。但是，删除镜像后，使用该自定义镜像创建的ECS实例无法重新初始化云盘，详情请参见[重新初始化云盘](intl.zh-CN/块存储/云盘/重新初始化云盘/重新初始化系统盘.md#)。

## 我曾把自己账号中的某个自定义镜像共享给其他账号，现在我可以删除这个镜像吗？ {#section_fqt_49s_s3v .section}

可以删除。但是当您删除共享镜像后，使用该共享镜像创建的ECS实例都不能重新初始化系统盘。所以，建议您把该自定义镜像的所有关系删除后再删除镜像。

## 我把某个自定义镜像（M）的共享账号（A）给删除了，会有什么影响？ {#section_qn6_1dm_1tn .section}

您将无法通过ECS控制台或者ECS API查询到共享镜像M。无法使用镜像M创建ECS实例和更换系统盘。如果账号A在删除共享关系前，使用镜像M创建了ECS实例，那么这些实例将不能重新初始化系统盘。

## 删除镜像的时候提示“指定的镜像Id还存在保有实例，不能删除该镜像”，为什么？ {#section_qe9_38d_hvk .section}

您可能使用快照创建了镜像。如果想删除镜像，必须选择**强制删除**。强制删除镜像后，不会影响现有实例的使用，但是使用该自定义镜像创建的ECS实例无法重新初始化云盘，详情请参见[删除自定义镜像](intl.zh-CN/镜像/自定义镜像/删除自定义镜像.md#)。

## 更换系统盘时，选择的镜像中包含数据盘的话，能通过更换系统盘实现更换镜像吗？ {#section_053_0tw_h6a .section}

不能。如果必须要使用这个镜像，建议您使用该镜像创建一个按量付费的ECS实例，为系统盘创建快照，然后再通过该快照创建只包含系统盘的自定义镜像，最后更换系统盘时选择该自定义镜像。

## 我目前有一台ECS服务器，想用现有的镜像来更换这台ECS的操作系统，怎么操作？ {#section_69i_52e_jfd .section}

使用现有镜像更换ECS实例操作系统的具体步骤，请参见[更换操作系统](intl.zh-CN/镜像/更换操作系统.md#)。

**说明：** 建议您操作之前创建快照备份数据。

## 账号A的服务器制作镜像后，能给账号B更换磁盘用吗？ {#section_oww_crp_0j9 .section}

您需要先共享镜像给账号B，然后再更换磁盘。共享镜像，请参见[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。

**说明：** 用于更换系统盘的镜像中，只能包含系统盘。

## 为什么创建实例时自定义镜像的配置费用高于公共镜像？ {#section_k04_yg7_uoa .section}

以下任一原因均可导致自定义镜像的配置费用高于公共镜像。

-   自定义镜像中包含数据盘。创建实例时，数据盘产生的费用，导致自定义镜像总费用高于相应的公共镜像。
-   自定义镜像基于付费公共镜像（如Windows Server、Redhat Enterprise Linux等）创建。

## 镜像市场的镜像有哪些功能？ {#section_8wl_8ju_9pi .section}

镜像市场的镜像在操作系统基础上预装了软件环境和多种功能，例如PHP/.NET/JAVA/LAMP等运行环境、控制面板、建站系统等。将镜像与云服务器配套使用,您只需进行一次简单操作，就可快速部署云服务器的运行环境或软件应用,再也不担心上云难了。

## 镜像市场的镜像能带来哪些便利？ {#section_c0p_y2e_36h .section}

通过镜像市场的镜像开通云服务器ECS，一键部署，您即可获得与镜像一致的系统环境或软件，便捷地创建已就绪的运行环境，同时轻松地搭建并管理站点。无需自行配置环境、安装软件。

## 目前镜像市场的镜像支持哪些服务器环境和应用场景？ {#section_4aa_s13_huj .section}

镜像市场提供上百款优质第三方镜像，不仅全面支持PHP/.NET/JAVA/LAMP/Docke虚拟容器等运行环境的部署，而且满足建站、应用开发、可视化管理等个性化需求。

## 镜像市场的镜像是否安全？ {#section_hng_971_32q .section}

镜像服务商均有丰富的系统维护和环境配置经验，所有镜像都基于包含云盾的阿里云官方操作系统制作，且预先经过严格安全审核，敬请放心使用。

## 镜像市场的镜像安装使用过程中出问题了怎么办？ {#section_jyl_7r1_85r .section}

查看购买页的服务信息，通过在线旺旺、电话或邮箱直接与镜像服务商联系，实时解答您的疑问。

## 如何购买镜像市场镜像？ {#section_hxc_rqc_ghb .section}

您可以在镜像市场单独购买，也可以在ECS售卖页面和ECS实例同时购买。

## 按次购买的镜像的使用期限是多久？ {#section_hqw_prc_ghb .section}

原则上可以一直使用，但要需要注意，镜像作为一种软件有自身的生命周期，另外服务商提供的服务支持实际上是有期限的，具体应以商品上的描述为准。

## 镜像市场的镜像支持退款吗？ {#section_gzm_qrc_ghb .section}

镜像按照云市场统一规则支持有限时间内无理由退款，但出现以下情况时不予退款。

-   在无理由退款时限内将购买的镜像部署在了云服务器上。
-   在提交退款的申请审批确认前，将购买的镜像部署在了云服务器上。
-   也就是说，镜像在不被使用的状态下可以退款。

## 镜像市场商业化后，还有免费的镜像市场镜像吗？ {#section_okl_src_ghb .section}

镜像市场还会存在一定数量的免费的镜像，可以放心使用。0元的镜像也需要购买后才能使用。

## 在杭州买了一个镜像市场的镜像，能否在北京创建ECS实例或者更换系统盘？ {#section_ndz_src_ghb .section}

不可以，购买的镜像市场镜像只能在相同地域进行创建ECS实例或者更换系统盘。

## ECS实例使用镜像市场的镜像，升级和续费ECS实例，需要为镜像继续付费吗？ {#section_jwc_fsx_fhb .section}

不需要付费。购买一个镜像可以一直在ECS实例上使用，无需再续费。

## ECS实例使用镜像市场的镜像，实例释放后，继续购买ECS实例还可以免费使用该镜像吗？ {#section_yqb_wrc_ghb .section}

可以。

## 使用镜像市场镜像创建ECS实例，该实例创建一个自定义镜像，使用该自定义镜像创建ECS实例需要为该镜像付费吗？ {#section_pnn_yrc_ghb .section}

需要，价格和原镜像市场的镜像价格相同。

## 来源于镜像市场的镜像复制到其他地域创建ECS实例，是否需要为该镜像付费？ {#section_bqm_zrc_ghb .section}

需要，价格和原镜像市场的镜像价格相同。

## 如果把来源于镜像市场的自定义镜像共享给其他账号（B）创建ECS实例，账号B是否需要为该镜像付费？ {#section_ymk_1sc_ghb .section}

账号B需要支付该镜像费用，价格和原镜像市场的镜像价格相同。

## 如果使用镜像市场的镜像或者来源于镜像市场的镜像进行更换系统盘，需要付费吗？ {#section_uj5_1sc_ghb .section}

需要看情况，如果当前的ECS实例使用的镜像和您要更换的镜像属于同一个镜像商品的不同版本的镜像，是不需要付费的，否则是需要付费的。

## ECS实例正在使用镜像市场的镜像，进行重置系统盘需要收费吗？ {#section_nj4_bsc_ghb .section}

不会。

## 怎么调用ECS API，使用镜像市场镜像或者来源镜像市场的自定义镜像或者共享镜像，创建ECS实例和更换系统盘？ {#section_xl1_csc_ghb .section}

1.  确认使用的镜像ID是镜像市场镜像或者是来源为镜像市场的镜像，调用DescribeImages查询到镜像的相关信息。

    如果您使用的镜像的镜像商品标示（`ProductCode`）不为空，表示该镜像是镜像市场的镜像或者来源于镜像市场的自定义镜像或者共享镜像。如果使用的镜像的商品标示ProductCode为abcd000111，您可以访问镜像商品的地址`http://market.aliyun.com/products/123/abcd000111.html`。

2.  需要选择镜像的版本和正确地域，只购买ECS镜像。

    购买某一地域的镜像，只能在该地域的ECS实例上使用。当前每次只能购买一个镜像，如果需要创建多个ECS实例，则需要购买多个镜像。

3.  购买完成后，您可以创建ECS实例和更换系统盘。

## 如果没有购买镜像市场的镜像或者来源于镜像市场的镜像，在调用ECS API使用该镜像创建ECS实例和更换系统盘，会报错吗？ {#section_sxt_hsc_ghb .section}

会报错，错误码为`QuotaExceed.BuyImage`。

## 我的ESS是自动创建机器的，并且量是不固定，设置最小值为10台，最大值为100台，那么使用镜像市场的镜像如何保证我的的需求实例能正常弹出来？ {#section_nfx_5sc_ghb .section}

如果您需要弹出n台同类型的镜像，您需要提前购买n台镜像市场的镜像。

## 镜像市场的镜像是否支持批量购买？ {#section_clp_ysc_ghb .section}

暂不支持批量购买。

## 如果之前使用的镜像市场的镜像，已不存在该商品（如：jxsc000010、jxsc000019），怎能保证已经设置的弹性伸缩组的机器能正常弹出？ {#section_stt_zsc_ghb .section}

此情况建议您选择镜像市场中可替代的镜像进行替代。

## 1个product code能否支持不同region的镜像？ {#section_os3_btc_ghb .section}

支持，前提是该地域region已经支持该商品镜像。

## 我买了100 product code同样值的镜像，是否可以支持在所有的地域可用？ {#section_uzj_ctc_ghb .section}

目前镜像市场的镜像已经具备region属性，请您购买相应地域的镜像。

## 勾选“I/O优化实例”选项导致购买ECS实例时无法选择镜像市场的镜像，为什么？怎么解决？ {#section_tch_39p_cv5 .section}

有关该问题的分析及解决方案如下：

-   问题现象：在阿里云官网购买ECS实例，选择镜像时，发现无法选取任何镜像市场的镜像。
-   原因分析：该问题可能是由于购买ECS实例时，勾选了**I/O优化实例**选项导致的。

    与普通ECS实例相比，I/O优化实例可在实例与云盘之间提供更好的网络能力，可保证SSD云盘存储发挥最高性能。由于相关优化操作涉及网络、存储和镜像内部相关驱动等，因此并非所有镜像都能支持I/O优化实例。

-   解决方法：购买I/O优化实例时，建议您选择实例支持的官方标准镜像，再自行部署相关业务环境。

如问题依然未解决,请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。

## 什么是镜像市场的包年包月和按周付费镜像？ {#section_zxy_n5c_ghb .section}

镜像市场的包年包月和按周付费镜像是指从阿里云云市场购买的，按周、按月或按年付费使用的镜像。这些镜像由镜像供应商开发并维护，所有售前咨询和售后服务都由镜像供应商提供。在本文中，这类镜像统称为预付费镜像。

## 预付费镜像能与哪种ECS实例搭配使用？ {#section_fts_45c_ghb .section}

预付费镜像只能与包年包月实例和按周付费实例搭配使用，而且镜像与ECS实例的付费周期应保持一致。

## 怎么购买预付费镜像？可以单独购买吗？ {#section_rfp_s5c_ghb .section}

目前您还不能单独购买预付费镜像。

您可以选择以下任一种方式购买预付费镜像：

-   在创建ECS实例时，付费方式选择**包年包月**，并从**镜像市场**选择镜像，再选择按周、按月或按年付费。

    **说明：** 在这种情况下，您需要同时支付实例与镜像的费用。如果实例创建成功，表明您已经同时支付了实例与镜像的费用，不会出现其中一项资源购买失败的情况。

-   如果您想在一台已有的包年包月或按周付费ECS实例上使用预付费镜像，您可以使用更换操作系统功能将操作系统更换为预付费镜像，此时，您只能按照ECS实例的付费周期选择镜像的付费周期。具体操作方式，请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

    **说明：** 在这种情况下，您只需要支付镜像的费用。


## 预付费镜像怎么付费？ {#section_xhj_w5c_ghb .section}

预付费镜像采用预付费，付费周期应与使用它的包年包月或按周付费ECS实例保持一致。

镜像的价格以供应商提供的信息为准。

## 预付费镜像到期了就不能用了吗？怎么继续使用？ {#section_cc4_x5c_ghb .section}

预付费镜像到期后，如果没有及时续费就不能再使用。

您不能单独为预付费镜像续费。如果要继续使用，您可以在为ECS实例续费的同时为镜像续费。续费后，可以继续使用镜像。

## 购买预付费镜像后，如果我不想再使用这个镜像，能要求退款吗？ {#section_gwb_z5c_ghb .section}

能否退款由镜像供应商决定。您可以在购买之前咨询镜像供应商。

## 退款时，费用怎么结算？ {#section_hvt_z5c_ghb .section}

如果可以退款，镜像供应商将按照您的实际使用情况退款。

## 预付费镜像能转换为按量付费镜像吗？ {#section_hpg_1vc_ghb .section}

目前不支持转换为按量付费镜像。后续我们会提供这个功能，具体时间请关注阿里云官网公告。

## 预付费镜像与其它镜像之间能互换吗？更换后费用怎么计算？ {#section_sqw_1vc_ghb .section}

可以。您可以通过ECS实例更换系统盘来更换镜像。更换镜像时有以下几种选择：

-   将其他类别的镜像（如公共镜像、自定义镜像、共享镜像）换成预付费镜像：更换后，系统将按镜像的费用和ECS实例的剩余付费周期计算实际费用。
-   将预付费镜像换成其它类别的镜像（如公共镜像、自定义镜像、共享镜像）：如果供应商允许退款，镜像供应商将按照您的实际使用情况退款。
-   将一个预付费镜像（设为镜像A）换成另一个预付费镜像（设为镜像B）：更换后，如果镜像 A 允许退款，将按退款方式结算费用，镜像B将按镜像的价格和ECS实例剩余付费周期计算实际费用。

## 在哪里查看并管理我购买的预付费镜像？ {#section_fmx_fvc_ghb .section}

您可以登录[ECS管理控制台](https://ecs.console.aliyun.com)，在**镜像** \> **镜像市场**中查看并管理您购买的预付费镜像。

## 使用预付费镜像制作的自定义镜像会收费吗？预付费镜像过期对于自定义镜像有什么影响？ {#section_klq_gvc_ghb .section}

当您使用由预付费镜像制作的自定义镜像时，无论是使用自定义镜像创建实例，还是更换系统盘，都是重新在镜像市场下单购买镜像的使用权。所以，用于制作自定义镜像的预付费镜像是否过期，对使用自定义镜像没有影响。

## 为什么有的ECS实例无法选择Windows操作系统？ {#section_ajg_qwc_ghb .section}

使用Windows 操作系统创建ECS实例时，需要确保实例内存大于等于1GiB。内存低于1GiB的ECS实例（例如， 512MiB）只能选择Linux镜像和Windows Server 1709镜像。

## ECS实例使用操作系统需要付费吗？ {#section_ttw_qwc_ghb .section}

大陆地域的Windows Server公共镜像自带正版激活，不收取系统正版激活费用，其他国家或地区地域会收取系统正版激活费用。

Windows Server 公共镜像默认最多允许2个会话（Session）[远程连接](../intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)，如果您新增连接数，请向微软单独购买远程桌面授权（RD授权）服务，该项授权费用需要您自理。

除Red Hat公共镜像外，Linux公共镜像不需要您支付版权费用。

## 我能自己安装或者升级操作系统吗？ {#section_zhs_twc_ghb .section}

不能自行安装或升级。ECS实例需要使用阿里云官方提供的镜像，您无法自行添加或升级。但是您可以进行下列操作：

-   更换系统盘重新选择操作系统。具体操作步骤，请参见[更换操作系统](../intl.zh-CN/镜像/更换操作系统.md#)。
-   从本地导入自己的镜像后使用自定义镜像创建ECS实例。导入镜像的操作步骤，请参见[导入镜像必读](../intl.zh-CN/镜像/自定义镜像/导入镜像/导入镜像必读.md#)。使用自定义镜像创建ECS实例的操作步骤，请参见[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。
-   为操作系统打补丁。

## 操作系统是否有图形界面？ {#section_ulp_xwc_ghb .section}

除Windows Server半年渠道实例以外，Windows操作系统是桌面管理形式。有关如何使用Windows Server半年渠道操作系统，请参见[Windows Server半年渠道镜像与实例管理](intl.zh-CN/镜像/常见问题/Windows Server半年渠道镜像与实例管理.md#)。

Linux 操作系统是命令行形式，您可以根据需要安装图形化桌面。

## 如何选择操作系统？ {#section_wqy_zwc_ghb .section}

选择操作系统，请参见[选择镜像](intl.zh-CN/镜像/选择镜像.md#)。

## 公共镜像自带FTP上传吗？ {#section_jtv_dxc_ghb .section}

不自带，需要您自己安装配置。具体操作，请参见[Windows实例搭建FTP站点](../intl.zh-CN/建站教程/搭建FTP站点/Windows实例搭建FTP站点.md#)和[Linux实例搭建FTP站点](../intl.zh-CN/建站教程/搭建FTP站点/Linux实例搭建FTP站点.md#)。

## 阿里云支持哪些SUSE版本？ {#section_mgc_fxc_ghb .section}

目前，阿里云公共镜像支持以下SUSE版本：

-   SUSE Linux Enterprise Server 12 SP4 64位
-   SUSE Linux Enterprise Server 12 SP2 64位
-   SUSE Linux Enterprise Server 11 SP4 64位

## SUSE操作系统提供哪些服务支持？ {#section_jpr_fxc_ghb .section}

阿里云线上售卖的SLES（SUSE Linux Enterprise Server）操作系统会与SUSE更新源保持定时同步。使用阿里云 SLES公共镜像创建的实例，其操作系统的支持服务涵盖在阿里云的企业级别支持服务中。如果您购买了企业级支持服务，可以提交工单联系阿里云获取帮助，阿里云工程师团队会协助您解决SLES操作系统上发生的问题。

## ECS实例到期释放后，如果这个实例之前手动制作了镜像快照，能不能找回之前实例的数据？ {#section_uj1_il5_0xb .section}

可以。您可通过以下任一方式找回实例数据：

-   使用之前制作的镜像创建新实例。具体步骤，请参见[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。
-   使用之前制作的镜像为当前实例更换系统盘。具体步骤，请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

    **说明：** 更换系统盘操作须注意以下两点：

    -   当前实例系统盘的内容会全部丢失，恢复为镜像的状态。
    -   镜像必须和您当前实例位于同一地域。

## 我先有一台ECS实例，想再买一台ECS实例并使用现有这台ECS实例的镜像部署，应该如何操作？ {#section_d2a_pl9_3vq .section}

您可以为之前的ECS实例创建自定义镜像，然后使用该自定义镜像创建ECS实例即可。具体步骤，请参见[使用实例创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)和[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。

## 我已经购买了新的ECS服务器，如何把我的共享镜像恢复到这台新购ECS服务器上？ {#section_54f_mg4_r2p .section}

请确保您已将镜像共享给新购服务器的账号，并根据实际情况选择下列方法之一进行操作。

-   如果共享镜像和新购服务器在同一个地域，可以更换系统盘，更换时选择您共享的镜像即可。具体步骤，请参见[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。
-   如果共享镜像和新购服务器不在同一个地域，需要先复制镜像到目标地域，再通过更换系统盘来更换镜像。 具体步骤，请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)和[更换系统盘（非公共镜像）](../intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

**说明：** 更换系统盘存在如下风险：

-   原系统盘会被释放，建议您提前创建快照备份数据。
-   更换系统盘需要停止实例，因此会中断您的业务。
-   更换系统盘完成后，您需要在新的系统盘中重新部署业务运行环境，有可能会对您的业务造成长时间的中断。
-   更换系统盘是重新为您的实例分配一个系统盘，磁盘ID会改变，所以基于旧的系统盘创建的快照将不能用于回滚新的系统盘。

## 实例的操作系统为Windows Server 2008 R2企业版，现在说Windows副本不是正版怎么办？ {#section_dcb_fs7_ljf .section}

您可以按照以下步骤操作：

1.  激活Windows，详情请参见[VPC环境下ECS Windows系统激活方法](https://www.alibabacloud.com/help/faq-detail/41056.htm)。

    **说明：** 操作之前请先关闭您实例的防火墙。

2.  正版激活后，登录ECS控制台。
3.  通过控制台的远程连接功能连接到该服务器，下载并安装补丁到您的服务器。详情请参见[登录Windows实例报错：The function requested is not supported](https://www.alibabacloud.com/help/faq-detail/71931.htm)（微软官方2018年5月更新了凭据安全支持提供程序协议（CredSSP）相关补丁和身份验证请求方式）。

## 我在阿里云有多个账号，想把账号A的一台服务器转移到账号B，或者用账号B购买一台服务器，通过镜像把服务器运行环境、所有安装应用迁移到账号B的服务器。怎么操作？ {#section_cvk_0gm_ods .section}

您可以通过下列步骤操作：

1.  使用账号A的实例创建自定义镜像。具体步骤，请参见[使用实例创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。
2.  共享镜像给账号B。具体步骤，请参见[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。
3.  账号B使用共享镜像创建实例。具体步骤，请参见[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)。

## 阿里云ECS实例之间如何迁移？ {#section_pkf_2xq_13z .section}

阿里云ECS实例间迁移步骤如下：

1.  为源ECS实例创建自定义镜像。
2.  根据源ECS实例与目标ECS实例的归属地域和归属账号，迁移分为以下几种情况。
    -   源实例与目标实例属于同地域同账号，可直接进入下一步。
    -   源实例与目标实例属于不同地域，需复制镜像至目标实例所在地域。详情请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)。
    -   源实例与目标实例属于不同账号，需共享镜像给目标实例的账号。详情请参见[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。
    -   源实例与目标实例属于不同地域和不同账号，需先复制镜像到目标地域，再分享给目标实例的账号。详情请参见[复制镜像](intl.zh-CN/镜像/自定义镜像/复制镜像.md#)和[共享镜像](intl.zh-CN/镜像/自定义镜像/共享镜像.md#)。
3.  使用镜像创建新的ECS实例，或为现有目标ECS实例更换镜像。详情请参见[使用自定义镜像创建实例](../intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md#)[更换操作系统（镜像）](intl.zh-CN/镜像/更换操作系统.md#)。

    **说明：** 为现有目标ECS实例更换镜像时，源镜像中不能包含数据盘快照。


以上迁移步骤不适用时，请参见[阿里云ECS实例间迁移](../intl.zh-CN/迁移服务/迁移教程/各源环境的迁移/阿里云ECS实例间迁移.md#)。

## 两个不同专有网络下的ECS服务器能否实现网络互通？ {#section_lqt_tci_xa6 .section}

内网互通可以通过高速通道和云企业网实现，详情请参见[同账号VPC互连](../../../../../intl.zh-CN/专有网络对等连接（关闭新购）/同账号VPC互连.md#)和[同账号跨地域VPC和VBR互通](../../../../../intl.zh-CN/快速入门/同账号跨地域VPC和VBR互通.md#)。

## 如何处理CentOS DNS解析超时？ {#section_x8y_les_u5u .section}

处理CentOS DNS解析超时的详情如下：

-   原因分析

    因CentOS 6和CentOS 7的DNS解析机制变动，导致2017年2月22日以前创建的ECS实例或使用2017年2月22日以前的自定义镜像创建的CentOS 6和CentOS 7实例可能出现DNS解析超时的情况。

-   解决方法

    请按下列步骤操作修复此问题：

    1.  下载脚本[fix\_dns.sh](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59344/cn_zh/1505957231428/fix_dns%20%281%29.sh)。
    2.  将下载的脚本放至CentOS系统的/tmp目录下。
    3.  运行bash /tmp/fix\_dns.sh命令，执行脚本。
-   脚本作用

    判断DNS解析文件/etc/resolv.conf中是否存在`options`\>`single-request-reope`配置。详情请参见[resolv.conf文件说明](http://man7.org/linux/man-pages/man5/resolv.conf.5.html)。

    CentOS 6和CentOS 7的DNS解析机制，使用相同的网络五元组发送IPV4 DNS请求和IPV6 DNS请求，此时应开启`single-request-reopen`配置。开启该配置后，一旦需要处理同一socket发送的两次请求时，解析端会在发送第一次请求后关闭socket，并在发送第二次请求前打开新的socket。配置成功后，无需重启实例即可生效。

-   脚本逻辑
    1.  判断实例系统是否为CentOS。
        -   如果实例为非CentOS系统（如Ubuntu和Debian）：脚本停止工作。
        -   如果实例为CentOS系统：脚本继续工作。
    2.  查询解析文件/etc/resolv.conf中`options`的配置情况。
        -   如果不存在`options`配置：

            默认使用阿里云`options`配置`options timeout:2 attempts:3 rotate single-request-reopen`。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592664646335_zh-CN.png)

        -   如果存在`options`配置：
            -   不存在`single-request-reopen`配置，则在`options`配置中追加该项。
            -   存在`single-request-reopen`配置，则脚本停止工作，不更改DNS nameserver的配置。

## 为什么ECS默认没有启用虚拟内存或Swap说明？ {#section_m02_5j5_qf2 .section}

Swap分区或虚拟内存文件，是在系统物理内存不够用的时候，由系统内存管理程序将那些很长时间没有操作的内存数据，临时保存到Swap分区虚拟内存文件中，以提高可用内存额度的一种机制。

但是，如果在内存使用率已经非常高，而同时I/O性能也不是很好的情况下，该机制其实会起到相反的效果。阿里云ECS云磁盘使用了分布式文件系统作为云服务器的存储，对每一份数据都进行了强一致的多份拷贝。该机制在保证用户数据安全的同时，由于3倍增涨的I/O操作，会降低本地磁盘的存储性能和I/O性能。

综上，为了避免当系统资源不足时进一步降低ECS云磁盘的I/O性能，所以ECS Windows默认没有启用虚拟内存，Linux默认未配置Swap分区。

## 如何在阿里云公共镜像中开启kdump？ {#section_kwb_4l4_a16 .section}

阿里云公共镜像中默认未开启kdump服务。若您需要实例在宕机时，生成core文件，并以此分析宕机原因，请参见以下步骤开启kdump服务。本步骤以公共镜像CentOS 7.2为例。实际操作时，请以您的操作系统为准。

1.  设置core文件生成目录。
    1.  运行vim /etc/kdump.conf打开kdump配置文件。
    2.  设置path为core文件的生成目录。本示例中，在/var/crash目录下生成core文件，则path的设置如下。

        ``` {#codeblock_byw_zlj_cgy}
        path /var/crash
        ```

    3.  保存并关闭/etc/kdump.conf文件。
2.  开启kdump服务。

    根据操作系统对命令的支持情况，选择开启方式。本示例中，CentOS 7.2使用方法一开启kdump服务。

    -   方法一： 依次运行以下命令开启kdump服务。

        ``` {#codeblock_w71_exg_1n3}
        systemctl enable kdump.service
        ```

        ``` {#codeblock_7kv_srv_lo0}
        systemctl start kdump.service
        ```

    -   方法二： 依次运行以下命令开启kdump服务。

        ``` {#codeblock_5j6_cgy_ptj}
        chkconfig kdump on
        ```

        ``` {#codeblock_m5w_zz9_974}
        service kdump start
        ```

3.  运行以下命令模拟宕机。

    ``` {#codeblock_wsl_49j_a81}
    echo c > /proc/sysrq-trigger
    ```

    **说明：** 运行该命令后，实例会与网络失去连接。您需要重新连接实例，完成后续操作。

4.  分析core dump文件。
    1.  运行以下命令安装Crash分析工具。

        ``` {#codeblock_a42_yzr_9lt}
        yum install crash
        ```

    2.  下载debug-info安装包。

        运行uname -r命令查看操作系统内核版本，下载相应版本的debug-info包。

        -   kernel-debuginfo-common-x86\_64-<内核版本\>.rpm
        -   kernel-debuginfo-<内核版本\>.rpm
        本示例中，系统的内核版本为`3.10.0-514.26.2.el7.x86_64`，因此下载命令为：

        ``` {#codeblock_uu7_oll_461}
        wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-common-x86_64-3.10.0-514.26.2.el7.x86_64.rpm
        ```

        ``` {#codeblock_kl2_nry_iaq}
        wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-3.10.0-514.26.2.el7.x86_64.rpm
        ```

    3.  依次运行下列命令，安装debug-info包。

        ``` {#codeblock_ytx_y7p_nrx}
        rpm -ivh kernel-debuginfo-common-x86_64-3.10.0-514.26.2.el7.x86_64.rpm
        ```

        ``` {#codeblock_6gk_8um_zil}
        rpm -ivh kernel-debuginfo-3.10.0-514.26.2.el7.x86_64.rpm
        ```

    4.  依次运行以下命令使用Crash工具分析core文件。

        ``` {#codeblock_2dc_m8n_36o}
        cd <core文件的生成目录>
        ```

        ``` {#codeblock_m03_lyk_a4y}
        crash /usr/lib/debug/lib/modules/<内核版本号>/vmlinux vmcore
        ```

        本示例中，core文件的生成目录为/var/crash/127.0.0.1-2019-07-08-15:52:25，内核版本号为`3.10.0-514.26.2.el7.x86_64`，因此运行的命令为：

        ``` {#codeblock_005_ola_62z}
        cd /var/crash/127.0.0.1-2019-07-08-15:52:25
        ```

        ``` {#codeblock_xga_w1x_m7d}
        crash /usr/lib/debug/lib/modules/3.10.0-514.26.2.el7.x86_64/vmlinux vmcore
        ```


## Linux镜像如何开启或关闭Meltdown与Spectre安全漏洞补丁？ {#section_mf9_75m_jnp .section}

安全漏洞的背景信息、涉及的公共镜像以及开启或关闭安全漏洞补丁的方法，请参见[Linux镜像如何开启或关闭Meltdown与Spectre安全漏洞补丁](intl.zh-CN/镜像/常见问题/Linux镜像如何开启或关闭Meltdown与Spectre安全漏洞补丁.md#)。

## 如何检查与修复CentOS 7实例和Windows实例IP地址缺失问题？ {#section_29l_kc7_8hw .section}

问题原因及解决方案，请参见[检查与修复CentOS 7实例和Windows实例IP地址缺失问题](https://www.alibabacloud.com/help/doc-detail/94181.html)。

