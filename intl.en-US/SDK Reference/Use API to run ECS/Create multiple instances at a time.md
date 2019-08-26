# Create multiple instances at a time {#concept_jgc_jkk_kfb .concept}

RunInstances can create multiple ECS instances at a time. It helps you fast develop and deploy application.

Compared with [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#), [RunInstances](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) has the following benefits:

-   RunInstances contains Amount to create and automatically run up to 100 instances or preemptible instances for one request.
-   When an instance is created, the instance status automatically becomes **Starting** and then **Running**. You do not need to call the StartInstance operation.
-   Instances have Internet IPs allocated if you set the value of InternetMaxBandwidthOut greater than 0.
-   You can also create 100 [preemptable instances](../../../../reseller.en-US/Product Introduction/Instances/Preemptible instance.md#) at a time to fully meet your requirements.
-   Release plan can be scheduled by setting AutoReleaseTime, and the number of created parameters can be set by configuring Amount. The error codes and available parameters of RunInstances are completely compatible with CreateInstance.
-   [Status polling of the created instances](../../../../reseller.en-US/API Reference/Instances/DescribeInstanceStatus.md#) is allowed since InstanceIdSets lists all the InstanceIds after the request.

## Prerequisites {#section_ikf_vkk_kfb .section}

Make sure you have created an [AccessKey](https://partners-intl.aliyun.com/help/doc-detail/53045.htm).

**Note:** Do not use the AccessKey of the primary account. If it is disclosed, your resources may be unsafe. Use the AccessKey of an RAM user account to reduce the risk of AccessKey disclosure.

## Install ECS Python SDK {#section_c53_xkk_kfb .section}

Make sure that you have runtime for Python. In this document, we take a version later than Python 2.7

as an example and the [SDK version](https://develop.aliyun.com/tools/sdk?#/python) is 4.4.3.

```
pip install aliyun-python-sdk-ecs
```

If you get any message indicating that you have no operation permission, switch to sudo.

```
sudo pip install aliyun-python-sdk-ecs
```

The version of the SDK used in this article is 4.4.3. If you are using an older version of the SDK, update it.

## Create instances {#Createinstances .section}

Create RunInstancesRequest object and then enter the related parameters:

In this example, we create two instances and specify to automatically check the instance status every 10 seconds. The creation procedure ends when the instance status turns into **Running**.

```
# your access key Id
ak_id = "YOU_ACCESS_KEY_ID"
# your access key secret
ak_secret = "YOU_ACCESS_SECRET"
region_id = "cn-beijing"
# your expected instance type
instance_type = "ecs.n4.small"
# The selected vswitchId
vswitch_id = "vws-xxxxx"
# The selected image info
image_id = "centos_7_03_64_20G_alibase_20170818.vhd"
# The selected security group of VPC network
security_group_id = "sg-xxxxx"
# instance number to launch, support 1-100, default value is 100
amount = 2;
# The auto release time is in accordance with ISO8601 and must be UTC. The format is `yyyy-MM-ddTHH:mm:ssZ`. The release time must be at least 30 minutes later than the current time and less than 3 years from the current time.
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

## Create instances with Internet IP {#section_lsw_clk_kfb .section}

[Create instances](#) and add a line of attribute to specify Internet bandwidth. In this example, we assign 1 Mbit/s bandwidth for each instance.

```
# create instance with public ip.
def batch_create_instance_with_public_ip():
    request = build_request()
    request.set_Amount(amount)
    request.set_InternetMaxBandwidthOut(1)
    _execute_request(request)
```

## Create instances with auto release time {#section_yxk_2lk_kfb .section}

[Create instances](#) and add a line of attribute to specify auto release time for instances. The auto release time is in accordance with [ISO8601](../../../../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) and must be UTC. The format is `YYYY-MM-DDTHH:mm:ssZ`. The release time cannot be 30 minutes earlier than the current time or more than 3 years from the current time.

```
# create instance with auto release time.
def batch_create_instance_with_auto_release_time():
    request = build_request()
    request.set_Amount(amount)
    request.set_AutoReleaseTime(auto_release_time)
    _execute_request(request)
```

## Complete example code {#section_gph_glk_kfb .section}

The complete example code is as follows.

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 4.4.3, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. RunInstancesRequest import RunInstancesRequest
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
# The selected vswitchId.
vswitch_id = "vws-xxxxx"
# The selected image info
image_id = "centos_7_03_64_20G_alibase_20170818.vhd"
# The selected security group of VPC network
security_group_id = "sg-xxxxx"
# instance number to launch, support 1-100, default value is 100
amount = 2;
# The auto release time is in accordance with ISO8601 and must be UTC. The format is `YYYY-MM-DDTHH:mm:ssZ`. The release time must be at least 30 minutes later than the current time and less than 3 years from the current time.
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

