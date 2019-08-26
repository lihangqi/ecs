# ImageType {#ImageType .reference}

镜像信息的类型。

## 节点名 {#section_pp3_yjp_ydb .section}

Image

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|ImageId|String|镜像编码|
|ImageVersion|String|镜像版本|
|OSType|String|操作系统类型，可选值有：-   windows
-   linux

|
|Platform|String|操作系统平台|
|Architecture|String|镜像系统类型：i386 | x86\_64|
|ImageName|String|镜像的名称|
|Description|String|描述信息|
|Size|Integer|镜像大小|
|ImageOwnerAlias|String|镜像所有者别名有效值：-   system – 系统公共镜像
-   self – 用户的自定义镜像
-   others – 其他用户的公开镜像
-   marketplace -镜像市场镜像

|
|OSName|String|操作系统的显示名称|
|DiskDeviceMappings|[DiskDeviceMapping](intl.zh-CN/API参考/数据类型/DiskDeviceMapping.md#)|镜像下包含磁盘和快照的系统描述|
|ProductCode|String|镜像市场的镜像商品标示|
|IsSubscribed|String|用户是否订阅了该镜像的商品码对应的镜像商品的服务条款.-   true：表示已经订阅
-   false：表示未订阅

|
|Progress|String|镜像完成的进度，单位为百分比|
|Status|String|镜像的状态，可能的值有：-   UnAvailable 不可用
-   Available 可用
-   Creating 创建中
-   CreateFailed 创建失败

|
|CreationTime|String|创建时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mmZ|
|Usage|String|有引用关系的资源类型，instance | none|
|IsCopied|String|是否是拷贝的镜像，true | false|

