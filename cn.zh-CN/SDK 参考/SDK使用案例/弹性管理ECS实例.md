# 弹性管理ECS实例 {#concept_vll_rmk_kfb .concept}

您除了可以通过 ECS管理控制台创建或管理ECS实例外，您也能通过 API 管理或定制开发 ECS 实例。阿里云提供了 SDK 来包装API，将云服务器 ECS 的管理集成到已有系统中。本文基于 Python 的开发来说明如何通过API 管理 ECS 实例。如果您没有 Python 开发经验，也能通过本文完成云服务的开发。

## 获取 RAM 子账号 AK 密钥 {#section_jyl_zmk_kfb .section}

使用API管理ECS实例，您需要能访问ECS资源的API密钥（AccessKey ID 和 AccessKey Secret）。为了保证云服务的安全，您需要创建一个能访问ECS资源的RAM用户，获取该用户的AccessKey密钥，并使用这个RAM用户和API管理ECS实例。

以下是获取RAM用户AccessKey密钥的操作步骤：

1.  [创建RAM用户并获取AccessKey密钥](../../../../intl.zh-CN/快速入门/创建 RAM 用户.md#)。
2.  [为RAM用户授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md#)，授予RAM用户管理云服务器服务（ECS）的权限。

## 安装 ECS Python SDK {#section_qwy_cnk_kfb .section}

首先确保您已经具备Python的Runtime，本文中使用的Python版本为2.7+。

```
pip install aliyun-python-sdk-ecs
```

如果提示您没有权限，请切换sudo继续执行。

```
sudo pip install aliyun-python-sdk-ecs
```

本文使用的SDK版本为2.1.2。

## Hello Alibaba Cloud {#section_ix2_gnk_kfb .section}

创建文件 hello\_ecs\_api.py。为了使用SDK，首先实例化AcsClient对象，这里需要RAM用户的AccessKey ID和AccessKey Secret。

**说明：** AccessKey ID和AccessKey Secret是RAM用户访问阿里云ECS服务API的密钥，具有该账户完全的权限，请妥善保管。

```
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.DescribeRegionsRequest import DescribeRegionsRequest
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
```

完成实例化后可以进行第一个应用的开发。查询当前账号支持的地域列表。具体的文档参见 [查询可用地域列表](../../../../intl.zh-CN/API 参考/地域/DescribeRegions.md#)。

```
def hello_aliyun_regions():
    request = DescribeRegionsRequest()
    response = _send_request(request)
    region_list = response.get('Regions').get('Region')
    assert response is not None
    assert region_list is not None
    result = map(_print_region_id, region_list)
    logging.info("region list: %s", result)
def _print_region_id(item):
    region_id = item.get("RegionId")
    return region_id
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
hello_aliyun_regions()
```

在命令行运行 `python hello_ecs_api.py` 会得到当前支持的 Region列表。类似的输出如下：

```
[u'cn-shenzhen', u'ap-southeast-1', u'cn-qingdao', u'cn-beijing', u'cn-shanghai', u'us-east-1', u'cn-hongkong', u'me-east-1', u'ap-southeast-2', u'cn-hangzhou', u'eu-central-1', u'ap-northeast-1', u'us-west-1']
```

## 查询当前的 Region 下的 ECS 实例列表 {#section_anw_knk_kfb .section}

查询实例列表和查询 Region 列表非常类似，替换入参对象为DescribeInstancesRequest 即可，更多的查询参数参考 [查询实例列表](../../../../intl.zh-CN/API 参考/实例/DescribeInstances.md#)。

```
def list_instances():
    request = DescribeInstancesRequest()
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        result = map(_print_instance_id, instance_list)
        logging.info("current region include instance %s", result)
def _print_instance_id(item):
    instance_id = item.get('InstanceId');
    return instance_id
```

输出结果为如下：

```
current region include instance [u'i-****', u'i-****'']
```

更多的API参考 [ECS API 概览](../../../../intl.zh-CN/API 参考/API 概览.md#)，您可以尝试作一个 [查询磁盘列表](../../../../intl.zh-CN/API 参考/磁盘/DescribeDisks.md#)，将实例的参数替换为 DescribeDisksRequest。

## 完整代码示例 {#section_wvk_4nk_kfb .section}

以上操作完整的代码示例如下所示。

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.DescribeRegionsRequest import DescribeRegionsRequest
# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
# sample api to list aliyun open api.
def hello_aliyun_regions():
    request = DescribeRegionsRequest()
    response = _send_request(request)
    if response is not None:
        region_list = response.get('Regions').get('Region')
        assert response is not None
        assert region_list is not None
        result = map(_print_region_id, region_list)
        logging.info("region list: %s", result)
# output the instance owned in current region.
def list_instances():
    request = DescribeInstancesRequest()
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        result = map(_print_instance_id, instance_list)
        logging.info("current region include instance %s", result)
def _print_instance_id(item):
    instance_id = item.get('InstanceId');
    return instance_id
def _print_region_id(item):
    region_id = item.get("RegionId")
    return region_id
# send open api request
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
if __name__ == '__main__':
    logging.info("Hello Aliyun OpenApi!")
    hello_aliyun_regions()
    list_instances()
```

如您想了解 ECS 中 API 的其它操作，请参考 [ECS中的API操作](../../../../intl.zh-CN/API 参考/简介.md#)。

