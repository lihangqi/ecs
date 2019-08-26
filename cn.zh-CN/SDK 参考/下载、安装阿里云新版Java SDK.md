# 下载、安装阿里云新版Java SDK {#concept_34917_zh .concept}

相较于旧版 Java SDK 直接开放下载，阿里云新版 Java SDK 采用了 Maven 的方式分发，阿里云旗下所有的 Java SDK 都统一在了一个 Maven 库中，方便统一管理。

以 Windows7 64 位与 Eclipse Luna 为例，下载 Java SDK 的示例步骤如下。

1.  访问 [Maven 官方下载页面](http://maven.apache.org/download.cgi) 下载对应操作系统的 Maven 软件。Checksum 文件可供您校验下载文件是否正确无误。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713402_zh-CN.png)

2.  打开 [Java SDK 下载页面](http://develop.aliyun.com/sdk/java)，将阿里云的 SDK 存放的 Maven 库加入到 Maven 软件中。找到之前下载的 Maven 压缩包并解压，将阿里云的 Maven 库信息添加到 conf 文件夹下的 settings.xml 中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713403_zh-CN.png)

3.  在 Eclipse 添加一个 Maven 项目或将已有的项目转换为 Maven 项目。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713404_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713405_zh-CN.jpg)

4.  打开项目下的 pom.xml 文件，将 Maven 的 dependency 加入到其中，可以通过图形化界面也可以直接编辑 pom.xml 文件添加。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713406_zh-CN.jpg)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759713407_zh-CN.jpg)

5.  保存之后就可以看到在项目下的 Maven Dependencies 中自动下载并加入了阿里云的 SDK jar 包了。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/153909759813408_zh-CN.jpg)


## 如何快速判断旧版和新版 SDK { .section}

可以通过下表中的 SDK 参数快速识别 SDK 版本。

|对比项|旧版 SDK|新版 SDK|
|:--|:-----|:-----|
|提交操作请求的方法|execute\(\)|getAcsResponse\(\)|
|存放 AccessKey 和 AccessKeySecret 的类|AliyunClient|IClientProfile|
|生成存放凭据对象的方法|new DefaultAliyunClient\(APIUrl, Access Key, Access Key Secret\)|DefaultProfile.getProfile\(RegionId, Access Key, Access Key Secret\)|
|包名前缀|com.aliyun.api|com.aliyuncs|

若您使用的是旧版 SDK，建议您切换为新版 SDK，以便获得最新功能。

