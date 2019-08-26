# UCloud迁移至阿里云 {#concept_tw3_zgw_fgb .concept}

您可以参考本文档中的步骤，将UCloud云主机迁移至阿里云ECS实例。

## UCloud Windows系统迁移至阿里云 {#section_nlw_bkj_pgb .section}

**准备工作**

1.  请您创建快照以备份您的数据。
2.  确保您的待迁移UCloud云主机能访问下列网址及端口。
    1.  ECS：`https://ecs.aliyuncs.com:443`。

        **说明：** 更多地域的ECS API接入地址，请参见[接入地址](../../../../../intl.zh-CN/API参考/快速入门/请求结构.md#section_mtp_xvb_wdb)。

    2.  VPC：`https://vpc.aliyuncs.com:443`。
    3.  STS：`https://sts.aliyuncs.com:443`。
    4.  ECS中转实例：端口8080和8703。

        **说明：** 中转实例是迁云工具在其运行过程中自动创建的临时实例。迁云过程中出现网络连接问题时，您需要运行以下命令确认待迁移UCloud云主机可以访问中转实例的8080和8703端口。

        ```
        telnet xxx.xx.xxx.xx 8080  #xxx.xx.xxx.xx为中转实例公网IP地址。当使用VPC内网迁移时，xxx.xx.xxx.xx为中转实例私网IP地址。
        telnet xxx.xx.xxx.xx 8703  #xxx.xx.xxx.xx为中转实例公网IP地址。当使用VPC内网迁移时，xxx.xx.xxx.xx为中转实例私网IP地址。
        ```

3.  检查并确保Windows系统VSS服务为启动状态 。
4.  检查是否安装了qemu-agent工具。如果安装了此工具，您需要先卸载。卸载的具体步骤，请参见[迁云工具FAQ](intl.zh-CN/迁移服务/P2V 迁云工具/迁云工具FAQ.md#)。
5.  检查授权应用。迁移到阿里云后，系统底层硬件设备会发生变化，可能会导致一些跟硬件绑定的应用许可证（license）失效，您需要做好检查。
6.  建议您先使用测试机，按照本文中介绍的迁云操作步骤进行测试演练。

**操作步骤**

1.  下载并安装迁云工具到待迁移的服务器。具体步骤请参见[下载并安装迁云工具](../../../../../intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_twq_sxz_jfb)。
2.  配置user\_config.json。

    user\_config.json配置文件的主要配置项包括：

    -   阿里云账号AccessKey信息
    -   迁移目标区域、目标镜像名称
    -   （可选）目标系统盘大小、目标数据盘配置
    -   迁移源系统平台、架构
    各配置项的详细配置方法，请参见[配置迁移源和迁移目标](../../../../../intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_p5x_xzz_jfb)。

3.  （可选）配置无需迁移的目录或文件。具体配置方法，请参见[（可选）排除不迁移的文件或目录](../../../../../intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_tzq_sxz_jfb)。
4.  运行迁云工具主程序。

    以管理员身份运行go2aliyun\_client.exe或go2aliyun\_gui.exe。如果是GUI版本，则需要单击start按钮开始迁移。


## UCloud Linux系统迁移至阿里云 {#section_y41_clj_pgb .section}

**准备工作**

1.  请创建快照以备份您的数据。
2.  确保您的待迁移UCloud云主机能访问下列网址及端口。
    1.  ECS：`https://ecs.aliyuncs.com:443`。

        **说明：** 更多地域的ECS API接入地址，请参阅[接入地址](../../../../../intl.zh-CN/API参考/快速入门/请求结构.md#section_mtp_xvb_wdb)。

    2.  VPC：`https://vpc.aliyuncs.com:443`。
    3.  STS：`https://sts.aliyuncs.com:443`。
    4.  ECS中转实例：端口8080和8703。

        **说明：** 中转实例是迁云工具在其运行过程中自动创建的临时实例。迁云过程中出现网络连接问题时，您需要运行以下命令确认待迁移UCloud云主机可以访问中转实例的8080和8703端口。

        ```
        telnet xxx.xx.xxx.xx 8080  #xxx.xx.xxx.xx为中转实例公网IP地址。当使用VPC内网迁移时，xxx.xx.xxx.xx为中转实例私网IP地址。
        telnet xxx.xx.xxx.xx 8703  #xxx.xx.xxx.xx为中转实例公网IP地址。当使用VPC内网迁移时，xxx.xx.xxx.xx为中转实例私网IP地址。
        ```

3.  检查授权应用。迁移到阿里云后，系统底层硬件设备会发生变化，可能会导致一些跟硬件绑定的应用许可证（license）失效，您需要做好检查。
4.  建议您先使用测试机，按照本文中介绍的迁云操作步骤进行测试演练。

**操作步骤**

1.  下载并解压迁云工具，运行迁云工具中的client\_check脚本，检查待迁移UCloud云主机是否满足迁移条件。具体操作步骤如下：
    1.  运行以下命令将迁云工具下载到待迁移的服务器。

        ```
        wget http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip
        ```

    2.  运行以下命令解压缩迁云工具。

        ```
        unzip Alibaba_Cloud_Migration_Tool.zip
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155477397638160_zh-CN.png)

    3.  运行以下命令查看待迁移Linux系统的型号，并将适用于该系统型号的迁云工具包解压缩。

        ```
        uname -a 
        unzip <适用于待迁移系统型号的迁云工具包>
        ```

        本示例中，Linux型号为 `x86_64`，因此，适用于该系统型号的迁云工具包为 go2aliyun\_client1.3.2.3\_linux\_x86\_64.zip，如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155477397638161_zh-CN.png)

    4.  运行以下命令进入解压后的迁云工具目录。

        ```
        cd <解压后的迁云工具目录>
        ```

        本示例中，该命令为 `cd go2aliyun_client1.3.2.3_linux_x86_64`。

    5.  运行以下命令检测Linux服务器是否满足迁移条件。

        ```
        chmod +x ./Check/client_check
        ./Check/client_check --check
        ```

        如果所有检测项的结果都为OK，表示该服务器满足迁移条件。您可以继续后面的迁移操作。

2.  配置迁移所需参数并运行迁云工具。具体操作步骤如下：
    1.  配置user\_config.json。

        user\_config.json配置文件的主要配置项包括：

        -   阿里云账号AccessKey信息
        -   迁移目标区域、目标镜像名称
        -   （可选）目标系统盘大小、目标数据盘配置
        -   迁移源系统平台、架构
        各配置项的详细配置方法，请参见[配置迁移源和迁移目标](../../../../../intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_p5x_xzz_jfb)。

    2.  （可选）配置无需迁移的目录或文件。具体配置方法，请参见[（可选）排除不迁移的文件或目录](../../../../../intl.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_tzq_sxz_jfb)。
    3.  使用root权限运行以下命令，为迁云工具主程序添加可执行权限并执行该程序。

        ```
        chmod +x go2aliyun_client
        ./go2aliyun_client
        ```

    4.  等待迁云工具运行完成。当运行迁云工具的界面上提示Go to Aliyun Finished!时，表示迁移完成。如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155477397638196_zh-CN.png)


## 常见问题 {#section_ipd_3hw_fgb .section}

问：迁移后的Linux实例为什么不能在ECS控制台正常启动和停止？

答：某些Linux系统内核由UCloud云平台定制，可能与阿里云平台不兼容。您可以更换Linux系统内核，例如，对于CentOS操作系统，您可以更换[CentOS官方内核](http://vault.centos.org/)。您也可以联系[技术支持](https://www.alibabacloud.com/help/doc-detail/96024.htm)。

