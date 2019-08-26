# DiskDeviceMapping {#DiskDeviceMapping .reference}

描述镜像和快照的关系。

## 节点名 {#section_jtq_ggp_ydb .section}

接口决定

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SnapshotId|String|快照ID|
|Size|String|生成磁盘的大小|
|Device|String|生成磁盘的Device信息：比如/dev/xvdb|
|Format|String|镜像格式|
|ImportOSSBucket|String|导入镜像的oss的bucket|
|ImportOSSObject|String|导入镜像文件的所属OSS的object|

