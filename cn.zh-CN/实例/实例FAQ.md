# 实例FAQ {#concept_gqy_fyx_wgb .concept}

本文汇总了使用云服务器ECS实例时的常见问题。

-   购买实例问题
    -   [如何查看某个地域或可用区是否能购买实例？](#section_dxe_iha_q0o)
    -   [购买实例时，资源已经售罄怎么办？](#section_lxw_bwz_qgb)
    -   [如何选择适合我业务的ECS实例？](#section_j8t_fwz_mjf)
    -   [购买ECS实例如何付款？](#section_huh_ipu_6gt)
    -   [开通一台云服务器需要多久？](#section_ska_yf3_rvx)
    -   [购买实例付款成功，但是没有生成实例，为什么？](#section_gbw_acs_xwn)
    -   [为什么购买实例时看不到按量付费资源？](#section_ls5_e9e_kt3)
-   企业级实例问题
    -   [什么是企业级实例？什么是入门级实例？](#section_2p8_osd_e5y)
    -   [企业级实例与入门级实例有什么本质区别？](#section_cm4_dks_zu1)
    -   [哪些是企业级实例？哪些是入门级实例？](#section_y0w_qjj_s3o)
    -   [在什么业务场景下，我需要购买企业级实例？](#section_8gs_zby_36p)
    -   [企业级实例的网络性能怎么样？](#section_omt_o32_8lt)
    -   [企业级实例支持哪几种云盘类型？](#section_9st_mh4_j3f)
    -   [企业级实例支持哪些类型的镜像？](#section_h1y_jjt_aer)
    -   [企业级实例规格变配有什么限制？](#section_rxb_abg_ub7)
    -   [入门级实例能否变配为企业级实例？](#section_90e_qq9_gmf)
-   GPU实例问题
    -   [为什么Nvidia驱动安装成功后，但是nvidia-smi无效，显示驱动未安装？](#section_6fo_f6k_wy9)
    -   [为什么gn5和gn5i的Windows实例安装官网驱动时断网？](#section_6ww_806_shg)
    -   [为什么Windows图形不支持DirectX等功能？](#section_5mx_en9_guy)
    -   [为什么ga1实例使用云市场预装AMD驱动的镜像，但是进入Windows设备管理器时显示GPU驱动未能正常加载？](#section_myh_mu2_r7g)
    -   [为什么使用云市场预装AMD驱动的镜像，启动实例时蓝屏？](#section_593_bs5_c1l)
    -   [GPU实例支持安卓模拟器吗？](#section_vwn_31g_4fn)
    -   [我能变更GPU云服务器的配置吗？](#section_sbj_dzq_gb1)
    -   [按量付费GPU云服务器支持停机不收费功能吗？](#section_pw6_mpa_a0f)
    -   [如何查看GPU监控数据？](#section_lv4_gwl_r5e)
-   弹性裸金属服务器问题
    -   [弹性裸金属服务器和传统云主机（虚拟机）和传统物理机有何本质区别？](#section_m7m_pvm_64b)
    -   [弹性裸金属服务器的网络性能怎么样？](#section_mtz_x6v_4v4)
    -   [弹性裸金属服务器支持哪些磁盘类型？可以挂载多少块数据盘？](#section_gu1_xmv_r8f)
    -   [弹性裸金属服务器是否支持规格变配和宕机迁移？](#section_qzc_rb4_og4)
-   超级计算集群（SCC）问题
    -   [如何创建SCC实例？](#section_9as_2qf_ted)
    -   [SCC实例如何计费？](#section_lew_64d_19y)
    -   [如何使用E-HPC创建SCC集群？](#section_pq2_wpe_y7q)
    -   [如何使用SCC RDMA功能？](#section_i2x_rle_0ql)
-   抢占式实例问题
    -   [我没有欠费，为什么抢占式实例被释放了？](#section_0ns_pj7_dxg)
    -   [抢占式实例被释放时会有通知吗？怎么通知？](#section_b3n_69r_ccj)
    -   [抢占式实例被释放后数据能自动保留吗？](#section_hqu_m54_1ac)
    -   [我已经设置了抢占式实例释放时间，能取消或者调整吗？](#section_4dz_4mk_utb)
    -   [抢占式实例能转为包年包月实例吗？](#section_4bx_hwo_gre)
    -   [抢占式实例的价格折扣包括了哪些资源？](#section_ns2_1jv_mbr)
    -   [怎么对抢占式实例出价？](#section_vv0_a6s_5zd)
    -   [抢占式实例的最高出价和当前市场价格有什么关系？](#section_67i_s25_aqc)
    -   [在同一时间启动的所有抢占式实例是否收取同样的费用？](#section_y3x_sk2_stu)
    -   [抢占式实例运行后一小时内，我支付的费用会随市场价格的变动而变化吗？](#section_scn_g76_t1n)
    -   [在购买抢占式实例前我能看到当前的市场价格吗？](#section_jxg_3ko_6xo)
    -   [我能查看抢占式实例规格的历史价格吗？怎么查看？](#section_z9a_do7_ofi)
    -   [抢占式实例停止后会继续收费吗？](#section_8yt_11m_q7i)
    -   [怎么查看抢占式实例消费明细？](#section_jg4_24g_j0e)
    -   [一个账号可以购买多少台抢占式实例？](#section_d2v_giu_8a4)
    -   [怎么提高vCPU的配额？](#section_u2j_bsw_7vd)
    -   [抢占式实例支持变更实例规格吗？](#section_yae_a2y_k7c)
    -   [哪些ECS实例规格族支持抢占式实例？](#section_8ws_4pm_9cc)
    -   [哪些地域支持抢占式实例？](#section_0zt_ehb_pts)
-   预留实例券问题
    -   [什么是预留实例券？](#section_et2_64u_fmh)
    -   [预留实例券能否提供库存预留？](#section_5g6_eu4_b0f)
    -   [预留实例券支持什么操作系统？](#section_xoy_vzx_szv)
    -   [哪些规格族能够使用预留实例券？](#section_j7h_12a_tuy)
    -   [预留实例券能否抵扣抢占式实例的账单？](#section_m9r_qk6_39q)
    -   [可以调整预留实例券的实例规格族吗？](#section_uee_304_jt3)
    -   [什么场景购买可用区级预留实例券？](#section_wcp_t5l_01b)
    -   [什么场景购买地域级预留实例券？](#section_rym_4rw_cl5)
    -   [如何应用可用区灵活性？](#section_6vd_nvw_m73)
    -   [如何应用实例大小灵活性？](#section_i9g_3my_drv)
    -   [可用区级的预留实例券支持实例大小灵活性吗？](#section_tpd_tx9_9ri)
    -   [可用区级的预留实例券支持可用区灵活性吗？](#section_qdz_h5b_f91)
    -   [可用区级预留实例券可以调整为地域级预留实例券吗？](#section_wry_8lc_jj4)
    -   [可以跨地域调整预留实例券的范围吗？](#section_m89_45m_v6k)
    -   [能否跨帐号使用预留实例券？](#section_6ta_i2c_mga)
    -   [预留实例券可以抵扣按量付费实例的存储和网络部分账单吗？](#section_prg_o9w_0de)
    -   [可以控制预留实例券抵扣指定实例的账单吗？](#section_30a_ovt_uhz)
    -   [预留实例券如何计费？](#section_whe_bza_0u2)
    -   [预留实例券购买后的生效时间如何计算？](#section_cdy_tt0_n68)
    -   [预留实例券修改、拆分、合并后的生效时间如何计算？](#section_kfw_q23_shl)
    -   [为什么购买时看不见0预付的选项？](#section_95a_y2p_hcl)
    -   [预留实例券支持修改券的付款类型吗？](#section_1ps_ydr_o6o)
    -   [预留实例券可以退款吗？](#section_vnd_a46_hbz)
    -   [预留实例券可以转售吗？](#section_j9e_1zq_35v)
    -   [Windows类型的预留实例券可以抵扣镜像费用吗？](#section_0w6_6mr_z27)
    -   [Linux类型的预留实例券可以抵扣镜像费用吗？](#section_wm8_tf8_rgx)
-   连接实例问题
    -   [管理终端是独享的吗？](#section_mdm_w4q_wgb)
    -   [忘记了远程连接密码，怎么办？](#section_tym_x4q_wgb)
    -   [为什么修改了远程连接密码还是连不上管理终端？](#section_huk_e8x_b38)
    -   [管理终端提示授权验证失败，怎么解决？](#section_xl9_o6y_79k)
    -   [连接到管理终端后出现黑屏，怎么办？](#section_xrm_6sm_10m)
    -   [管理终端无法访问了，怎么办？](#section_65w_3px_xpu)
    -   [我使用IE8.0，为什么无法使用管理终端？](#section_82j_21b_xj0)
    -   [我用Firefox浏览器打开管理终端会报错安全连接失败，怎么办？](#section_l6t_kik_vmy)
    -   [如何远程登录到Linux实例？](#section_tkz_v77_wbf)
    -   [远程登录实例操作系统时，默认用户名和密码是什么？](#section_u82_ecw_928)
-   升降配实例问题
    -   [我能升级包年包月ECS实例规格和配置吗？](#section_5ap_zkp_361)
    -   [我能升级按量付费ECS实例规格和配置吗？](#section_472_rev_qvi)
    -   [升级ECS实例过程大约需要多久？](#section_ju8_yai_0f9)
    -   [升级ECS实例产生的费用怎么计算？](#section_ckm_8hg_3uy)
    -   [升级ECS实例对我的云上业务的配置有什么影响吗？](#section_s9y_1yw_w5c)
    -   [如何升级ECS资源？](#section_grz_gr2_rve)
    -   [为什么降配时实例预计退款为0？](#section_wrl_689_36t)
    -   [为什么升级实例配置后没有效果？](#section_jsb_os8_bbb)
    -   [升级包年包月实例带宽，为什么提示按使用流量计费的带宽不支持带宽临时升级？](#section_8de_1dx_l78)
-   管理实例问题
    -   [ECS实例长时间为Starting状态，且AliyunService被禁用或被删除怎么办？](#section_3kd_bat_4p4)
    -   [如何通过ECS服务器让OSS支持HTTPS访问？](#section_0mh_dus_4lh)
    -   [如何操作f1实例？](#section_ug1_lb2_d7l)
    -   [macOS如何通过FTP工具上传文件？](#section_39c_w47_rds)
    -   [为什么无法在ECS实例上登录淘宝网？](#section_n4z_oet_sdc)
    -   [购买ECS实例后如何备案域名？](#section_br4_f3k_1jw)
    -   [为什么ECS实例无法加载内核启动？](#section_o58_xbc_j1a)
    -   [如何在实例内部修改登录密码？](#section_5dx_x72_cb8)
    -   [购买了ECS实例，想对ECS实例添加声卡和显卡，且发现无法添加，是什么原因？](#section_lqe_uwn_har)
    -   [可以转移某台ECS剩余使用时间到别的ECS上吗？](#section_nwm_uhx_s6y)
    -   [ECS实例如何查询云服务器IP地址归属地？](#section_uvf_mwq_enl)
    -   [云服务器默认提供数据库吗？](#section_h97_kf4_xjp)
    -   [云服务器上是否可以搭建数据库？](#section_jli_u2y_g3m)
    -   [云服务器是否支持Oracle数据库？](#section_j1b_acd_1f7)
    -   [公网IP和私网IP是否独立，能指定或增加IP吗？](#section_dvt_enw_7gr)
    -   [云服务器能否做负载均衡？](#section_g6s_x91_9m2)
    -   [购买ECS实例后可以更换地域吗？](#section_wm7_rby_mij)
    -   [可以调整已购磁盘的分区大小吗？](#section_nih_446_koq)
    -   [如何将实例的固定公网IP更换为其它EIP？](#section_grq_3gj_n2r)
    -   [如何查看同一地域下的包年包月实例？](#section_bud_chq_gek)
    -   [如何查看同一账号下所有地域的包年包月实例？](#section_s5o_w6z_95z)
    -   [什么时候可以强制停止实例？有什么后果？](#section_nlp_9qg_6gq)
    -   [为什么会重开机失败？](#section_vk6_sjc_agd)
    -   [使用弹性伸缩功能时，伸缩组内ECS实例开启了释放保护，为什么仍然被自动释放了？](#section_so8_gdz_2i5)
-   实例安全问题
    -   [ECS实例中AliVulfix进程是什么？](#section_4ek_d0m_191)
    -   [云服务器能防网络攻击吗？](#section_t6g_7b5_165)
    -   [阿里云安全方面有哪些服务？](#section_cxr_p7b_a9w)
-   Linux实例使用问题
    -   [ECS Linux服务器到期续费后站点无法访问怎么办？](#section_s8j_d1f_1u6)
    -   [如何查询Linux实例的账号和密码？](#section_sri_3o0_prt)
    -   [如何检查Linux实例磁盘和进行分区格式化？](#section_csf_vvp_2z1)
    -   [如何向Linux实例上传文件？](#section_861_wjj_km6)
    -   [如何调整Linux实例目录文件的拥有者和拥有组？](#section_kf0_kn1_74z)
    -   [如何更新Linux实例的软件源？](#section_8jc_uw1_mjn)
    -   [如何在Linux实例上搭建支持PHP的Web环境？](#section_ww2_idc_mq1)
-   实例建站问题
    -   [织梦建站选择什么服务器？](#section_nff_lzp_v4l)
-   实例使用限制问题
    -   [ECS实例转移和更换公网IP地址有什么限制？](#section_y49_iww_fvq)
    -   [云服务器ECS创建多少个网站？](#section_999_02s_59y)
    -   [收到违规信息整改通知邮件如何处理？](#section_ybb_uao_2kh)
    -   [ECS实例是否可以访问亚马逊网站？](#section_q6i_bio_ba9)
    -   [为什么登录到ECS实例后访问不了海外网站？](#section_ags_ovh_bde)
    -   [我需要增加按量付费的服务器，如何增加台数？](#section_xt4_ax4_x66)
    -   [如何查看资源的限额？](#section_z6z_9bh_9is)
-   中国大陆用户购买其他国家或地区实例资源问题
    -   [中国大陆用户购买其它国家或地区资源可以享受与阿里云中国大陆资源相同的品质和服务吗？](#section_16z_pn3_0qf)
    -   [是否可以通过镜像复制功能将中国大陆的ECS转移到其它国家或地区？](#section_50j_2mc_pdr)
    -   [我是非中国大陆的用户，能否使用其他币种线上支付？](#section_lwb_bgi_n6q)
    -   [中国大陆以外地域的实例与中国大陆地域实例有什么区别？怎么判断哪个国家或地区的地域适合我？](#section_jxf_qpr_bbi)
    -   [在中国大陆以外地域购买的实例，能互换Linux系统和Windows系统吗？](#section_1dv_ju1_xq6)
    -   [中国大陆以外地域是否支持购买镜像市场的镜像？](#section_4rw_exo_4dv)
    -   [中国大陆以外地域如果遇到产品售后等问题，如何解决？](#section_yk8_a2w_7d8)
    -   [中国大陆以外地域是否提供产品试用服务？](#section_fq5_90q_u3q)
    -   [中国大陆以外地域是否支持5天无理由退款？](#section_kpb_wty_9qe)
    -   [我要买中国大陆以外地域的实例，需要单独申请一个国际站账号吗？](#section_hn3_htw_jyg)
    -   [如何在中国大陆以外地域部署ECS实例？](#section_t1s_784_kli)
    -   [可否将中国大陆地域的实例迁移到中国大陆以外地域呢？](#section_up6_nbw_5vn)
    -   [为什么有些实例规格只能在中国大陆地域购买，而在中国大陆以外地域无法购买？](#section_fuo_80o_9lm)
    -   [如果我使用中国大陆以外地域的实例搭建了一个网站，我的用户将通过域名访问网站，这个域名需要ICP备案吗？](#section_bso_zgt_6t6)
    -   [不同地域的实例，价格一样吗？](#section_w86_nck_hic)
    -   [各个地域的网络覆盖范围是什么呢？](#section_qyy_69n_4sl)
    -   [中国大陆以外地域是否都可以提供经典网络和专有网络的类型呢？网络类型是否可以变更呢？](#section_2z3_zvk_4tu)
-   实例计费问题
    -   [按量付费ECS实例停机或欠费停机后，会产生费用吗？](#section_bll_9fl_9qs)
    -   [按量付费转包年包月时下单失败如何处理？](#section_ye3_pyk_bzl)
    -   [支付完成后多久能完成按量付费转包年包月？](#section_07w_jp4_rlu)
    -   [按量付费转包年包月失败时如何处理？](#section_ulz_fn2_oxb)
    -   [按量付费转包年包月之后带宽计费方式是否发生变化？](#section_4lm_u5o_2my)
    -   [我有一个按量付费转包年包月订单，但是还没有支付，这时我升级了实例的配置，转换订单还有效吗？](#section_tih_umb_qaz)
    -   [包年包月转按量付费失败时如何处理？](#section_xqt_ua4_1cf)
    -   [新创建的包年包月实例在5天内转为按量付费，属于5天无理由退款吗？](#section_kfr_lv0_ois)
    -   [为什么更改硬盘收费方式提示三次机会已用完？](#section_bxy_dkr_1f9)
    -   [为什么无法将按量付费实例转为包年包月实例？](#section_vlz_58s_9es)
    -   [如何查询实例到期时间？](#section_8hf_t8x_5n3)

## 如何查看某个地域或可用区是否能购买实例？ {#section_dxe_iha_q0o .section}

您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例的可购情况。

## 购买实例时，资源已经售罄怎么办？ {#section_lxw_bwz_qgb .section}

如果在创建实例时遇到资源售罄的情况，建议您采取以下措施：

-   更换地域
-   更换可用区
-   更换资源配置

如果调整需求后仍然没有资源，建议您等待一段时间再购买。实例资源是动态的，如果资源不足，阿里云会尽快补充资源，但是需要一定时间。

您也可以使用到货通知功能：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441448634_zh-CN.png)

## 如何选择适合我业务的ECS实例？ {#section_j8t_fwz_mjf .section}

-   根据您实际的业务需求。
-   确定您网站的类型。
-   确定您网站的日均PV。
-   确认首页大小。
-   确认数据容量。

## 购买ECS实例如何付款？ {#section_huh_ipu_6gt .section}

-   在线支付：单击[账户总览](https://expense.console.aliyun.com/)页面的**充值**，充值之后，通过现金账户的余额进行支付，即时到账。
-   银行对公柜台支付，请参见[如何进行线下汇款或公对公转账](https://help.aliyun.com/knowledge_detail/37108.html)。

## 开通一台云服务器需要多久？ {#section_ska_yf3_rvx .section}

一般需要1~2分钟完成实例创建，实例创建成功后：

-   对Linux实例，您可以[连接ECS实例](../cn.zh-CN/个人版快速入门/连接ECS实例.md#)。
-   对Windows实例，操作系统内部还需要使用sysprep进行初始化。初始化期间，请不要重启实例。初始化完成后，您可以[连接ECS实例](../cn.zh-CN/个人版快速入门/连接ECS实例.md#)。初始化耗时由I/O优化类型决定：
    -   I/O优化的Windows实例，初始化一般耗时2~3分钟。
    -   非I/O优化的Windows实例，初始化一般耗时10分钟。

**说明：** 如果云服务器创建过程中出现异常，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 购买实例付款成功，但是没有生成实例，为什么？ {#section_gbw_acs_xwn .section}

可能是该可用区下该实例规格库存不足。系统会自动退款，如果半小时内没有收到退款，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例的可购情况。

## 为什么购买实例时看不到按量付费资源？ {#section_ls5_e9e_kt3 .section}

16核及以上实例规格可能存在按量高配限制。如果您在购买实例时能看到包年包月资源，但是看不到按量付费资源，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)确认当前账号是否已经获得购买该实例规格按量高配资源的授权。

如果已获得授权，仍然看不到按量资源，可能是当前地域下库存不足，请参见[购买实例时，资源已经售罄怎么办？](#section_lxw_bwz_qgb)。

## 什么是企业级实例？什么是入门级实例？ {#section_2p8_osd_e5y .section}

企业级实例是阿里云2016年9月开始推出的一系列实例规格族的总称，具有高性能、稳定计算能力和平衡网络性能的特点。因为具有独享且稳定的计算、存储、网络资源，这些实例规格族非常适合对业务稳定性具有高要求的企业场景。

入门级实例是一系列面向一般中小网站或个人的实例规格（族）总称。与企业级实例相比，入门级实例在资源利用上更多强调资源性能的共享，所以无法保证实例计算性能的稳定，但是成本相对来说也更低

## 企业级实例与入门级实例有什么本质区别？ {#section_cm4_dks_zu1 .section}

企业级实例采用固定CPU调度模式。每个vCPU绑定到一个物理CPU超线程，实例间无CPU资源争抢，实例计算性能稳定且有严格的SLA保证。

入门级实例采用非绑定CPU调度模式。每个vCPU会被随机分配到任何空闲CPU超线程上，不同实例vCPU会争抢物理CPU资源，并导致高负载时计算性能波动不稳定，有可用性SLA保证，但无性能SLA保证。

## 哪些是企业级实例？哪些是入门级实例？ {#section_y0w_qjj_s3o .section}

目前，在售的[实例规格族](cn.zh-CN/实例/实例规格族.md#)中，入门级实例有：n4、mn4、xn4、e4，其它都属于企业级实例。

## 在什么业务场景下，我需要购买企业级实例？ {#section_8gs_zby_36p .section}

不同企业级实例适用的业务场景请参见[实例规格族](cn.zh-CN/实例/实例规格族.md#)。

## 企业级实例的网络性能怎么样？ {#section_omt_o32_8lt .section}

企业级实例的网络性能与实例规格相关：小规格实例的网络性能低，大规格实例的网络性能高。不同实例规格对应的网络性能，请参见[实例规格族](cn.zh-CN/实例/实例规格族.md#)。

## 企业级实例支持哪几种云盘类型？ {#section_9st_mh4_j3f .section}

企业级实例支持的云盘类型请参见[云盘类型](../cn.zh-CN/块存储/云盘/云盘概述.md#section_d9f_cog_644)。

## 企业级实例支持哪些类型的镜像？ {#section_h1y_jjt_aer .section}

企业级实例支持的公共镜像请参见[公共镜像概述](../cn.zh-CN/镜像/公共镜像/公共镜像概述.md#)。

您也可以导入自定义镜像，详情请参见[导入自定义镜像](../cn.zh-CN/镜像/自定义镜像/导入镜像/导入自定义镜像.md#)。

## 企业级实例规格变配有什么限制？ {#section_rxb_abg_ub7 .section}

企业级实例规格变配限制请参见[支持变配的实例规格](cn.zh-CN/实例/升降配实例/支持变配的实例规格.md#)。

## 入门级实例能否变配为企业级实例？ {#section_90e_qq9_gmf .section}

详情请参见[支持变配的实例规格](cn.zh-CN/实例/升降配实例/支持变配的实例规格.md#)。

## 为什么Nvidia驱动安装成功后，但是nvidia-smi无效，显示驱动未安装？ {#section_6fo_f6k_wy9 .section}

问题分析：kernel-devel和kernel版本不一致，导致在安装driver rpm过程中driver编译出错。

解决方案：查看kernel版本号，网上下载对应的kernel-devel包，在实例里运行`rpm –qa | grep kernel`检测版本是否一致。确认版本后，再重新安装驱动。

## 为什么gn5和gn5i的Windows实例安装官网驱动时断网？ {#section_6ww_806_shg .section}

问题分析：Nvidia对图形功能做了限制，需要特定的驱动并认证License。

解决方案：当前只在特定可用区（华北2可用区E、华北5）安装测试版本的驱动可用，保证不断网，测试驱动有效时间为7−100天。100天后需要认证的License。

以下是针对不同版本Windows的测试驱动下载地址：

-   [Windows Server 2016](http://vgpu-internal-59120.oss-cn-shanghai.aliyuncs.com/385.41_grid_win10_server2016_64bit_international.exe)
-   [Window Server 2008 或 2012](http://vgpu-internal-59120.oss-cn-shanghai.aliyuncs.com/385.41_grid_win8_win7_server2012R2_server2008R2_64bit_international.exe)

## 为什么Windows图形不支持DirectX等功能？ {#section_5mx_en9_guy .section}

问题分析：对于Windows系统，GPU驱动安装生效后，Windows自带的远程连接（RDP）协议不支持DirectX、OpenGL等相关应用。

解决方案：您需要自行安装VNC服务和客户端，或其它支持的协议，例如PCOIP、XenDeskop HDX 3D等。

## 为什么ga1实例使用云市场预装AMD驱动的镜像，但是进入Windows设备管理器时显示GPU驱动未能正常加载？ {#section_myh_mu2_r7g .section}

1.  登录实例。
2.  打开**设备管理器**。
3.  右击**GPU设备名称**。
4.  单击**更新驱动程序软件**。
5.  选择**自动搜索更新的驱动程序软件**。
6.  在Windows系统完成设备驱动更新后重启系统。

## 为什么使用云市场预装AMD驱动的镜像，启动实例时蓝屏？ {#section_593_bs5_c1l .section}

阿里云会更新云市场中预装驱动镜像里所包含的驱动程序来修复此问题。如果您使用的是老版本镜像，可以通过更新GPU驱动程序来避免此问题。

如果出现蓝屏无法启动实例，您必须进入安全模式卸载之前的驱动程序，再正常启动Windows系统，然后安装新版的GPU驱动。

## GPU实例支持安卓模拟器吗？ {#section_vwn_31g_4fn .section}

不支持。

## 我能变更GPU云服务器的配置吗？ {#section_sbj_dzq_gb1 .section}

不支持变配带本地盘的GPU云服务器实例，如ga1、gn5。支持变配不带本地盘的GPU云服务器实例，详情请参见[支持变配的实例规格](cn.zh-CN/实例/升降配实例/支持变配的实例规格.md#)。

## 按量付费GPU云服务器支持停机不收费功能吗？ {#section_pw6_mpa_a0f .section}

不带本地盘的GPU云服务器规格族支持按量付费实例停机不收费功能，包括 gn4（Nvidia M40）、gn5i（Nvidia P4）和 gn6v（Nvidia V100），更多信息参见[按量付费实例停机不收费](../cn.zh-CN/产品定价/按量付费实例停机不收费.md#)。

## 如何查看GPU监控数据？ {#section_lv4_gwl_r5e .section}

您可以通过[云监控控制台](https://cloudmonitor.console.aliyun.com/)或[DescribeMetricList](../../../../../cn.zh-CN/API参考/云产品时序指标类监控数据/DescribeMetricList.md#)来查看GPU监控数据，详情请参见[GPU监控](../../../../../cn.zh-CN/用户指南/主机监控/GPU监控.md#)。

## 弹性裸金属服务器和传统云主机（虚拟机）和传统物理机有何本质区别？ {#section_m7m_pvm_64b .section}

弹性裸金属服务器、传统云主机（虚拟机）和传统物理机的差异请参见[什么是弹性裸金属服务器](cn.zh-CN/实例/选择实例规格/弹性裸金属服务器（神龙）/什么是弹性裸金属服务器.md#)。

## 弹性裸金属服务器的网络性能怎么样？ {#section_mtz_x6v_4v4 .section}

弹性裸金属服务器实例的网络性能与实例规格相关：小规格实例的网络性能低，大规格实例的网络性能高。不同实例规格对应的网络性能，请参见[实例规格族](cn.zh-CN/实例/实例规格族.md#)。

## 弹性裸金属服务器支持哪些磁盘类型？可以挂载多少块数据盘？ {#section_gu1_xmv_r8f .section}

弹性裸金属服务器支持高效云盘和SSD云盘，最多可以挂载16块数据盘。

## 弹性裸金属服务器是否支持规格变配和宕机迁移？ {#section_qzc_rb4_og4 .section}

不支持规格变配。当弹性裸金属服务器发生硬件故障时，支持故障转移，数据都保留在云盘中。

## 如何创建SCC实例？ {#section_9as_2qf_ted .section}

创建SCC实例有两种方式：

-   如果您只需使用RDMA功能，在ECS控制台[创建SCC实例](cn.zh-CN/实例/选择实例规格/超级计算集群（SCC）/创建SCC实例.md#)即可。
-   如果您不仅需要使用RDMA功能，还需要使用HPC调度器以及集群扩容缩容服务，可以通过[E-HPC控制台](https://ehpc.console.aliyun.com)创建SCC集群来创建SCC实例。

## SCC实例如何计费？ {#section_lew_64d_19y .section}

SCC实例支持包年包月和按周付费。

## 如何使用E-HPC创建SCC集群？ {#section_pq2_wpe_y7q .section}

您可以通过[E-HPC控制台](https://ehpc.console.aliyun.com)或CreateCluster接口创建SCC集群。

## 如何使用SCC RDMA功能？ {#section_i2x_rle_0ql .section}

创建SCC实例时，选择SCC定制版的系统镜像，该镜像支持RDMA RoCE驱动和OFED堆栈。您可以通过IB verbs编程使用RDMA功能或者通过MPI进行RDMA通讯。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441550536_zh-CN.png)

## 我没有欠费，为什么抢占式实例被释放了？ {#section_0ns_pj7_dxg .section}

抢占式实例的保护周期为一小时，如果一个小时后某一时刻的市场价格高于您的出价，或者ECS资源的供需情况发生变化，抢占式实例会被回收。

## 抢占式实例被释放时会有通知吗？怎么通知？ {#section_b3n_69r_ccj .section}

有通知。如果因为市场价格变化或供需调整需要释放抢占式实例，实例会先进入待回收状态，约5分钟后再自动释放。您可以通过[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)或者[DescribeInstances](../cn.zh-CN/API参考/实例/DescribeInstances.md#)接口返回的OperationLocks信息查看实例是否进入待回收状态。

## 抢占式实例被释放后数据能自动保留吗？ {#section_hqu_m54_1ac .section}

不能。如果您暂时不需要使用抢占式实例，建议您先[创建快照](../cn.zh-CN/快照/使用快照/创建快照.md#)备份数据和环境，并释放实例，然后在需要使用抢占式实例时再重新购买。

## 我已经设置了抢占式实例释放时间，能取消或者调整吗？ {#section_4dz_4mk_utb .section}

能。抢占式实例释放前，您可以随时取消或调整释放时间。

## 抢占式实例能转为包年包月实例吗？ {#section_4bx_hwo_gre .section}

不能。

## 抢占式实例的价格折扣包括了哪些资源？ {#section_ns2_1jv_mbr .section}

仅实例规格的价格有折扣。其他资源（包括系统盘、数据盘、网络带宽）的价格与按量付费实例的价格保持一致，没有折扣。

## 怎么对抢占式实例出价？ {#section_vv0_a6s_5zd .section}

在创建抢占式实例时，您必须设定可以承受的最高价格（按小时计），当出价高于当前市场价格时，实例就会运行，最终按市场价格计费。更多信息请参见[创建抢占式实例](cn.zh-CN/实例/选择实例购买方式/抢占式实例/创建抢占式实例.md#)。

## 抢占式实例的最高出价和当前市场价格有什么关系？ {#section_67i_s25_aqc .section}

抢占式实例仅在最高出价高于当前市场价格时才能运行。如果最高出价低于市场价格，抢占式实例不会运行，或者运行中的抢占式实例会被释放。不管您出价多少，抢占式实例都按照市场价格计费。

## 在同一时间启动的所有抢占式实例是否收取同样的费用？ {#section_y3x_sk2_stu .section}

是的。

## 抢占式实例运行后一小时内，我支付的费用会随市场价格的变动而变化吗？ {#section_scn_g76_t1n .section}

不会。抢占式实例的小时单价是在各个实例的小时（自然）初始时设定的，适用于整个小时。

## 在购买抢占式实例前我能看到当前的市场价格吗？ {#section_jxg_3ko_6xo .section}

可以。通过控制台创建抢占式实例时，选择实例规格后，您就能查看所选实例规格的市场价格区间以及历史价格，创建页面底部会显示当前总配置（即实例规格 + 存储 + 网络带宽）的费用。其中，实例规格的价格即是当前实例规格的市场价格。

## 我能查看抢占式实例规格的历史价格吗？怎么查看？ {#section_z9a_do7_ofi .section}

可以。通过控制台创建抢占式实例时，选择实例规格后即可查看该实例规格的历史价格。您也可以使用[DescribeSpotPriceHistory](../cn.zh-CN/API参考/实例/DescribeSpotPriceHistory.md#)接口查询历史价格。

## 抢占式实例停止后会继续收费吗？ {#section_8yt_11m_q7i .section}

会。如果您暂时不需要使用抢占式实例，建议您先[创建快照](../cn.zh-CN/快照/使用快照/创建快照.md#)备份数据和环境，并释放实例，然后在需要使用抢占式实例时再重新购买。

**说明：** 此处指在ECS控制台上或通过StopInstance接口手动停止实例。

## 怎么查看抢占式实例消费明细？ {#section_jg4_24g_j0e .section}

详细操作请参见[查看抢占式实例账单](cn.zh-CN/实例/选择实例购买方式/抢占式实例/创建抢占式实例.md#section_pkj_3qt_qgb)。

**说明：** 与按量付费的云服务器配置收费金额不同，抢占式实例的云服务器配置的收费金额是实际成交价格。

## 一个账号可以购买多少台抢占式实例？ {#section_d2v_giu_8a4 .section}

抢占式实例的配额单位是vCPU，而不是实例个数。在创建抢占式实例时，选择实例规格后，您就能查看可用的vCPU配额。详细信息请参见[实例使用限制](../cn.zh-CN/产品简介/使用限制.md#section_tbg_zdx_wdb)。

## 怎么提高vCPU的配额？ {#section_u2j_bsw_7vd .section}

请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 抢占式实例支持变更实例规格吗？ {#section_yae_a2y_k7c .section}

不支持。

## 哪些ECS实例规格族支持抢占式实例？ {#section_8ws_4pm_9cc .section}

与支持按量付费售卖的实例规格相同。如果某些实例规格因资源紧张导致无法购买，请您购买其他实例规格。

## 哪些地域支持抢占式实例？ {#section_0zt_ehb_pts .section}

所有地域均支持抢占式实例。如果某些地域因资源紧张导致无法购买，请您更换其他适用的地域。

## 什么是预留实例券？ {#section_et2_64u_fmh .section}

预留实例券是一种抵扣券，可以抵扣按量付费实例（不含抢占式实例）的账单，也能够预留实例资源。相比包年包月实例，预留实例券与按量付费实例这种组合模式可以兼顾灵活性和成本，比包年包月方式的包月价格更优惠。

## 预留实例券能否提供库存预留？ {#section_5g6_eu4_b0f .section}

当您购买可用区级的预留实例券时，系统会预留与预留实例券匹配的实例库存。 当您购买地域级的预留实例券时，不提供库存预留。

## 预留实例券支持什么操作系统？ {#section_xoy_vzx_szv .section}

支持抵扣Linux和Windows实例的按量账单。例如，当您购买操作系统类型为Linux的预留实例券后，不论您采用何种方式为按量付费实例导入镜像（公共镜像、自定义镜像、共享镜像、镜像市场），只要是Linux操作系统镜像即可符合条件。

如果您的按量付费实例使用自带许可证（BYOL）的镜像，且需要使用预留实例券抵扣账单，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 哪些规格族能够使用预留实例券？ {#section_j7h_12a_tuy .section}

能够使用预留实例券的规格族包括：sn1ne、sn2ne、se1ne、ic5、c5、g5、r5、i2、i2g、hfc5、hfg5和t5。

其中，[突发性能实例t5](cn.zh-CN/实例/选择实例规格/突发型/什么是突发性能实例.md#)只支持可用区级预留实例券，不支持地域级预留实例券，也不支持合并、拆分或者范围调整。

## 预留实例券能否抵扣抢占式实例的账单？ {#section_m9r_qk6_39q .section}

不可以。

## 可以调整预留实例券的实例规格族吗？ {#section_uee_304_jt3 .section}

不可以。

## 什么场景购买可用区级预留实例券？ {#section_wcp_t5l_01b .section}

当您有明确的库存预留需求时，建议选择购买可用区级预留实例券。

## 什么场景购买地域级预留实例券？ {#section_rym_4rw_cl5 .section}

您不需要库存预留，但是想更方便、灵活地使用预留实例券抵扣按量付费实例账单，例如需要更好的可用区灵活性和实例大小灵活性，建议购买地域级预留实例券。

## 如何应用可用区灵活性？ {#section_6vd_nvw_m73 .section}

仅地域级预留实例券支持可用区灵活性。下面举例说明：

您持有以下运行中的按量付费实例：

1台Linux实例，ecs.c5.xlarge，华北1（青岛）可用区B。名称为C5PAYG-b。

您购买了以下预留实例券：

1张地域级券，ecs.c5.xlarge，华北1（青岛）。名称为C5RI。

购买成功后，C5RI匹配C5PAYG-b，抵扣C5PAYG-b的账单。

由于业务需要，您释放掉了C5PAYG-b，在可用区C启动了一台相同规格的C5PAYG-c，则该预留实例券继续匹配C5PAYG-c，抵扣C5PAYG-c的账单。

## 如何应用实例大小灵活性？ {#section_i9g_3my_drv .section}

仅地域级预留实例券支持实例大小灵活性。下面举例说明：

您的账户下有一个地域级预留实例券，规格为ecs.g5.4xlarge；可以抵扣到1个ecs.g5.4xlarge按量实例；也可以抵扣2个ecs.g5.2xlarge按量实例；或者抵扣4个ecs.g5.xlarge按量实例。

您的账户下有一个1年期地域级预留实例券，规格为ecs.g5.xlarge；可以抵扣1个ecs.g5.xlarge按量实例运行1年的账单；或者抵扣1个ecs.g5.2xlarge按量实例运行半年的账单。

## 可用区级的预留实例券支持实例大小灵活性吗？ {#section_tpd_tx9_9ri .section}

不支持。使用可用区级的预留实例券抵扣时，按量付费实例规格必须和券面实例规格完全一致。

## 可用区级的预留实例券支持可用区灵活性吗？ {#section_qdz_h5b_f91 .section}

不支持。使用可用区级的预留实例券抵扣时，按量付费实例的所属可用区必须和券面的可用区信息完全一致。

## 可用区级预留实例券可以调整为地域级预留实例券吗？ {#section_wry_8lc_jj4 .section}

可以。您在购买预留实例券后，仍然可以随时调整预留实例券的范围，包括：

-   将范围从可用区级改为地域级。
-   将范围从地域级改为可用区级。
-   对于可用区级预留实例券，支持在同一地域下更改可用区。

## 可以跨地域调整预留实例券的范围吗？ {#section_m89_45m_v6k .section}

不可以。例如，如果您持有华东1（杭州）可用区B下的可用区级预留实例券，可以调整为华东1（杭州）其它可用区下的可用区级预留实例券，或者调整为华东1（杭州）下的地域级预留实例券，但不能将范围改为其它地域或者其它地域下的可用区。

## 能否跨帐号使用预留实例券？ {#section_6ta_i2c_mga .section}

不可以。

## 预留实例券可以抵扣按量付费实例的存储和网络部分账单吗？ {#section_prg_o9w_0de .section}

不可以。预留实例券用于抵扣按量付费实例的计算资源（vCPU和内存）的账单，同时Windows类型的预留实例券还可以抵扣镜像的账单。

## 可以控制预留实例券抵扣指定实例的账单吗？ {#section_30a_ovt_uhz .section}

不可以。当您有多台符合抵扣标准的实例时，系统将自动按优化后的匹配方案进行抵扣。

## 预留实例券如何计费？ {#section_whe_bza_0u2 .section}

预留实例券自身单独计费，支持多种付款类型：全预付、部分预付和0预付。

购买成功后，预留实例券即开始计算有效期。无论能否匹配到按量付费实例，在有效期内您都需要按付款类型支付费用，选择全预付可以节省更多成本。

## 预留实例券购买后的生效时间如何计算？ {#section_cdy_tt0_n68 .section}

在购买成功后，预留实例券的生效时间按整点计算，从生效时间开始计费，失效时间为到期日次日的零点。例如，您在2019-02-26 13:45:00成功购买了一张预留实例券，有效期为一年，该预留实例券的生效时间和计费开始时间为2019-02-26 13:00:00，失效时间为2020-02-27 00:00:00。如果您在购买预留实例券时已经持有可匹配的实例，则从2019-02-26 13:00～14:00的小时账单开始抵扣，直至预留实例券失效。

## 预留实例券修改、拆分、合并后的生效时间如何计算？ {#section_kfw_q23_shl .section}

如果您对预留实例券进行修改、拆分或者合并，将会生成新的预留实例券，同时旧的预留实例券会失效。新的预留实例券生效时间按整点计算，同时旧的预留实例券失效。例如，您在2019-02-26 13:45:00成功将一张规格为ecs.g5.2xlarge的可用区级预留实例券（RI1）拆分成两张规格为ecs.g5.xlarge的可用区级预留实例券（RI2和RI3）。则RI1的失效时间为2019-02-26 13:00:00，RI2和RI3的生效时间也为2019-02-26 13:00:00。从2019-02-26 13:00:00开始，可抵扣和预留的实例规格也由ecs.g5.2xlarge变为ecs.g5.xlarge，不再抵扣ecs.g5.2xlarge实例的小时账单。如果RI2和RI3在生效后立即成功匹配到实例，也从2019-02-26 13:00:00开始抵扣ecs.g5.xlarge实例的小时账单。

## 为什么购买时看不见0预付的选项？ {#section_95a_y2p_hcl .section}

目前仅部分账号支持0预付（根据您的云服务器的使用情况而定）。

## 预留实例券支持修改券的付款类型吗？ {#section_1ps_ydr_o6o .section}

不支持。

## 预留实例券可以退款吗？ {#section_vnd_a46_hbz .section}

发生以下情况时，您可以申请退款：

-   购买预留实例券后，五天内可申请无理由退款。每个账号每年只有一次无理由退款的机会，不限产品。例如，您同时购买了一台ECS实例和一张预留实例券，如果ECS实例无理由退款，则同年内无法再申请预留实例券无理由退款。
-   购买预留实例券后，目标地域或可用区下的实例资源库存不足。
-   拆分、合并预留实例券或者调整预留实例券范围后，目标地域或可用区下的实例资源库存不足。

退款时会扣除掉已经消费的金额，另外需要支付手续费，详情请参见[退款规则及退款流程](https://help.aliyun.com/knowledge_detail/37096.html)。

## 预留实例券可以转售吗？ {#section_j9e_1zq_35v .section}

不可以。

## Windows类型的预留实例券可以抵扣镜像费用吗？ {#section_0w6_6mr_z27 .section}

可以。Windows类型的预留实例券在购买时已经包括了Windows镜像的费用，可以为运行Windows系统的按量付费实例抵扣镜像部分的账单。

## Linux类型的预留实例券可以抵扣镜像费用吗？ {#section_wm8_tf8_rgx .section}

不可以。

## 管理终端是独享的吗？ {#section_mdm_w4q_wgb .section}

是的。如果一个用户已经登录，其他用户则无法再登录。

## 忘记了远程连接密码，怎么办？ {#section_tym_x4q_wgb .section}

您可以修改远程连接密码，详细步骤请参见[修改远程连接密码](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#section_nmj_5mx_wdb)。

## 为什么修改了远程连接密码还是连不上管理终端？ {#section_huk_e8x_b38 .section}

如果您操作的是非I/O优化实例，还需要通过控制台重启实例，新密码才会生效，详细步骤请参见[重启实例](cn.zh-CN/实例/管理实例/重启实例.md#)。

**说明：** 在ECS实例内部重启实例无效。

## 管理终端提示授权验证失败，怎么解决？ {#section_xl9_o6y_79k .section}

输入远程连接密码后，提示授权验证失败，可能是因为您输入了错误的远程连接密码，请按以下步骤排查：

1.  确认您输入了正确的远程连接密码。
2.  如果您忘了密码，可以[修改远程连接密码](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#section_nmj_5mx_wdb)之后再重试。
3.  如果要连接非 I/O 优化实例，修改密码后，您需要先在控制台上[重启实例](cn.zh-CN/实例/管理实例/重启实例.md#)使新的远程连接密码生效。

## 连接到管理终端后出现黑屏，怎么办？ {#section_xrm_6sm_10m .section}

连接到管理终端后出现黑屏，说明系统处于休眠状态。根据操作系统不同，执行不同的操作：

-   如果是Linux实例，您可以按任意键激活该实例，进入登录界面。
-   如果是Windows实例出现持续黑屏，您可以在界面左上角单击**发送远程命令** \> **CTRL+ALT+DELETE**，进入登录界面。

## 管理终端无法访问了，怎么办？ {#section_65w_3px_xpu .section}

您可以使用Chrome浏览器进入管理终端界面，在键盘上按F12键显示开发者工具，然后分析**Console**中显示的信息。

## 我使用IE8.0，为什么无法使用管理终端？ {#section_82j_21b_xj0 .section}

仅支持IE10及以上版本的IE浏览器中使用管理终端，请下载最新版本的IE浏览器。

建议使用Chrome浏览器，阿里云的控制台对Chrome浏览器的兼容性更好。

## 我用Firefox浏览器打开管理终端会报错安全连接失败，怎么办？ {#section_l6t_kik_vmy .section}

可能您使用的Firefox版本没有共用的加密算法。

建议使用Chrome浏览器，阿里云的控制台对Chrome浏览器的兼容性更好。

## 如何远程登录到Linux实例？ {#section_tkz_v77_wbf .section}

通常Linux系统使用SSH服务提供远程连接。您可以：

-   [使用管理终端连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)。
-   [使用用户名密码验证连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
-   [使用SSH密钥对连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md#)。
-   [在移动设备上连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/在移动设备上连接Linux实例.md#)。

## 远程登录实例操作系统时，默认用户名和密码是什么？ {#section_u82_ecw_928 .section}

默认用户名和实例类型有关：

-   远程登录Windows实例时，默认用户名是`administrator`。
-   远程登录Linux实例时，默认用户名是`root`。

密码由您在创建实例时设置，请参见[使用向导创建实例](cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。如果忘记了登录密码，您也可以重置密码，请参见[重置实例登录密码](cn.zh-CN/实例/管理实例/重置实例登录密码.md#)。

**说明：** 此处的登录密码指登录Windows或Linux操作系统时的密码，不是管理终端的远程连接密码。

## 我能升级包年包月ECS实例规格和配置吗？ {#section_5ap_zkp_361 .section}

可以，请参见[包年包月实例升级配置](cn.zh-CN/实例/升降配实例/升配包年包月实例/包年包月实例升级配置.md#)。

## 我能升级按量付费ECS实例规格和配置吗？ {#section_472_rev_qvi .section}

可以，但需要预先停止实例。您可以参见文档[按量付费实例变更实例规格](cn.zh-CN/实例/升降配实例/升降配按量付费实例/按量付费实例变更实例规格.md#)或者通过API接口[ModifyInstanceSpec](../cn.zh-CN/API参考/实例/ModifyInstanceSpec.md#)升级按量付费实例的配置。

## 升级ECS实例过程大约需要多久？ {#section_ju8_yai_0f9 .section}

-   升级包年包月实例规格无需预先停止实例，大约15分钟左右。
-   升级按量付费实例规格需要预先停止实例，大约15分钟左右。
-   升级实例带宽无需预先停止实例，大约5分钟左右。

## 升级ECS实例产生的费用怎么计算？ {#section_ckm_8hg_3uy .section}

升级ECS实例规格和配置时，页面上会显示费用信息。您也可以在[账户总览](https://expense.console.aliyun.com/)页面查询产生的费用详情。

## 升级ECS实例对我的云上业务的配置有什么影响吗？ {#section_s9y_1yw_w5c .section}

升级按量付费实例时，需要预先停止实例。升级包年包月实例时，需要重启实例后新配置才能生效。升级操作会使您的业务短暂中断，建议您在业务不繁忙时升级。升级后的实例能无缝对接业务，您无需重新配置云服务器ECS环境。

## 如何升级ECS资源？ {#section_grz_gr2_rve .section}

升级ECS资源的方式请参见[升降配方式汇总](cn.zh-CN/实例/升降配实例/升降配方式汇总.md#)。

-   除带本地存储的实例外，云服务器ECS支持在线变更CPU、内存和带宽升级，升级实例生效之后支持降级。
-   云服务器ECS支持最多挂载16块数据盘，升级数据盘生效后不支持再次降级。
-   云服务器ECS带宽单位为Mbps（Megabit per Second），带宽速率范围为0−200 Mbps。您可以进行临时升级带宽、续费降配等操作。

## 为什么降配时实例预计退款为0？ {#section_wrl_689_36t .section}

降配时实例预计退款显示为0，可能是因为您在购买实例时享受了折扣价，降配后的配置按官网原价计算，差价可能会小于等于0元，这时均会显示为0。

## 为什么升级实例配置后没有效果？ {#section_jsb_os8_bbb .section}

升级实例配置后，需要在控制台[重启实例](cn.zh-CN/实例/管理实例/重启实例.md#)。

## 升级包年包月实例带宽，为什么提示按使用流量计费的带宽不支持带宽临时升级？ {#section_8de_1dx_l78 .section}

公网带宽计费方式分为按固定带宽和按使用流量。

包年包月实例的带宽按使用流量计费时，不支持临时升级带宽，但您可以通过升级配置功能升级基础带宽。具体操作，请参见[包年包月实例升级配置](cn.zh-CN/实例/升降配实例/升配包年包月实例/包年包月实例升级配置.md#)。

## ECS实例长时间为Starting状态，且AliyunService被禁用或被删除怎么办？ {#section_3kd_bat_4p4 .section}

问题描述：启动云服务器ECS实例后，ECS实例长时间处于Starting状态，然后自动关机。登录系统查看系统服务，发现AliyunService被删除或禁用。

解决方法：

-   如果AliyunService被禁用：
    1.  将AliyunService修改为自动状态。
    2.  重启云服务器 ECS。
-   如果AliyunService被删除：
    1.  执行以下命令重新添加服务。

        ``` {#codeblock_z9n_oe1_dty}
        sc create AliyunService type= "own" start= "auto" binPath= "C:\Program Files\AliyunService\AliyunService.exe -d" tag= "no" DisplayName= "AliyunService"
        ```

        **说明：** 请注意保留`=`后面的空格。

    2.  打开注册表HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\AliyunService，将`c:\Program Files\AliyunService\AliyunService.exe -d`修改为`"c:\Program Files\AliyunService\AliyunService.exe" -d`。
    3.  重启云服务器ECS实例。

## 如何通过ECS服务器让OSS支持HTTPS访问？ {#section_0mh_dus_4lh .section}

假设您持有以下OSS Bucket，要通过域名www.example.com实现HTTPS访问。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441543179_zh-CN.png)

1.  创建一台和Bucket位于相同地域的ECS实例。

    详细步骤请参见[使用向导创建实例](cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。

2.  在ECS实例上配置反向代理。

    反向代理配置中nginx的server段样例如下：

    ``` {#codeblock_xmc_jvy_lgx}
    server {
      listen 80;
      #填写对外提供反向代理服务的域名
      server_name www.example.com;
      location / {
      root /alidata/www/ www.example.com/;
      #填写Bucket的内网访问域名，如果ECS实例与Bucket不在同一个地域，需填写外网域名
      proxy_pass http://bucketname.oss-cn-hangzhou-internal.aliyuncs.com/;
      }
    }
    ```

3.  配置www.example.com的A记录指向ECS实例的外网地址。
4.  验证反向代理可以正常工作。

    使用ECS外网地址加文件访问路径访问OSS资源，可以访问即表示工作正常。

5.  在ECS实例上为www.example.com添加并配置SSL证书。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 如何操作f1实例？ {#section_ug1_lb2_d7l .section}

创建f1实例之后，阿里云会向您共享一个FPGA开发镜像（目前只能支持CentOS 7u2）。您可以在该镜像上免费试用Intel Quartus全套开发组件和f1实例相应器件的约束文件，体验一整套云上开发环境。

**说明：** 您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例的可购情况。

使用f1实例的基本流程如下：

1.  开发完成后，您可以在工程编译阶段生成一个中间qar文件，将qar文件上传到您的OSS bucket（目前只能支持华东1地域），然后调用API将qar的相关信息注册到阿里云。

    建议您在云上完成相应的开发、编译、仿真的操作，从而利用免费的Intel Quartus开发套件。

2.  阿里云会审核qar文件注册请求，在安全验证通过后向您发送通知邮件，通知邮件中同时包含FPGA的镜像ID。
3.  部署时，先调用API关联云服务器实例与FPGA镜像，利用f1实例ID和FPGA镜像ID作为参数。

    您可以在任何能访问ECS API的场景下发起关联。

    -   如果该f1实例从未关联过任何FPGA镜像，可以直接发起关联操作。
    -   如果该f1实例之前关联并装载过FPGA镜像，在发起关联命令之前，必须保证FPGA镜像已经从该f1实例上擦除。
4.  关联成功后，继续调用API装载FPGA镜像。

    装载操作必须从f1实例所在的云服务器上发起，指定FPGA镜像ID后，阿里云的底层服务会把对应的FPGA镜像烧制到实例对应的FPGA器件。


如果想将f1实例恢复至初始状态，可以调用API从f1实例擦除已经烧制的FPGA镜像。

更多f1实例的操作指南，请参见：

-   [创建f1实例](cn.zh-CN/实例/选择实例规格/FPGA计算型/创建f1实例.md#)
-   [f1实例OpenCL开发最佳实践](../cn.zh-CN/最佳实践/FaaS实例最佳实践/f1实例OpenCL开发最佳实践.md#)
-   [使用f1 RTL](../cn.zh-CN/最佳实践/FaaS实例最佳实践/使用f1 RTL.md#)

## macOS如何通过FTP工具上传文件？ {#section_39c_w47_rds .section}

方式一：通过macOS自带终端上传

您可以通过macOS本身的终端或者iTerm2（[单击此处](https://www.iterm2.com/)下载iTerm2）上传文件。注意正确地选择上传文件的路径。

1.  连接FTP服务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441543224_zh-CN.png)

2.  进入正确的目录，Windows系统无需切换，Linux系统切换至htdocs。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441549119_zh-CN.png)

3.  运行put命令上传。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441649120_zh-CN.png)


方式二：通过第三方工具上传

1.  [单击此处](https://www.yummysoftware.com/)下载Yummy FTP。
2.  在macOS中安装Yummy FTP。
3.  填写FTP的服务器IP、用户名和密码；协议选择标准（FTP），端口选择默认21（或更改为其您所使用的端口），不选择SSH密匙。
4.  单击**连接**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441643228_zh-CN.png)

5.  在右侧选择要上传的目录（Windows不需要选择目录，Linux主机选择htdocs目录），然后在左边窗口选择要上传的文件，单击上传即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441643230_zh-CN.png)

    **说明：** 若安装Yummy FTP时系统提示：您的安全性偏好设置仅允许安装来自Mac App Store和被认可的开发者的应用程序，按以下步骤设置您的电脑。

    1.  依次打开： **系统偏好设置** \> **安全性与隐私** 。
    2.  单击左下角的安全锁，输入管理员密码解锁。
    3.  在**允许从以下位置下载的应用程序**菜单中，选择**任何来源**。
    设置后即可正常安装该软件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441643238_zh-CN.png)


如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 为什么无法在ECS实例上登录淘宝网？ {#section_n4z_oet_sdc .section}

问题描述：无法登录淘宝账号，尝试登录时一直提示系统繁忙，提示输入验证码，输入多次验证码还是无法登录。

问题解决：淘宝网对外部访问的一些API存在限制。如果需要正常调用，建议通过使用聚石塔主机解决。更多详情请访问[聚石塔解决方案](https://cloud.tmall.com/)。

问题描述：ECS实例无法访问[手机淘宝](m.taobao.com)。

问题解决：移动淘宝主要供APP无线客户端访问，无线产品会有相应的安全策略，属于淘宝网对IP端的限制，阿里云无法保证ECS（属于PC端）一定可以访问成功。

## 购买ECS实例后如何备案域名？ {#section_br4_f3k_1jw .section}

待备案的ECS实例需要满足购买要求，且每台实例可申请的备案服务号数量有限，详细信息请参见[备案服务器（接入信息）准备与检查](../../../../../cn.zh-CN/ICP备案前准备/托管服务器及接入检查/备案服务器（接入信息）准备与检查.md#)。

备案流程请参见[ICP备案快速入门](../../../../../cn.zh-CN/ICP备案快速入门/ICP备案快速入门.md#)。

## 为什么ECS实例无法加载内核启动？ {#section_o58_xbc_j1a .section}

问题描述：系统启动时，在GRUB菜单界面选择任何一个选项都无响应。在该ECS实例上挂载LiveCD镜像登录系统后查看文件系统权限正常，message的日志信息正常。

问题原因：系统中了加密勒索病毒。

解决方案：请备份重要数据，重新初始化系统。

更多信息，请参见[加密勒索病毒处理方案](https://help.aliyun.com/knowledge_detail/50358.html)。

## 如何在实例内部修改登录密码？ {#section_5dx_x72_cb8 .section}

详细步骤请参见[在实例内部修改登录密码](cn.zh-CN/实例/管理实例/在实例内部修改登录密码.md#)。

## 购买了ECS实例，想对ECS实例添加声卡和显卡，且发现无法添加，是什么原因？ {#section_lqe_uwn_har .section}

阿里云提供的是常规服务器，不是多媒体服务器，服务器默认不提供声卡和显卡组件，所以在系统中无法添加声卡和显卡。

## 可以转移某台ECS剩余使用时间到别的ECS上吗？ {#section_nwm_uhx_s6y .section}

不支持。如果您需要兼顾灵活性和成本，建议在购买实例时选择按量付费实例，然后搭配预留实例券，更多信息请参见[预留实例券概述](cn.zh-CN/实例/选择实例购买方式/预留实例券/预留实例券概述.md#)。

## ECS实例如何查询云服务器IP地址归属地？ {#section_uvf_mwq_enl .section}

用户购买的ECS实例所在地域即是IP的归属地地域，可以通过[http://ip.taobao.com](http://ip.taobao.com)进行查询。

**说明：** 第三方网站可能会有IP地址数据库更新不及时的情况，导致查询结果与实际地域不同，请酌情选择查询网站。

## 云服务器默认提供数据库吗？ {#section_h97_kf4_xjp .section}

云服务器默认不提供数据库，您可以：

-   自行部署数据库。

    **说明：** 数据库部署教程，请参见[在ECS上部署数据库](../cn.zh-CN/建站教程/在ECS上部署数据库.md#)。

-   单独购买阿里云[RDS数据库](https://rdsnext.console.aliyun.com/)服务。
-   使用镜像市场配置环境数据库。

## 云服务器上是否可以搭建数据库？ {#section_jli_u2y_g3m .section}

可以。您可以根据需求安装数据库软件和配置环境，ECS不作限制。同时您也可以单独购买阿里云[RDS 数据库](https://rdsnext.console.aliyun.com/)服务。

## 云服务器是否支持Oracle数据库？ {#section_j1b_acd_1f7 .section}

支持。建议您在安装Oracle数据库前压测ECS性能，确认实例可以满足您的数据库读写需求。

## 公网IP和私网IP是否独立，能指定或增加IP吗？ {#section_dvt_enw_7gr .section}

经典网络：公网IP和私网IP相互独立。经典网络私网IP一般用于云服务器之间、云服务器与OSS、RDS之间的通信（0 M带宽的云服务器不分配公网IP）。正常使用的情况下，IP不会变化，且不能指定、选择或者增加购买IP。

专有网络：公网IP以NAT模式映射到私网IP。您可以指定辅助私网IP，也可以通过多IP方式增加IP。

## 云服务器能否做负载均衡？ {#section_g6s_x91_9m2 .section}

Linux操作系统的云服务器和Windows操作系统的云服务器都可以实现负载均衡，但是必须保证Web云服务器配置和网站代码一致，同一账号下一台ECS实例就可以使用负载均衡，但是为了保证负载均衡效果，建议您使用2台及以上的ECS实例做负载均衡。

## 购买ECS实例后可以更换地域吗？ {#section_wm7_rby_mij .section}

阿里云ECS实例不支持更换地域。

## 可以调整已购磁盘的分区大小吗？ {#section_nih_446_koq .section}

出于系统安全和稳定性考虑，Windows和Linux实例均不支持系统盘二次分区。如果您强行使用第三方工具进行二次分区操作，可能引发未知风险，如系统崩溃、数据丢失等。

数据盘可以进行二次分区，但容易导致数据丢失，不建议进行二次分区。

## 如何将实例的固定公网IP更换为其它EIP？ {#section_grq_3gj_n2r .section}

如果您在购买服务器时选择了固定带宽，并且已经购买了新EIP，请按以下步骤操作：

1.  将固定带宽转换为按量带宽，具体操作请参见[变更计费方式](../cn.zh-CN/产品定价/公网带宽计费.md#section_nxl_ntk_zdb)。
2.  将固定公网IP转换为EIP，具体操作请参见[ECS固定公网IP转换为EIP](../../../../../cn.zh-CN/用户指南/申请EIP/ECS固定公网IP转换为EIP.md#)。
3.  解绑转换得到的EIP，具体操作请参见[解绑EIP](../../../../../cn.zh-CN/用户指南/解绑EIP.md#)。
4.  绑定新的EIP，具体操作请参见[绑定ECS实例](../../../../../cn.zh-CN/用户指南/绑定云资源/绑定ECS实例.md#)。

## 如何查看同一地域下的包年包月实例？ {#section_bud_chq_gek .section}

您可以使用资源概览功能查看同一个地域下的包年包月实例，详细步骤请参见[查看资源概览](../cn.zh-CN/标签与资源/查看资源概览.md#)。

## 如何查看同一账号下所有地域的包年包月实例？ {#section_s5o_w6z_95z .section}

您可以前往续费管理页面查看所有地域下的包年包月实例。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在顶部状态栏处，选择**费用** \> **续费管理**。

## 什么时候可以强制停止实例？有什么后果？ {#section_nlp_9qg_6gq .section}

在不能通过正常关机流程停止实例时，您可以强制停止实例。强制停止实例等同于断电处理，可能丢失实例操作系统中未写入磁盘的数据。

## 为什么会重开机失败？ {#section_vk6_sjc_agd .section}

重开机失败可能是以下原因：

-   账号欠费，请结清账单后重试。
-   系统繁忙，请稍后重试。
-   资源已经售罄。

    **说明：** 您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例的可购情况。


## 使用弹性伸缩功能时，伸缩组内ECS实例开启了释放保护，为什么仍然被自动释放了？ {#section_so8_gdz_2i5 .section}

在弹性伸缩自动创建一台ECS实例后，如果您在ECS控制台的实例列表页面或者调用[ModifyInstanceAttribute](../cn.zh-CN/API参考/实例/ModifyInstanceAttribute.md#)为ECS实例开启了释放保护，并不能阻止弹性伸缩自动释放实例。

您可以在弹性伸缩控制台将伸缩组内的ECS实例转为保护状态，避免被自动释放，具体操作请参见[实例转为保护状态](../../../../../cn.zh-CN/用户指南/维护自动伸缩/实例转为保护状态.md#)。

## ECS实例中AliVulfix进程是什么？ {#section_4ek_d0m_191 .section}

AliVulfix进程是云盾进行漏洞检测的程序，用于扫描云服务器是否有漏洞。

## 云服务器能防网络攻击吗？ {#section_t6g_7b5_165 .section}

阿里云云服务器配有云盾服务，可以防御DDoS流量攻击。当出现网络攻击时，阿里云监控系统自动检测并清洗异常流量。如果攻击量非常大，阿里云会做黑洞处理，保护您的ECS实例。出于安全考虑，建议您自己安装防护软件加强防护效果，并封闭不常用的端口。

## 阿里云安全方面有哪些服务？ {#section_cxr_p7b_a9w .section}

阿里云云盾结合阿里云云计算平台强大的数据分析能力，为您提供一站式安全服务，例如安全漏洞检测、网页木马检测、面向云服务器用户提供的主机入侵检测和防御DDoS流量攻击等。

更多安全服务请查看[安全产品](https://security.aliyun.com/)页面。

## ECS Linux服务器到期续费后站点无法访问怎么办？ {#section_s8j_d1f_1u6 .section}

问题描述：ECS到期后服务器处于停止状态。续费后启动服务器，发现站点无法访问。

问题分析：可能是因为未启动网站服务。

解决方法：

1.  远程登录服务器，运行以下命令查看网站服务是否已启动。

    ``` {#codeblock_72x_ahr_4k6}
    #netstat -nltp //查看服务器80端口是否处于监听状态
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441741861_zh-CN.png)

2.  如果未显示80端口信息，说明网站服务没有启动，运行命令手动开启网站服务及相关服务。

    Linux系统一般采用PHP+MySQL搭建网站。

    -   如果为Apache环境，启动网站服务和MySQL即可。

        ``` {#codeblock_y5p_uic_anm}
        #/etc/init.d/httpd start          //启动网站服务,适用于Apache环境
        #/etc/init.d/mysqld start         //启动MySQL
        ```

    -   如果为Nginx环境，需启动网站服务、PHP和MySQL。

        ``` {#codeblock_jng_pj1_5zz}
        #/etc/init.d/nginx start          //启动网站服务，适用于Nginx环境
        #/etc/init.d/php-fpm start        //启动PHP
        #/etc/init.d/mysqld start         //启动MySQL
        ```

3.  再次查看网站服务是否已启动。

    ``` {#codeblock_248_ghb_rjh}
    #netstat -nltp //查看服务器80端口是否处于监听状态
    ```

4.  如果网站服务是否已启动，尝试重新访问站点。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 如何查询Linux实例的账号和密码？ {#section_sri_3o0_prt .section}

云服务器ECS的账号和密码会在创建成功后发送到您账号绑定的手机和邮箱。Linux系统的默认管理员账号是root。

## 如何检查Linux实例磁盘和进行分区格式化？ {#section_csf_vvp_2z1 .section}

您可以通过df –h命令查询磁盘空间和使用情况，通过fdisk –l命令查询磁盘信息。 Linux实例磁盘分区和格式化操作，请参见[Linux格式化数据盘](../cn.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)。

## 如何向Linux实例上传文件？ {#section_861_wjj_km6 .section}

您可以使用FTP服务将文件上传到Linux实例。

## 如何调整Linux实例目录文件的拥有者和拥有组？ {#section_kf0_kn1_74z .section}

如果Web服务器中文件或者目录的权限不正确，会导致访问网站时出现403错误。因此在调整文件和目录前要确认所在进程的运行身份。

您可以使用ps和grep命令查询文件和目录所在进程的运行身份。

您可以使用ls –l命令来查询文件和目录的拥有者和拥有组。

您可以使用chown命令修改权限。例如，chown -R www.www /alidata/www/phpwind/可将目录/alidata/www/phpwind下的所有文件和目录的拥有者和拥有组都修改为www账户。

## 如何更新Linux实例的软件源？ {#section_8jc_uw1_mjn .section}

您可以使用软件源自动更新工具，请参见[云服务器ECS Linux软件源自动更新工具](https://help.aliyun.com/knowledge_detail/41177.html)。

## 如何在Linux实例上搭建支持PHP的Web环境？ {#section_ww2_idc_mq1 .section}

搭建支持PHP的Web环境，通常需要安装Apache/Nginx+PHP+MySQL。您可以使用云市场的[阿里云Linux一键安装Web环境](https://market.aliyun.com/products/56014009/cmgj000262.html)。

## 织梦建站选择什么服务器？ {#section_nff_lzp_v4l .section}

您可以使用[云虚拟主机](https://wanwang.aliyun.com/hosting)搭建网站，或者前往[云市场](https://market.aliyun.com/)选购织梦建站服务。

## ECS实例转移和更换公网IP地址有什么限制？ {#section_y49_iww_fvq .section}

转移和更换ECS实例的公网IP地址有以下限制：

-   经典网络
    -   不支持公网IP跨账号转移。
    -   实例创建后6小时内，允许更换公网IP地址，最多可以更换3次。6小时后，不能再更换公网IP地址。具体操作，请参见[修改公网IP地址](../cn.zh-CN/网络/修改IPv4地址/修改公网IP地址.md#)。
    -   使用高防IP业务后，最多支持更换10次源站IP。具体操作，请参见DDoS高防IP用户指南的[更换 ECS IP](../../../../../cn.zh-CN/DDoS高防IP/用户指南/实例管理/更换 ECS IP.md#)。
-   专有网络
    -   不支持公网IP及EIP跨账号转移。
    -   如果实例没有分配公网IP，您可以为实例绑定EIP。您可以通过绑定新的EIP更换公网IP。
    -   如果实例已经分配了公网IP：
        -   实例创建后6小时内，允许更换公网IP地址，最多可以更换3次。具体操作，请参见[修改公网IP地址](../cn.zh-CN/网络/修改IPv4地址/修改公网IP地址.md#)。
        -   通过将公网IP转换为EIP的方式更换IP。具体操作，请参见[专有网络公网IP转换为弹性公网IP](../cn.zh-CN/网络/修改IPv4地址/专有网络公网IP转换为弹性公网IP.md#)。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 云服务器ECS创建多少个网站？ {#section_999_02s_59y .section}

一个云服务器ECS最多支持绑定5个备案服务号（SN号），可供您完成5次网站备案。每个网站可以绑定多个域名。

示例：您备案了两个网站，第一个网站绑定域名example1.com，第二个网站绑定example2.com、example3.com、example4.com等域名。备案通过后，您可以使用每个绑定的域名正常访问网站。

**说明：** 

-   假如第二个网站绑定了多个域名，您需要保证这几个域名打开的是同一个网站内容。不能在备案通过后，又使用exmple3.com去绑定另外一个网站。
-   备案只针对一级域名。您可以在云服务器ECS新创建一个站点，绑定blog.example1.com，再创建一个站点绑定new.example2.com。这种建站方式不在限制范围内，也不计算在最多备案5个网站的限制内。

## 收到违规信息整改通知邮件如何处理？ {#section_ybb_uao_2kh .section}

收到邮件，内容如下：

您好，接主管部门通知，您的主机存在通过技术手段使其成为境内获取境外非法信息的途径等行为，根据《互联网信息服务管理办法》第十五条规定九不准内容及阿里云服务条款3.1.3.11，请您在二十四小时内停止上述行为，并做好自查。如逾期未处理或再次收到通知，阿里云将按要求及规定停止对您提供服务。 涉及主机：\*\*\*\*\*\*\*

根据工信部《关于清理规范互联网网络接入服务市场的通知》2-4的规定： 未经电信主管部门批准，不得自行建立或租用专线（含虚拟专用网络VPN）等其他信道开展跨境经营活动。基础电信企业向用户出租的国际专线，应集中建立用户档案，向用户明确使用用途仅供其内部办公专用，不得用于连接境内外的数据中心或业务平台开展电信业务经营活动。

建议您核实是否有搭建VPN服务、代理服务器等。如果远程连接正常，不建议您搭建VPN服务，否则会出现以上异常情况。

## ECS实例是否可以访问亚马逊网站？ {#section_q6i_bio_ba9 .section}

ECS实例可以访问亚马逊网站，确保您的ECS实例可以正常访问外网即可。

## 为什么登录到ECS实例后访问不了海外网站？ {#section_ags_ovh_bde .section}

访问海外网站需要满足实例所在国家或地区的政策规定。请确保您的ECS实例可以正常访问外网，并且访问合规的海外网站。

## 我需要增加按量付费的服务器，如何增加台数？ {#section_xt4_ax4_x66 .section}

如果您无法继续购买按量付费实例，可能是因为可购数量达到上限，详情请参见[实例使用限制](../cn.zh-CN/产品简介/使用限制.md#section_tbg_zdx_wdb)。您也可以在ECS控制台概览页面查看权益配额，具体步骤请参见[管理配额](../cn.zh-CN/标签与资源/管理配额.md#)。

## 如何查看资源的限额？ {#section_z6z_9bh_9is .section}

查看资源的使用限制和限额，请参见[使用限制](../cn.zh-CN/产品简介/使用限制.md#)。

## 中国大陆用户购买其它国家或地区资源可以享受与阿里云中国大陆资源相同的品质和服务吗？ {#section_16z_pn3_0qf .section}

是的，阿里云中国站为所有用户提供相同品质产品与服务，购买地域不同不会影响您在阿里云中国站所享受的服务权益。

## 是否可以通过镜像复制功能将中国大陆的ECS转移到其它国家或地区？ {#section_50j_2mc_pdr .section}

可以。

## 我是非中国大陆的用户，能否使用其他币种线上支付？ {#section_lwb_bgi_n6q .section}

目前阿里云中国站只支持人民币支付。

## 中国大陆以外地域的实例与中国大陆地域实例有什么区别？怎么判断哪个国家或地区的地域适合我？ {#section_jxf_qpr_bbi .section}

其它国家或地区的实例部署在中国大陆以外的机房，对于非中国大陆用户来说地理及市场优势十分明显，这些机房对当地网络连接也相对快速，可以满足国际化客户的需求，更适合有其它国家或地区业务的用户。

支持的地域请参见[地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#)。

## 在中国大陆以外地域购买的实例，能互换Linux系统和Windows系统吗？ {#section_1dv_ju1_xq6 .section}

中国大陆以外地域下的实例，只能在同类型操作系统间互换，即一种Linux发行版本更换为另一种Linux发行版本，或者一种Windows版本更换为另一种Windows发行版本。

## 中国大陆以外地域是否支持购买镜像市场的镜像？ {#section_4rw_exo_4dv .section}

支持。

## 中国大陆以外地域如果遇到产品售后等问题，如何解决？ {#section_yk8_a2w_7d8 .section}

如果在阿里云官网购买的，可以直接拨打阿里云的官方7x24小时服务热线（95187）或者[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)，售后工单7x24小时为您服务。

## 中国大陆以外地域是否提供产品试用服务？ {#section_fq5_90q_u3q .section}

您可以前往[免费套餐](https://free.aliyun.com/)页面查看可免费体验的产品。

## 中国大陆以外地域是否支持5天无理由退款？ {#section_kpb_wty_9qe .section}

如果符合规则，阿里云中国站支持，详情请参见[退款规则及操作说明](https://help.aliyun.com/knowledge_detail/37096.html)。

## 我要买中国大陆以外地域的实例，需要单独申请一个国际站账号吗？ {#section_hn3_htw_jyg .section}

使用阿里云中国站账号既可以购买中国大陆地域的实例，也可以购买其它国家或地区的实例，无需分别申请中国站账号和国际站账号。

## 如何在中国大陆以外地域部署ECS实例？ {#section_t1s_784_kli .section}

中国大陆以外地域的实例与中国大陆地域的实例只是地域上有区别，如果是相同类型的操作系统，部署方式并没有区别。

## 可否将中国大陆地域的实例迁移到中国大陆以外地域呢？ {#section_up6_nbw_5vn .section}

实例的地域和可用区不能变更。如果您需要在其它国家或地区使用实例，您需要重新购买实例或者复制镜像。

## 为什么有些实例规格只能在中国大陆地域购买，而在中国大陆以外地域无法购买？ {#section_fuo_80o_9lm .section}

某些地域可能不支持部分实例规格。您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例的可购买情况。

## 如果我使用中国大陆以外地域的实例搭建了一个网站，我的用户将通过域名访问网站，这个域名需要ICP备案吗？ {#section_bso_zgt_6t6 .section}

中国大陆地域的网站，域名需要备案。其它国家或地区的网站，域名不需要ICP备案。详细信息请参见[什么是备案](../../../../../cn.zh-CN/产品简介/什么是备案.md#)。

## 不同地域的实例，价格一样吗？ {#section_w86_nck_hic .section}

购买一台实例时，实例价格的内容包括实例规格、存储、网络带宽，部分其它国家或地区还包括镜像使用费用。不同的地域，上述各部分的价格可能不同，所以实例的价格也不同。

具体的价格信息，请参见[详细价格总览](https://www.aliyun.com/price/product#/ecs/detail)。

## 各个地域的网络覆盖范围是什么呢？ {#section_qyy_69n_4sl .section}

-   华北5（呼和浩特）、华北3（张家口）、华北2（北京）、华北1（青岛）、华东1（杭州）、华南1（深圳）和华东2（上海）地域：提供多线BGP骨干网线路，网络能力覆盖全国各省市，实现稳定高速国内大陆地域访问。
-   中国香港、新加坡、澳大利亚（悉尼）、马来西亚（吉隆坡）、日本（东京）、德国（法兰克福）、阿联酋（迪拜）地域：提供国际带宽访问，覆盖中国香港、亚太、东南亚、日本、韩国、欧洲、中东、澳洲等地域。
-   美国（硅谷）和美国（弗吉尼亚）地域：位于美国，通过BGP线路直接接连多家美国运营商骨干网，可覆盖全美，同时可以很好的辐射南美洲和欧洲大陆。

## 中国大陆以外地域是否都可以提供经典网络和专有网络的类型呢？网络类型是否可以变更呢？ {#section_2z3_zvk_4tu .section}

如果您在2017年6月14日下午5点（UTC+8时间）以后首次购买ECS实例，阿里云中国站全地域不再提供经典网络选项。

如问题还未解决，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 按量付费ECS实例停机或欠费停机后，会产生费用吗？ {#section_bll_9fl_9qs .section}

欠费停机是指按量付费ECS实例因账号欠费而自动停止服务，处于这个状态的实例不计费。

停机是指按量付费ECS实例在正常运行期间，您通过ECS管理控制台或StopInstance接口，使实例进入**已停止**状态。此时，按量付费实例的计费情况和网络类型有关。

-   专有网络：可以设置为实例停机不收费，即开通实例停机不收费功能后，专有网络按量付费实例从创建开始计费，实例处于**已停止**状态时停止计费，实例启动后又重新计费。实例停机不收费功能只适用于实例的计算资源（即vCPU和内存）和公网IP地址，但云盘仍旧计费。详情请参见[按量付费实例停机不收费](../cn.zh-CN/产品定价/按量付费实例停机不收费.md#)。
-   经典网络：进入**已停止**状态后仍然正常计费。

## 按量付费转包年包月时下单失败如何处理？ {#section_ye3_pyk_bzl .section}

以下情况都会造成下单失败：

-   实例当前状态不支持转换。
-   实例已经设置了自动释放时间，暂不支持转换。
-   实例当前处于**已过期**状态，暂不支持转换。
-   实例的信息发生变化，不允许转换。
-   实例存在未支付的转换订单。

如果出现以上错误提示，请根据错误提示调整实例。

## 支付完成后多久能完成按量付费转包年包月？ {#section_07w_jp4_rlu .section}

支付完成后，会有异步任务执行转换操作。目前同时转换1~20个实例的计费方式所需时间为1~4秒。转换完成后，您可以在控制台上看到实例的计费方式已经更新为**包年包月**。

## 按量付费转包年包月失败时如何处理？ {#section_ulz_fn2_oxb .section}

请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex?spm=a2c4g.11186623.2.7.8oI1Ug)。

## 按量付费转包年包月之后带宽计费方式是否发生变化？ {#section_4lm_u5o_2my .section}

不变。按量付费转包年包月功能只支持转换实例和云盘的计费方式，带宽计费方式的变更方法请参见[变更公网带宽计费方式](cn.zh-CN/实例/升降配实例/升降配方式汇总.md#ChangeBilling)。

## 我有一个按量付费转包年包月订单，但是还没有支付，这时我升级了实例的配置，转换订单还有效吗？ {#section_tih_umb_qaz .section}

按量付费转包年包月时会创建一个新购订单，您必须支付该订单才能正常完成转换。如果您在未支付订单时升级了实例配置，由于实例组件已经发生变化，原订单的金额已经无法满足转换要求，此时订单会被禁止支付。如果您仍然需要转换实例的计费方式，必须先作废当前未支付订单，再执行新的转换操作。

## 包年包月转按量付费失败时如何处理？ {#section_xqt_ua4_1cf .section}

以下情况都会造成转换失败：

-   实例当前状态不支持转换。
-   实例当前处于**已过期**状态，不支持转换。
-   实例的信息发生变化，不允许转换。

如果出现以上明确的错误提示，建议您根据错误提示调整实例。如果问题仍旧存在，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

## 新创建的包年包月实例在5天内转为按量付费，属于5天无理由退款吗？ {#section_kfr_lv0_ois .section}

不属于。包年包月转按量付费后您依旧在使用实例。关于5天无理由退款的规则请参见[5天无理由退款说明（ECS）](https://help.aliyun.com/knowledge_detail/37096.html)。

## 为什么更改硬盘收费方式提示三次机会已用完？ {#section_bxy_dkr_1f9 .section}

每个包年包月ECS实例最多只能执行3次实时降配操作。实时降配操作包括：实例规格配置、降低带宽配置、云盘付费方式转按量付费。

## 为什么无法将按量付费实例转为包年包月实例？ {#section_vlz_58s_9es .section}

待转换的ECS实例需要满足以下条件：

-   不能是系列I实例规格，也不能是n1、n2、e3实例规格族中的任一种实例规格。具体实例规格描述请参见[系列I实例规格](../cn.zh-CN/实例/选择实例规格/已停售的实例规格.md#section_ilt_c3h_4gb)和[入门级实例 n1/n2/e3](../cn.zh-CN/实例/选择实例规格/已停售的实例规格.md#section_z2t_5ch_4gb)。
-   不能是抢占式实例。
-   不能有未完成的转换订单。

    如果实例有未支付的转换订单，您必须作废这个未支付的订单后才能执行新的转换操作。

-   没有设置自动释放时间。

    如果实例已经设置过自动释放时间，您必须先关闭自动释放设置才能进行转换操作。如何关闭自动释放，请参见[关闭自动释放](../cn.zh-CN/实例/管理实例/释放实例.md#section_mqg_ccn_xdb)。

-   归属于您的账号下。
-   状态为**运行中**或**已停止**。

    如果您在ECS实例处于**运行中**或**已停止**时下单成功，但是在支付未完成时实例状态发生了变化不再处于上述状态，支付会失败，从而导致计费方式转换失败。当实例重新处于上述状态时，您可以去订单中心重新支付这个订单。


## 如何查询实例到期时间？ {#section_8hf_t8x_5n3 .section}

您可以在ECS控制台实例列表页面的**付费方式**列查看包年包月实例的到期时间。

**说明：** 如果没有**付费方式**列，则在页面右上方单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441753726_zh-CN.png)按钮，勾选**付费方式**，并单击**确定**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156688441753728_zh-CN.png)

