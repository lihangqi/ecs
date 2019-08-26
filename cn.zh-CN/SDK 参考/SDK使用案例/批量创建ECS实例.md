# 批量创建ECS实例 {#concept_jgc_jkk_kfb .concept}

RunInstances 批量创建实例接口可以帮助您一次创建多台 ECS 按量付费或预付费实例来完成应用的开发和部署，方便实现弹性的资源创建。

和 [CreateInstance](../../../../intl.zh-CN/API 参考/实例/CreateInstance.md#) 接口相比，[RunInstances](../../../../intl.zh-CN/API 参考/实例/RunInstances.md#) 接口有下面的优点：

-   单次可以最多创建 100 台实例，避免重复调用。
-   实例创建之后，实例会自动变成 Starting 状态，然后变成 Running 状态，不需要您调用 StartInstance 的操作。
-   创建实例的时候指定了 InternetMaxBandwidthOut，则自动为您分配公网 IP，不需要您再调用分配 IP 的操作。
-   您也可以一次创建 100 台 [抢占式实例](../../../../intl.zh-CN/产品简介/实例/抢占式实例.md#)，充分满足您的弹性需求。
-   创建的参数保持和 CreateInstance 保持兼容，增加了 Amount 参数来设定创建的个数，以及 AutoReleaseTime 参数来设定自动释放时间，不需要您再额外设置自动释放时间。
-   创建返回一个 InstanceIdSets 会记录相关的 InstanceIds，您只需要根据实例 ID [轮询实例状态](../../../../intl.zh-CN/API 参考/实例/DescribeInstanceStatus.md#)即可。

## 前提条件 {#section_ikf_vkk_kfb .section}

调用 API 前，您需要 [创建 AccessKey](https://www.alibabacloud.com/help/doc-detail/53045.htm)。

**说明：** 禁止使用主账号 AK，因为主账号 AK 泄露会威胁您所有资源的安全。请使用子账号 AK 进行操作，可有效降低 AK 泄露的风险。

## 安装 ECS Python SDK {#section_c53_xkk_kfb .section}

首先确保您已经具备 Python 的 Runtime，本文中使用的 Python 版本为 2.7+。

这里以 Python 为示例，[其他的版本 SDK](https://develop.aliyun.com/tools/sdk?#/python) 大于 4.4.3 即可。

```
pip install aliyun-python-sdk-ecs
```

如果提示您没有权限，请切换sudo继续执行。

```
sudo pip install aliyun-python-sdk-ecs
```

本文使用的 SDK 版本为 4.4.3， 如果您使用是旧版本的 SDK，需要更新。

## 批量创建实例 {#Createinstances .section}

首先创建 RunInstancesRequest 的实例，然后填入相关需要的参数即可。

下面的例子创建了 2 台实例，并且添加了自动每隔 10 秒钟检查一次实例的运行状态。直到实例状态变成Running结束创建流程。

```
# your access key Id
ak_id = "YOU_ACCESS_KEY_ID"
# your access key secret
ak_secret = "YOU_ACCESS_SECRET"
region_id = "cn-beijing"
# your expected instance type
instance_type = "ecs.n4.small"
# 选择的vswitchId
vswitch_id = "vws-xxxxx"
# 使用的镜像信息
image_id = "centos_7_03_64_20G_alibase_20170818.vhd"
# 当前vpc类型的安全组
security_group_id = "sg-xxxxx"
# instance number to launch, support 1-100, default value is 100
amount = 2;
# instance auto delete time 按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为 yyyy-MM-ddTHH:mm:ssZ 。 最短在当前时间之后半小时。最长不能超过当前时间起三年
auto_release_time = "2017-12-05T22:40:00Z"
clt = client.AcsClient(ak_id, ak_secret, 'cn-beijing')
# create instance automatic running
def batch_create_instance():
    request = build_request()
    request.set_Amount(amount)
    _execute_request(request)
def _execute_request(request):
    response = _send_request(request)
    if response.get('Code') is None:
        instance_ids = response.get('InstanceIdSets').get('InstanceIdSet')
        running_amount = 0
        while running_amount < amount:
            time.sleep(10)
            running_amount = check_instance_running(instance_ids)
    print("ecs instance %s is running", instance_ids)
def check_instance_running(instance_ids):
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps(instance_ids))
    response = _send_request(request)
    if response.get('Code') is None:
        instances_list = response.get('Instances').get('Instance')
        running_count = 0
        for instance_detail in instances_list:
            if instance_detail.get('Status') == "Running":
                running_count += 1
        return running_count
def build_request():
    request = RunInstancesRequest()
    request.set_ImageId(image_id)
    request.set_VSwitchId(vswitch_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceName("Instance12-04")
    request.set_InstanceType(instance_type)
    return request
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
```

## 批量创建实例并自动分配公网 IP {#section_lsw_clk_kfb .section}

相比[批量创建实例的代码](#)，只需要添加一行属性，指定公网的带宽即可。下面的例子中默认给实例都分配了 1 M 的按流量带宽。

```
# create instance with public ip.
def batch_create_instance_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)
```

## 批量创建实例并自动设置自动释放时间 {#section_yxk_2lk_kfb .section}

相比[批量创建实例的代码](#)，只需要添加一行属性，指定实例的自动释放时间即可。自动释放时间按照 [ISO8601](../../../../intl.zh-CN/API 参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间，格式为 `yyyy-MM-ddTHH:mm:ssZ`。最短在当前时间之后半小时，最长不能超过当前时间起三年。

```
# create instance with auto release time.
def batch_create_instance_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)
```

## 完整代码示例 {#section_gph_glk_kfb .section}

以上操作完整的代码示例如下所示。

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 4.4.3, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.RunInstancesRequest import RunInstancesRequest
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
# your access key Id
ak_id = "YOU_ACCESS_KEY_ID"
# your access key secret
ak_secret = "YOU_ACCESS_SECRET"
region_id = "cn-beijing"
# your expected instance type
instance_type = "ecs.n4.small"
# 选择的vswitchId
vswitch_id = "vws-xxxxx"
# 使用的镜像信息
image_id = "centos_7_03_64_20G_alibase_20170818.vhd"
# 当前vpc类型的安全组
security_group_id = "sg-xxxxx"
# instance number to launch, support 1-100, default value is 100
amount = 2;
# instance auto delete time 按照 ISO8601 标准表示，并需要使用 UTC 时间。格式为 yyyy-MM-ddTHH:mm:ssZ 。 最短在当前时间之后半小时。最长不能超过当前时间起三年
auto_release_time = "2017-12-05T22:40:00Z"
clt = client.AcsClient(ak_id, ak_secret, 'cn-beijing')
# create instance automatic running
def batch_create_instance():
    request = build_request()
    request.set_Amount(amount)
    _execute_request(request)
# create instance with public ip.
def batch_create_instance_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)
# create instance with auto release time.
def batch_create_instance_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)
def _execute_request(request):
    response = _send_request(request)
    if response.get('Code') is None:
        instance_ids = response.get('InstanceIdSets').get('InstanceIdSet')
        running_amount = 0
        while running_amount < amount:
            time.sleep(10)
            running_amount = check_instance_running(instance_ids)
    print("ecs instance %s is running", instance_ids)
def check_instance_running(instance_ids):
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps(instance_ids))
    response = _send_request(request)
    if response.get('Code') is None:
        instances_list = response.get('Instances').get('Instance')
        running_count = 0
        for instance_detail in instances_list:
            if instance_detail.get('Status') == "Running":
                running_count += 1
        return running_count
def build_request():
    request = RunInstancesRequest()
    request.set_ImageId(image_id)
    request.set_VSwitchId(vswitch_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceName("Instance12-04")
    request.set_InstanceType(instance_type)
    return request
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
    print "hello ecs batch create instance"
    # batch_create_instance()
    # batch_create_instance_with_public_ip()
    # batch_create_instance_with_auto_release_time()
```

