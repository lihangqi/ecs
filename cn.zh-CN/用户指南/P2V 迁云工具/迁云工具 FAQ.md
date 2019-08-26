# 迁云工具 FAQ {#ServerMigrationFAQ .reference}

-   [我在什么场景下可以使用迁云工具？](#)
-   [迁云工具的迁移过程是什么？](#)
-   [迁云工具是否支持断点续传？](#)
-   [迁云工具是否支持迁移增量数据？](#)
-   [迁云完成后的结果是什么？](#)
-   [迁移完成得到自定义镜像后该如何操作？](#)
-   [如何处理迁云中断或提示失败？](#)
-   [关于中转实例，我需要注意什么？](#)
-   [关于user\_config.json，我需要注意什么？](#)
-   [什么时候需要过滤目录或文件？](#)
-   [关于client\_data文件，我需要注意什么？](#)
-   [什么时候需要清理client\_data文件？](#)
-   [迁云完成后再次迁云该如何操作？](#)
-   [误释放了中转实例怎么办？](#)
-   [为什么提示账号余额不足NotEnoughBalance？](#)
-   [为什么提示RAM权限不足Forbidden.RAM？](#)
-   [为什么提示子账号权限不足Forbidden.SubUser？](#)
-   [我的服务器在出方向需要访问哪些公网地址和端口？](#)
-   [迁移Windows服务器后怎么检查系统？](#)
-   [阿里云支持激活哪些Windows服务器许可证？](#)
-   [迁移Linux服务器前怎么检查是否满足迁云条件？](#)
-   [迁移Linux服务器后怎么检查系统？](#)

 **1. 我在什么场景下可以使用迁云工具？** 

迁云工具可以将物理服务器、虚拟机以及其他云平台云主机一站式地迁移到阿里云ECS，支持迁移主流Windows和Linux操作系统。更多详情，请参阅 [什么是迁云工具与P2V](intl.zh-CN/用户指南/P2V 迁云工具/什么是迁云工具.md#)。

 **2. 迁云工具的迁移过程是什么？** 

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/154872628213350_zh-CN.png)

-   检查源服务器是否满足迁移条件。
-   在您的云账号下创建一台临时中转实例，将源服务器系统数据传输到中转实例。
-   从中转实例打快照制作自定义镜像。

 **3. 迁云工具是否支持断点续传？** 

支持。数据传输中断后，重新运行迁云工具即可继续迁云。

 **4. 迁云工具是否支持迁移增量数据？** 

不支持。建议在迁云前先暂停如数据库或容器服务之类的应用，或者先 [过滤](#Excludes) 相关数据目录，迁云完成后再同步数据。

 **5. 迁云完成后的结果是什么？** 

生成一份源服务器操作系统的自定义镜像，您可以登录 [ECS管理控制台](https://ecs.console.aliyun.com/)，在相应地域的镜像列表中查看。

 **6. 迁移完成得到自定义镜像后该如何操作？** 

建议先使用该镜像创建一台按量付费的实例，检查系统是否正常。确认镜像可用后，选择合适您业务的 [实例规格](../intl.zh-CN/产品简介/实例规格族.md#) 并 [创建一台或多台ECS实例](intl.zh-CN/用户指南/实例/创建实例/使用向导创建实例.md#)。

**7. 如何处理迁云中断或提示失败？**

-   当迁云工具程序异常退出或者迁云进度卡顿时，可以尝试重新运行迁云工具恢复迁云。

-   如果迁云失败并提示`Not Finished`，您可以查看Logs目录下的日志文件，并参阅 [排查故障](intl.zh-CN/用户指南/P2V 迁云工具/问题排查.md#) 或者 [API错误中心](https://error-center.alibabacloud.com/status/product/Ecs) 查看报错原因。

    如果问题仍未解决，建议您添加 [迁云工具支持钉钉群](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.x8X0fd&code=ca190154ff)。也可以 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 并附上日志信息，联系售后客服支持。


**8. 关于中转实例，我需要注意什么？**

-   迁云工具自动创建、启动、停止和释放中转实例INSTANCE\_FOR\_GOTOALIYUN。为保证顺利完成迁云，请勿人为干预中转实例的运行状态。

-   中转实例的默认安全组在入方向开放了8080和8703端口，这是中转实例的迁云服务端口，请勿修改或删除该安全组配置。

-   迁云完成后，中转实例会被自动释放，如果迁云失败，需要手动 [释放实例](intl.zh-CN/用户指南/实例/释放实例.md#)。


 **9. 关于user\_config.json，我需要注意什么？** 

如果已经开始迁云，并且中转实例已经创建，请勿修改user\_config.json里的系统盘大小或数据盘大小数量配置。如果仍然需要修改，必须清理client\_data文件后重新迁云。

 **10. 什么时候需要过滤目录或文件？** 

源服务器中有不需要上传的数据目录或文件，可以通过配置Excludes文件过滤，提高迁云效率。

特别地，您可以过滤无法暂停的数据库、Docker容器或者处于活动状态的数据目录或文件，以提高数据传输的稳定性。

 **11. 关于client\_data文件，我需要注意什么？** 

client\_data文件记录了迁云过程数据，包含中转实例信息、迁云进度等。一般情况下请不要手动修改或删除client\_data文件，否则可能会导致迁云失败。

 **12. 什么时候需要清理client\_data文件？** 

清理client\_data文件可以使用 [CLI命令](intl.zh-CN/用户指南/P2V 迁云工具/CLI参数.md#) `--cleardata`，或者通过 [Windows GUI](intl.zh-CN/用户指南/P2V 迁云工具/迁云工具 Windows GUI 版本介绍.md#) 的Client Client Data菜单项。

-   迁云已经开始后如果想重新迁云，可以清理现有的client\_data文件或者使用原始的client\_data文件覆盖后再运行。

-   同时在某些迁云失败的情况下，如误释放中转实例、VPC、虚拟交换机或者安全组不存在等，可以尝试清理client\_data操作来解决。


 **13. 迁云完成后再次迁云该如何操作？** 

清理client\_data数据文件，然后运行迁云工具重新迁云。

 **14. 误释放了中转实例怎么办？** 

清理client\_data数据文件，然后运行迁云工具重新迁云。

 **15. 为什么提示账号余额不足NotEnoughBalance？** 

迁云工具本身是免费的，但迁云时默认创建 [按量付费](../intl.zh-CN/产品定价/按量付费.md#) 中转实例。根据阿里云收费服务标准，创建按量付费实例需要您的云账号余额不低于100元人民币。

 **16. 为什么提示RAM权限不足Forbidden.RAM？** 

您的RAM账号创建的AccessKey没有管理ECS和VPC资源的权限。建议您联系主账号授权 [`AliyunECSFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunECSFullAccess/info) 和 [`AliyunVPCFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunVPCFullAccess/info) 角色策略。

 **17. 为什么提示子账号权限不足Forbidden.SubUser？** 

迁云工具需要使用账号AccessKeyID和AccesKeySecret创建中转实例，该操作属于下单操作。RAM账户没有下单权限时会出现报错Forbidden.SubUser。建议您迁云时使用主账号AccessKey。

**18. 我的服务器在出方向需要访问哪些公网地址和端口？**

确认源服务器能访问以下服务地址IP端口：

-   云服务器 ECS：`https://ecs.aliyuncs.com` 443 端口。有关其他地域 ECS 服务地址，请参见[接入地址](../intl.zh-CN/API参考/HTTP调用方式/请求结构.md#)。
-   专有网络 VPC：`http://vpc.aliyuncs.com` 443 端口。
-   安全凭证 STS：`https://sts.aliyuncs.com` 443 端口。
-   中转实例：公网 IP 地址 8080 和 8703 端口。使用 [VPC 内网迁移](intl.zh-CN/用户指南/P2V 迁云工具/VPC内网迁云.md#) 方案时，访问私有 IP 地址。

**说明：** 源服务器不需要开放任何入方向的端口，但是需要在出方向访问上述公网地址和端口。

 **19. 迁移Windows服务器后怎么检查系统？** 

迁移Windows系统后初次启动实例时：

1.  检查系统盘数据是否完整。

2.  如果有数据盘缺失，进入磁盘管理检查盘符是否丢失。

3.  等待文件系统权限修复过程完成后，选择是否重启实例：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/154872628213956_zh-CN.png)

    **说明：** 初次启动ECS实例后，如果文件系统权限修复程序未自启动，您可以运行C:\\go2aliyun\_prepare\\go2aliyun\_restore.exe手动修复。执行前要确保实例上的磁盘数量和盘符路径跟源系统保持一致。

4.  检查网络服务是否正常。

5.  检查其他系统应用服务是否正常。


 **20. 阿里云支持激活哪些Windows Server？** 

支持自动激活Windows Server 2003、2008、2012和2016。其他不在此列版本的Windows如果迁移至ECS，需要 [申请许可移动性证](https://www.alibabacloud.com/help/doc-detail/84749.html)。

 **21. 迁移Linux服务器前怎么检查是否满足迁云条件？** 

可以使用迁云工具里面自带的client\_check工具检测，运行`./client_check --check`命令即可，如果所有检测项提示`OK`则表示满足迁云条件。

 **22. 迁移Linux服务器后怎么检查系统？** 

迁移Linux系统后初次启动实例时：

1.  检查系统盘数据是否完整。

2.  如果有数据盘，您需要自行 [挂载数据盘](intl.zh-CN/用户指南/云盘/挂载云盘.md#)。

3.  检查网络服务是否正常。

4.  然后检查其他系统服务是否正常。


