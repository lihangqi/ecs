# Disk category {#EcsApiDiskCategroy .reference}

See the following table for the disks provided by ECS.

|Name|Code| Maximum capacity per disk \(GiB\)|Volume limit per instance|Maximum capacity of disks allowed per instance \(GiB\)|
|:---|:---|:---------------------------------|:------------------------|:-----------------------------------------------------|
|Basic cloud disk|cloud|2000|17|2000 \* 17|
|Ultra cloud disks|cloud\_efficiency|32768|17|32768 \* 17|
|SSD cloud disks|cloud\_ssd|32768|17|32768 \* 17|
|ESSD[\*](#Note1)|essd|32768|17|32768 \* 17|

\* Currently, the ESSD disk cannot be managed by calling the Alibaba Cloud ECS API.

For more information, see [Storage parameters and performance test](../../../../intl.en-US/Product Introduction/Block storage/Storage parameters and performance test.md#).

