# 时间配置：NTP服务器与其他基础服务 {#TimeCalibrationNTP .reference}

阿里云ECS提供了内网NTP服务器，对于阿里云以外的设备，阿里云同时提供了公网NTP服务器，供互联网上的设备使用。

## 内网和公网NTP服务器 {#section_oh2_y5t_hfb .section}

ECS为您提供了高精度的时间参考NTP服务器，其中`ntp.cloud.aliyuncs.com`服务器在地域级别上提供原子参考钟服务。适合金融、通讯、科研和天文等以时间精度核心的生产行业。

|经典网络内网|专有网络VPC内网|公网|
|:-----|:--------|:-|
|ntp.cloud.aliyuncs.com|ntp1.aliyun.com|
|ntp1.cloud.aliyuncs.com|ntp7.cloud.aliyuncs.com|ntp2.aliyun.com|
|ntp2.cloud.aliyuncs.com|ntp8.cloud.aliyuncs.com|ntp3.aliyun.com|
|ntp3.cloud.aliyuncs.com|ntp9.cloud.aliyuncs.com|ntp4.aliyun.com|
|ntp4.cloud.aliyuncs.com|ntp10.cloud.aliyuncs.com|ntp5.aliyun.com|
|ntp5.cloud.aliyuncs.com|ntp11.cloud.aliyuncs.com|ntp6.aliyun.com|
|ntp6.cloud.aliyuncs.com|ntp12.cloud.aliyuncs.com|ntp7.aliyun.com|

## 其他互联网基础服务 {#section_uh2_y5t_hfb .section}

阿里云还提供了其他的互联网基础服务，如下表所示：

|公共服务|描述|
|----|--|
|公共DNS：223.5.5.5 / 223.6.6.6|域名：`http://www.alidns.com`|
|公共镜像站：`http://mirrors.aliyun.com`|镜像同步频率：每天凌晨2:00−4:00。覆盖了大多数开源软件及Linux发行版。|

