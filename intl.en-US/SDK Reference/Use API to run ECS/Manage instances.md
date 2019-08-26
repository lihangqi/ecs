# Manage instances {#concept_vll_rmk_kfb .concept}

In addition to using the ECS console for resource creation and daily management, you can also use API to manage and customize resources. API allows you to manage and configure ECS instances with greater flexibility. Alibaba Cloud encapsulates API in an SDK to integrate ECS instance management into existing systems. This topic describes how to manage ECS instances through API based on Python development. You can develop ECS instances easily even if you do not have Python development experience.

## Get the AccessKey for a RAM user {#section_jyl_zmk_kfb .section}

An AccessKey \(AccessKey ID and AccessKey Secret\) is required when you want to use API to manage ECS instances. To keep your cloud service secure, you have to create a RAM user and generate an AccessKey for it, and authorize the RAM user to manage ECS resources only. Then, you can use the RAM user and its AccessKey to manage ECS resources by using API.

Follow these steps to get the AccessKey for a RAM user:

1.  [Create a RAM user and get the AccessKey](../../../../reseller.en-US/Quick Start/Create a RAM user.md#).
2.  [Grant permissions to the RAM user directly](../../../../reseller.en-US/Quick Start/Authorize RAM users.md#). To manage ECS resources, you have to grant AliyunECSFullAccess to the RAM user.

## Install the ECS Python SDK {#section_qwy_cnk_kfb .section}

Make sure that the Python runtime environment has been installed. This article uses Python 2.7+.

```
pip install aliyun-python-sdk-ecs
```

If you do not have the permission, switch to sudo to continue.

```
sudo pip install aliyun-python-sdk-ecs
```

The SDK version is 2.1.2.

## Hello Alibaba Cloud {#section_ix2_gnk_kfb .section}

Create the file hello\_ecs\_api.py. To use SDK, you have to use the AccessKey of the RAM user to instantialize an AcsClient object.

**Note:** The AccessKey allows the RAM user to access Alibaba Cloud APIs and give you full access to the user. Keep them safe.

```
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. DescribeRegionsRequest import DescribeRegionsRequest
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
```

You can develop your first application after the AcsClient object is instantiated. Query the list of regions that your account supports. For more information, see [query the list of available regions](../../../../reseller.en-US/API Reference/Regions/DescribeRegions.md#).

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

In the command line, run `python hello_ecs_api.py` to obtain a list of supported regions. The output is similar to the following.

```
[u'cn-shenzhen', u'ap-southeast-1', u'cn-qingdao', u'cn-beijing', u'cn-shanghai', u'us-east-1', u'cn-hongkong', u'me-east-1', u'ap-southeast-2', u'cn-hangzhou', u'eu-central-1', u'ap-northeast-1', u'us-west-1']
```

## Query the list of ECS instances in the current region {#section_anw_knk_kfb .section}

The process for querying the instance list is similar to the region list. You only need to replace the input parameter DescribeRegionsRequest with DescribeInstancesRequest. For a full list of query parameters, see [query an instance list](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#).

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

The output is as follows.

```
current region include instance [u'i-****', u'i-****'']
```

For a full list of APIs, see [ECS API overview](../../../../reseller.en-US/API Reference/API overview.md#). If you want to [query a list of disks](../../../../reseller.en-US/API Reference/Disk/DescribeDisks.md#), replace DescribeInstancesRequest with DescribeDisksRequest.

## Complete code {#section_wvk_4nk_kfb .section}

The following is the complete code of the operations described in this document.

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. DescribeRegionsRequest import DescribeRegionsRequest
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

If you want to learn other API operations in ECS, see [ECS API operation](../../../../reseller.en-US/API Reference/Introduction.md#).

