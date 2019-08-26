# 镜像FAQ {#concept_q1j_bty_dhb .concept}

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
-   镜像FAQ
    -   [镜像有哪些功能？](#section_hhl_prx_fhb)
    -   [镜像能带来哪些便利？](#section_owg_qrx_fhb)
    -   [目前镜像支持哪些服务器环境和应用场景？](#section_lfh_rrx_fhb)
    -   [镜像是否安全？](#section_sdd_srx_fhb)
    -   [选择了镜像后能更换吗？](#section_ovb_trx_fhb)
    -   [镜像安装使用过程中出问题了怎么办？](#section_kl5_trx_fhb)
-   自定义镜像FAQ
    -   [如何查看数据盘？](#section_hrq_fgx_fhb)
    -   [如何卸载（umount）和删除disk table里的数据？](#section_lzy_rgx_fhb)
    -   [如何确认已经卸载数据盘，并可以新建自定义镜像？](#section_wdy_3ty_dhb)
    -   [实例释放后，自定义镜像是否还存在？](#section_qbd_ghx_fhb)
    -   [实例释放后，快照是否还存在？](#section_uw5_ghx_fhb)
    -   [用于创建自定义镜像的实例到期或释放数据后，创建的自定义镜像是否受影响？使用自定义镜像开通的实例是否受影响？](#section_zc5_shx_fhb)
    -   [使用自定义镜像创建的实例是否可以更换操作系统？更换系统后原来的自定义镜像是否还可以使用？](#section_j1z_thx_fhb)
    -   [更换系统盘时另选操作系统，是否可以使用自定义镜像？](#section_b21_zhx_fhb)
    -   [已创建的自定义镜像，是否可以用于更换另一台云服务器ECS的系统盘数据？](#section_cv1_g3x_fhb)
    -   [是否可以升级自定义镜像开通的云服务器ECS的 CPU、内存、带宽、硬盘等？](#section_y35_m3x_fhb)
    -   [是否可以跨地域使用自定义镜像？](#section_twm_n3x_fhb)
    -   [包年包月实例的自定义镜像，是否可以用于创建按量付费的云服务器ECS？](#section_t5m_cjx_fhb)
    -   [如果使用自定义镜像创建了ECS实例，我可以删除这个镜像吗？](#section_rzt_hct_xdb)
-   复制镜像FAQ
    -   [什么情况下需要复制镜像？](#section_pbs_h4c_ghb)
    -   [可以复制哪些镜像？](#section_j4j_n4c_ghb)
    -   [当前有哪些支持复制镜像功能的地域？](#section_jcb_44c_ghb)
    -   [复制一个镜像大概需要多久？](#section_wzx_44c_ghb)
    -   [复制镜像怎么收费的？](#section_nbz_q4c_ghb)
    -   [在复制镜像过程中，源镜像和目标镜像有什么限制？](#section_inj_s4c_ghb)
    -   [怎么复制我的云账号的镜像资源到其他阿里云账号的其他地域？](#section_kyv_54c_ghb)
    -   [复制镜像有镜像容量限制吗？](#section_k14_x4c_ghb)
-   共享镜像FAQ
    -   [我最多可以获得多少个共享镜像？](#section_xry_y4c_ghb)
    -   [每个镜像最多可以共享给多少个用户？](#section_pwp_ypc_ghb)
    -   [使用共享镜像是否占用我的镜像名额？](#section_agd_2qc_ghb)
    -   [使用共享镜像创建实例的时候存不存在地域限制？](#section_mls_2qc_ghb)
    -   [我曾把自己账号中的某个自定义镜像共享给其他账号，现在我可以删除这个镜像吗？](#section_zv4_fqc_ghb)
    -   [我把某个自定义镜像（M）的共享账号（A）给删除了，会有什么影响？](#section_nfy_jqc_ghb)
    -   [使用共享镜像创建实例存在什么样的风险？](#section_p4w_lqc_ghb)
    -   [我把自定义镜像共享给其他账号，存在什么风险？](#section_r4q_nqc_ghb)
    -   [我能把别人共享给我的镜像再共享给他人吗？](#section_abm_4qc_ghb)
    -   [我把镜像共享给他人，还能使用该镜像创建实例吗？](#section_xny_pqc_ghb)
-   删除镜像FAQ
    -   [如果使用自定义镜像创建了ECS实例，我可以删除这个镜像吗？](#section_rzt_hct_xdb)
-   镜像商业化FAQ
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
    -   [如果没有购买镜像市场的镜像或者来源于镜像市场的镜像，在调用ECS API 使用该镜像创建ECS实例和更换系统盘，会报错吗？](#section_sxt_hsc_ghb)
    -   [我的ESS是自动创建机器的，并且量是不固定，设置最小值为10台，最大值为100台，那么使用镜像市场的镜像如何保证我的的需求实例能正常弹出来？](#section_nfx_5sc_ghb)
    -   [镜像市场的镜像是否支持批量购买？](#section_clp_ysc_ghb)
    -   [如果之前使用的镜像市场的镜像，已不存在该商品（如：jxsc000010、jxsc000019），怎能保证已经设置的弹性伸缩组的机器的正常弹出？](#section_stt_zsc_ghb)
    -   [1个product code能否支持不同region的镜像？](#section_os3_btc_ghb)
    -   [我买了100 product code同样值的镜像，是否可以支持在所有的地域可用？](#section_uzj_ctc_ghb)
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

产品与CentOS 7.6.1810发行版保持二进制兼容，在此基础上提供差异化的操作系统功能。

与CentOS及RHEL相比，差异点体现在：

-   满足您的操作系统新特性诉求，更快的发布节奏，更新的Linux 内核、用户态软件及工具包。
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

Aliyun Linux 2将会保留CentOS 7的数据加密工具包，并确保CentOS 7与KMS协同工作的加密方案可以在Aliyun Linux 2得到支持。

## 怎样设置Aliyun Linux 2的有关权限？ {#section_f41_jqv_fhb .section}

Aliyun Linux 2属于与CentOS 7同源的操作系统。CentOS 7的管理员可以无缝地使用完全一致的管理命令做相关的权限设置，Aliyun Linux 2的缺省权限设置与阿里云CentOS 7镜像完全一致。

## 镜像有哪些功能？ {#section_hhl_prx_fhb .section}

镜像在操作系统基础上预装了软件环境和多种功能，如PHP/.NET/JAVA/LAMP等运行环境、控制面板、建站系统等。将镜像与云服务器配套使用,您只需进行一次简单操作，就可快速部署云服务器的运行环境或软件应用,再也不担心上云难了。

## 镜像能带来哪些便利？ {#section_owg_qrx_fhb .section}

过去，开启云服务器（ECS）后，您需自行配置环境、安装软件，繁琐且耗时。现在通过镜像开通云服务器，一键部署，您可获得与镜像一致的系统环境或软件，便捷地创建就绪的运行环境，同时轻松地搭建并管理站点。

## 目前镜像支持哪些服务器环境和应用场景？ {#section_lfh_rrx_fhb .section}

镜像市场提供上百款优质第三方镜像，不仅全面支持PHP/.NET/JAVA/LAMP/Docke虚拟容器等运行环境的部署，而且满足建站、应用开发、可视化管理等个性化 需求。

## 镜像是否安全？ {#section_sdd_srx_fhb .section}

镜像服务商均有丰富的系统维护和环境配置经验，所有镜像都基于包含云盾的阿里云官方操作系统制作，且预先经过严格安全审核，敬请放心使用。

## 选择了镜像后能更换吗？ {#section_ovb_trx_fhb .section}

可以更换。在ECS控制台，选择更换系统盘，即可选择所需的镜像进行更换。请注意，更换镜像会导致系统盘数据丢失，请在确认更换前做好数据备份。

## 镜像安装使用过程中出问题了怎么办？ {#section_kl5_trx_fhb .section}

查看购买页的服务信息，通过在线旺旺、电话或邮箱直接与镜像服务商联系，实时解答您的疑问。

## 如何查看数据盘？ {#section_hrq_fgx_fhb .section}

您可以通过df命令查看数据盘的使用情况，以及文件系统被挂载的位置。例如：df –lh。

您可以通过fdisk命令获取数据盘的分区情况。例如：fdisk -l

## 如何卸载（umount）和删除disk table里的数据？ {#section_lzy_rgx_fhb .section}

假设/dev/hda5已经挂载在/mnt/hda5上，您可以使用下列任一命令卸载已挂载的文件系统：

```
umount /dev/hda5
umount /mnt/hda5
umount /dev/hda5 /mnt/hda5
```

/etc/fstab是Linux系统下比较重要的配置文件，其包含了系统在启动时挂载的文件系统和存储设备的详细信息。

当您不想在启动实例时挂载指定分区，需要删除当前文件中对应的语句行。例如，删除下面的语句可以在启动的时候断开xvdb1：

```
/dev/xvdb1 /leejd ext4 defaults 0 0
```

Linux其他较重要的配置文件如下：

|配置文件|配置说明|修改该配置文件的风险|
|:---|:---|:---------|
|/etc/issue\*, /etc/\*-release, /etc/\*\_version|系统发行版信息配置文件|修改/etc/issue\*会导致系统发行版无法被正常识别，导致系统创建失败。|
|/boot/grub/menu.lst, /boot/grub/grub.conf|系统引导启动配置文件|修改/boot/grub/menu.lst会导致内核无法正确加载，导致系统无法启动。|
|/etc/fstab|系统启动挂载分区配置文件|修改该文件会导致异常分区无法被加载，导致系统无法启动。|
|/etc/shadow|系统密码相关配置文件|修改该文件为只读会导致无法修改密码文件，导致系统创建失败。|
|/etc/selinux/config|系统安全策略配置文件|修改/etc/selinux/config开启SELinux导致系统无法启动。|

## 如何确认已经卸载数据盘，并可以新建自定义镜像？ {#section_wdy_3ty_dhb .section}

1.  确认/etc/fstab文件中对应的自动挂载数据盘分区语句行已被删除。
2.  使用mount命令查看所有设备的挂载信息，请确认执行结果中不包含对应的数据盘分区信息。

## 实例释放后，自定义镜像是否还存在？ {#section_qbd_ghx_fhb .section}

存在。

## 实例释放后，快照是否还存在？ {#section_uw5_ghx_fhb .section}

保留手动快照，自动快照会随着实例释放而被清除。更多详情，请参见[快照FAQ](../../../../../cn.zh-CN/快照/常见问题/快照FAQ.md#)。

## 用于创建自定义镜像的实例到期或释放数据后，创建的自定义镜像是否受影响？使用自定义镜像开通的实例是否受影响？ {#section_zc5_shx_fhb .section}

均不受影响。

## 使用自定义镜像创建的实例是否可以更换操作系统？更换系统后原来的自定义镜像是否还可以使用？ {#section_j1z_thx_fhb .section}

可以。更换后原来的自定义镜像还可以继续使用。

## 更换系统盘时另选操作系统，是否可以使用自定义镜像？ {#section_b21_zhx_fhb .section}

可以。详情请参见[更换系统盘（非公共镜像）](../../../../../cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

**说明：** 系统盘更换为自定义镜像后，原来的数据将被全覆盖。

## 已创建的自定义镜像，是否可以用于更换另一台云服务器ECS的系统盘数据？ {#section_cv1_g3x_fhb .section}

可以。详情请参见[更换系统盘（非公共镜像）](../../../../../cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

**说明：** 自定义镜像将全部覆盖该服务器系统盘的所有数据。

## 是否可以升级自定义镜像开通的云服务器ECS的 CPU、内存、带宽、硬盘等？ {#section_y35_m3x_fhb .section}

均可以升级。

## 是否可以跨地域使用自定义镜像？ {#section_twm_n3x_fhb .section}

不可以。自定义镜像只能在同一个地域使用。例如：使用华东1地域的实例创建的自定义镜像，不可以直接用来开通华东2地域的云服务器ECS。

如果您需要跨地域使用自定义镜像，可以先复制镜像到目标地域，请参见[复制镜像](../../../../../cn.zh-CN/镜像/自定义镜像/复制镜像.md#)。

## 包年包月实例的自定义镜像，是否可以用于创建按量付费的云服务器ECS？ {#section_t5m_cjx_fhb .section}

可以。自定义镜像功能不区分实例的付费方式，即不区分是否包年包月或按量付费。

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
-   复制过来的快照会占用快照容量。目前快照容量已经收费，详情请参见[快照计费方式](../../../../../cn.zh-CN/产品定价/快照计费方式.md#)。

## 在复制镜像过程中，源镜像和目标镜像有什么限制？ {#section_inj_s4c_ghb .section}

在复制过程中，源镜像禁止删除，目标镜像可以取消复制，不能用于更换系统盘和创建ECS实例。

## 怎么复制我的云账号的镜像资源到其他阿里云账号的其他地域？ {#section_kyv_54c_ghb .section}

您需要复制自己的镜像到目标地域，并将该镜像共享给对方的云账号。对方云账号的共享镜像列表中会显示该镜像。

## 复制镜像有镜像容量限制吗？ {#section_k14_x4c_ghb .section}

没有限制。但是，复制容量超过500 GiB时需要提交工单申请，当您在控制台单击**复制镜像**时，控制台会提示您提交工单申请。

## 我最多可以获得多少个共享镜像？ {#section_xry_y4c_ghb .section}

100个。

## 每个镜像最多可以共享给多少个用户？ {#section_pwp_ypc_ghb .section}

50个。

## 使用共享镜像是否占用我的镜像名额？ {#section_agd_2qc_ghb .section}

不占用。

## 使用共享镜像创建实例的时候存不存在地域限制？ {#section_mls_2qc_ghb .section}

有地域限制。同一个共享源，地域也应该相同。

## 我曾把自己账号中的某个自定义镜像共享给其他账号，现在我可以删除这个镜像吗？ {#section_zv4_fqc_ghb .section}

可以删除。但是当您删除共享镜像后，使用该共享镜像创建的ECS实例都不能重新初始化系统盘。所以，建议您把该自定义镜像的所有关系删除后再删除镜像。

## 我把某个自定义镜像（M）的共享账号（A）给删除了，会有什么影响？ {#section_nfy_jqc_ghb .section}

您将无法通过ECS控制台或者ECS API查询到共享镜像M。无法使用镜像M创建ECS实例和更换系统盘。如果账号A 在删除共享关系前，使用镜像M创建了ECS实例，那么这些实例将不能重新初始化系统盘。

## 使用共享镜像创建实例存在什么样的风险？ {#section_p4w_lqc_ghb .section}

镜像拥有者可以查看该镜像的共享关系，也可以删除该镜像。共享镜像被拥有者删除后，会导致使用共享镜像的ECS实例不能重新初始化系统盘。

阿里云不保证其他账号共享镜像的完整性和安全性，使用共享镜像时您需要自行承担风险，请您选择信任的账号共享的镜像。使用共享镜像创建ECS实例时，您需要登录该ECS实例检查一下共享镜像的安全性和完整性。

## 我把自定义镜像共享给其他账号，存在什么风险？ {#section_r4q_nqc_ghb .section}

有数据泄露和软件泄露的风险。在共享给其他账号之前，请确认该镜像上是否存在敏感的和安全的重要数据和软件。得到您的共享镜像的账号，可以用这个共享镜像创建ECS实例，还可以用这个ECS实例创建更多自定义镜像，其中的数据会不停传播，造成泄露风险。

## 我能把别人共享给我的镜像再共享给他人吗？ {#section_abm_4qc_ghb .section}

不能。只有镜像的拥有者才能共享给其他账号。

## 我把镜像共享给他人，还能使用该镜像创建实例吗？ {#section_xny_pqc_ghb .section}

可以。您将镜像共享给其他账号后，还可以用该镜像创建ECS实例，在该ECS实例的基础上也可以继续创建自定义镜像。

## 如果使用自定义镜像创建了ECS实例，我可以删除这个镜像吗？ {#section_rzt_hct_xdb .section}

您可以**强制删除**这个镜像。但是，删除镜像后，使用该自定义镜像创建的ECS实例无法 [ZH-CN\_TP\_9679.md\#](cn.zh-CN/块存储/云盘/重新初始化云盘.md#)。

## 如何购买镜像市场镜像？ {#section_hxc_rqc_ghb .section}

您可以在镜像市场单独购买，也可以在ECS售卖页面和ECS实例同时购买。

## 按次购买的镜像的使用期限是多久？ {#section_hqw_prc_ghb .section}

原则上可以一直使用，但要需要注意，镜像作为一种软件有自身的生命周期，另外服务商提供的服务支持实际上是有期限的，具体应以商品上的描述为准。

## 镜像市场的镜像支持退款吗？ {#section_gzm_qrc_ghb .section}

镜像按照云市场统一规则支持有限时间内无理由退款，但出现以下情况时不予退款：

-   在无理由退款时限内将购买的镜像部署在了云服务器上。
-   在提交退款的申请审批确认前，将购买的镜像部署在了云服务器上。
-   也就是说，镜像在不被使用的状态下可以退款。

## 镜像市场商业化后，还有免费的镜像市场镜像吗？ {#section_okl_src_ghb .section}

镜像市场还会存在一定数量的免费的镜像，可以放心使用。0元的镜像也需要购买后才能使用。

## 在杭州买了一个镜像市场的镜像，能否在北京创建ECS实例或者更换系统盘？ {#section_ndz_src_ghb .section}

不可以，购买的镜像市场镜像只能在相同地域进行创建ECS实例或者更换系统盘。

## ECS实例使用镜像市场的镜像，升级和续费ECS实例，需要为镜像继续付费吗？ {#section_jwc_fsx_fhb .section}

不需要付费，购买一个镜像可以一直使用在ECS实例上，不需要在续费。

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

    如果您使用的镜像的镜像商品标示（`ProductCode`）不为空，表示该镜像是镜像市场的镜像或者来源于镜像市场的自定义镜像或者共享镜像。如果使用的镜像的商品标示ProductCode为abcd000111，您可以访问镜像商品的地址`http://market.aliyun.com/products/123/abcd000111.html`

2.  需要选择镜像的版本和正确地域，只购买ECS镜像。

    购买某一地域的镜像只能使用在该地域的ECS实例上。当前每次只能购买一个镜像，如果需要创建多个ECS实例，则需要购买多个镜像。

3.  购买完成后，您可以创建ECS实例和更换系统盘。

## 如果没有购买镜像市场的镜像或者来源于镜像市场的镜像，在调用ECS API 使用该镜像创建ECS实例和更换系统盘，会报错吗？ {#section_sxt_hsc_ghb .section}

会报错，错误码为`QuotaExceed.BuyImage`。

## 我的ESS是自动创建机器的，并且量是不固定，设置最小值为10台，最大值为100台，那么使用镜像市场的镜像如何保证我的的需求实例能正常弹出来？ {#section_nfx_5sc_ghb .section}

如果您需要弹出n台同类型的镜像，您需要提前购买n台镜像市场的镜像。

## 镜像市场的镜像是否支持批量购买？ {#section_clp_ysc_ghb .section}

暂不支持批量购买。

## 如果之前使用的镜像市场的镜像，已不存在该商品（如：jxsc000010、jxsc000019），怎能保证已经设置的弹性伸缩组的机器的正常弹出？ {#section_stt_zsc_ghb .section}

此情况建议您选择镜像市场可以替代的镜像进行替代。

## 1个product code能否支持不同region的镜像？ {#section_os3_btc_ghb .section}

支持，前提是该地域region已经支持该商品镜像。

## 我买了100 product code同样值的镜像，是否可以支持在所有的地域可用？ {#section_uzj_ctc_ghb .section}

目前镜像市场镜像已经具备region属性，请您购买需要使用的地域镜像。

## 什么是镜像市场的包年包月和按周付费镜像？ {#section_zxy_n5c_ghb .section}

镜像市场的包年包月和按周付费镜像是指从阿里云云市场购买的，按周、按月或按年付费使用的镜像。这些镜像由镜像供应商开发并维护，所有售前咨询和售后服务都由镜像供应商提供。在本文中，这类镜像统称为预付费镜像。

## 预付费镜像能与哪种ECS实例搭配使用？ {#section_fts_45c_ghb .section}

预付费镜像只能与包年包月实例和按周付费实例搭配使用，而且镜像与ECS实例的付费周期应保持一致。

## 怎么购买预付费镜像？可以单独购买吗？ {#section_rfp_s5c_ghb .section}

目前您还不能单独购买预付费镜像。

您可以选择以下任一种方式购买预付费镜像：

-   在创建ECS实例时，付费方式选择**包年包月**，并从**镜像市场**选择镜像，再选择按周、按月或按年付费。

    **说明：** 在这种情况下，您需要同时支付实例与镜像的费用。如果实例创建成功，表明您已经同时支付了实例与镜像的费用，不会出现其中一项资源购买失败的情况。

-   如果您想在一台已有的包年包月或按周付费ECS实例上使用预付费镜像，您可以使用更换操作系统 功能将操作系统更换为预付费镜像，此时，您只能按照ECS实例的付费周期选择镜像的付费周期。具体操作方式，请参见[更换系统盘（非公共镜像）](../../../../../cn.zh-CN/块存储/云盘/更换系统盘/更换系统盘（非公共镜像）.md#)。

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

如果可以退款，镜像供应商将按照你的实际使用情况退款。

## 预付费镜像能转换为按量付费镜像吗？ {#section_hpg_1vc_ghb .section}

目前不支持转换为按量付费镜像。后续我们会提供这个功能，具体时间请关注阿里云官网公告。

## 预付费镜像与其它镜像之间能互换吗？更换后费用怎么计算？ {#section_sqw_1vc_ghb .section}

可以。您可以通过ECS实例更换系统盘来更换镜像。更换镜像时有以下几种选择：

-   将其他类别的镜像（如公共镜像、自定义镜像、共享镜像）换成预付费镜像：更换后，系统将按镜像的费用和ECS实例的剩余付费周期计算实际费用。
-   将预付费镜像换成其它类别的镜像（如公共镜像、自定义镜像、共享镜像）：如果供应商允许退款，镜像供应商将按照你的实际使用情况退款。
-   将一个预付费镜像（设为镜像A）换成另一个预付费镜像（设为镜像B）：更换后，如果镜像 A 允许退款，将按退款方式结算费用，镜像B将按镜像的价格和ECS实例剩余付费周期计算实际费用。

## 在哪里查看并管理我购买的预付费镜像？ {#section_fmx_fvc_ghb .section}

您可以登录[云服务器ECS管理控制台](https://ecs.console.aliyun.com)，在**镜像** \> **镜像市场**中查看并管理您购买的预付费镜像。

## 使用预付费镜像制作的自定义镜像会收费吗？预付费镜像过期对于自定义镜像有什么影响？ {#section_klq_gvc_ghb .section}

当您使用由预付费镜像制作的自定义镜像时，无论是使用自定义镜像创建实例，还是更换系统盘，都是重新在镜像市场下单购买镜像的使用权。所以，用于制作自定义镜像的预付费镜像是否过期，对使用自定义镜像没有影响。

## 为什么有的ECS实例无法选择Windows操作系统？ {#section_ajg_qwc_ghb .section}

使用Windows 操作系统创建ECS实例时，需要确保实例内存大于等于1 GiB。内存低于1 GiB的ECS实例（例如， 512 MiB）只能选择Linux镜像和Windows Server 1709镜像。

## ECS实例使用操作系统需要付费吗？ {#section_ttw_qwc_ghb .section}

大陆地域的Windows Server公共镜像自带正版激活，不收取系统正版激活费用，其他国家或地区地域会收取系统正版激活费用。

Windows Server 公共镜像默认最多允许2个会话（Session）[远程连接](../../../../../cn.zh-CN/实例/实例生命周期/连接实例/在本地客户端上连接Windows实例.md#)，如果您新增连接数，请向微软单独购买远程桌面授权（RD授权）服务，该项授权费用需要您自理。

除Red Hat公共镜像外，Linux公共镜像不需要您支付版权费用。

## 我能自己安装或者升级操作系统吗？ {#section_zhs_twc_ghb .section}

不能自行安装或升级。ECS实例需要使用阿里云官方提供的镜像，您无法自行添加或升级。但是您可以

-   更换系统盘重新选择操作系统。具体操作步骤，请参见[../../../../../dita-oss-bucket/SP\_2/DNA0011894323/ZH-CN\_TP\_9640.md\#](../../../../../cn.zh-CN/镜像/更换操作系统.md#)。
-   从本地导入自己的镜像后使用自定义镜像创建ECS实例。导入镜像的操作步骤，请参见[../../../../../dita-oss-bucket/SP\_2/DNA0011894323/ZH-CN\_TP\_9702.md\#](../../../../../cn.zh-CN/镜像/自定义镜像/导入镜像/导入镜像必读.md#)。使用自定义镜像创建ECS实例的操作步骤，请参见[../../../../../dita-oss-bucket/SP\_2/DNA0011894323/ZH-CN\_TP\_9627.md\#](../../../../../cn.zh-CN/实例/实例生命周期/创建实例/使用自定义镜像创建实例.md#)。
-   为操作系统打补丁。

## 操作系统是否有图形界面？ {#section_ulp_xwc_ghb .section}

除Windows Server 1709以外，Windows操作系统是桌面管理形式。有关如何使用Windows Server 1709操作系统，请参见[Windows Server Version 1709 镜像简介与实例管理](https://help.aliyun.com/knowledge_detail/74510.html)。

Linux 操作系统是命令行形式，您可以根据需要安装图形化桌面，请参见[为Linux 实例安装图形化桌面](https://help.aliyun.com/knowledge_detail/41227.html)。

## 如何选择操作系统？ {#section_wqy_zwc_ghb .section}

请参见[ECS 实例操作系统选择说明](https://help.aliyun.com/knowledge_detail/40651.html)。

## 公共镜像自带FTP上传吗？ {#section_jtv_dxc_ghb .section}

不自带，需要您自己安装配置。具体操作，请参见[Windows实例搭建FTP站点](../../../../../cn.zh-CN/建站教程/搭建FTP站点/Windows实例搭建FTP站点.md#)和[Linux实例搭建FTP站点](../../../../../cn.zh-CN/建站教程/搭建FTP站点/Linux实例搭建FTP站点.md#)。

## 阿里云支持哪些SUSE版本？ {#section_mgc_fxc_ghb .section}

目前，阿里云公共镜像支持以下SUSE版本：

-   SUSE Linux Enterprise Server 12 SP2 64位
-   SUSE Linux Enterprise Server 11 SP4 64位

## SUSE操作系统提供哪些服务支持？ {#section_jpr_fxc_ghb .section}

阿里云线上售卖的SLES（SUSE Linux Enterprise Server）操作系统会与SUSE更新源保持定时同步。使用阿里云 SLES公共镜像创建的实例，其操作系统的支持服务涵盖在阿里云的企业级别支持服务中。如果您购买了企业级支持服务，可以提交工单联系阿里云获取帮助，阿里云工程师团队会协助您解决SLES操作系统上发生的问题。

