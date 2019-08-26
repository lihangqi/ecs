# Release an instance {#concept_smk_npk_kfb .concept}

One important feature of ECS is on-demand resource creation. You can create custom resources elastically on demand during peak service hours, and then release those resources after service computing is completed. This document describes how to easily release ECS instances and achieve elasticity.

This topic covers the following APIs:

-   [DeleteInstance](../../../../reseller.en-US/API Reference/Instances/DeleteInstance.md#)
-   [ModifyInstanceAutoReleaseTime](../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAutoReleaseTime.md#)
-   [StopInstance](../../../../reseller.en-US/API Reference/Instances/StopInstance.md#)
-   [Instance list query API](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#)

After an ECS instance is released, the physical resources used by the instance are recycled, including disks and snapshots. The data of the instance is completely lost and can never be recovered. If you want to retain the data, we recommend that you create snapshots of disks before releasing the ECS instance. The snapshots can be directly used to create a new ECS instance.

To release an ECS instance, you must stop it first. If any application is affected after the ECS instance is stopped, restart the instance.

## Stop an ECS instance {#section_axd_nqk_kfb .section}

Use the StopInstance interface to stop an ECS instance, regardless of the billing method of the instance. The stop command is as follows. When the ForceStop parameter is set to true, the ECS instance is stopped directly but data is not necessarily written to a disk, similar to power failure. Therefore, if you want to release an instance, set ForceStop to true.

```
def stop_instance(instance_id, force_stop=False):
    '''
    stop one ecs instance.
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param force_stop: if force stop is true, it will force stop the server and not ensure the data
    write to disk correctly.
    :return:
    '''
    request = StopInstanceRequest()
    request.set_InstanceId(instance_id)
    request.set_ForceStop(force_stop)
    logging.info("Stop %s command submit successfully.", instance_id)
    _send_request(request)
```

## Release an ECS instance {#section_v1w_pqk_kfb .section}

If you release an ECS instance when it is not in the Stopped status, an error occurs:

```
{"RequestId":"3C6DEAB4-7207-411F-9A31-6ADE54C268BE","HostId":"ecs-cn-hangzhou.aliyuncs.com","Code":"IncorrectInstanceStatus","Message":"The current status of the resource does not support this operation."}
```

When the ECS instance is in the **Stopped** status, you can release it. The API has only two request parameters:

-   InstanceId: Instance ID
-   Force: If this parameter is set to “true”, the ECS instance is released forcibly even when it is not in the **Stopped** status. Use caution when setting this parameter. Release by mistake may affect your services.

The request to release an ECS instance is as follows.

```
def release_instance(instance_id, force=False):
    '''
    delete instance according instance id, only support after pay instance.
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param force:
    if force is false, you need to make the ecs instance stopped, you can
    execute the delete action.
    If force is true, you can delete the instance even the instance is running.
    :return:
    '''
    request = DeleteInstanceRequest();
    request.set_InstanceId(instance_id)
    request.set_Force(force)
    _send_request(request)
```

The following response is returned when an ECS instance is released successfully:

```
{"RequestId":"689E5813-D150-4664-AF6F-2A27BB4986A3"}
```

## Set the automatic release time for an ECS instance {#section_wpt_tqk_kfb .section}

You can set the automatic release time for an ECS instance to simplify instance management. When the set time is reached, Alibaba Cloud releases your ECS instance automatically. Use the ModifyInstanceAutoReleaseTime to set the automatic release time for an ECS instance.

**Note:** The automatic release time follows the ISO8601 standard in UTC time. The format is yyyy-MM-ddTHH:mm:ssZ. If the seconds place is not 00, it is automatically set to start from the current minute. The automatic release time must be at least half an hour later than the current time, and must not be more than 3 years since the current time.

```
def set_instance_auto_release_time(instance_id, time_to_release = None):
    '''
    setting instance auto delete time
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param time_to_release: if the property is setting, such as '2017-01-30T00:00:00Z'
    it means setting the instance to be release at that time.
    if the property is None, it means cancel the auto delete time.
    :return:
    '''
    request = ModifyInstanceAutoReleaseTimeRequest()
    request.set_InstanceId(instance_id)
    if time_to_release is not None:
        request.set_AutoReleaseTime(time_to_release)
    _send_request(request)
```

Run the command `set_instance_auto_release_time('i-1111', '2017-01-30T00:00:00Z')` to set the time.

Then you can use the DescribeInstances to query the automatic release time.

```
def describe_instance_detail(instance_id):
    '''
    describe instance detail
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :return:
    '''
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps([instance_id]))
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        if len(instance_list) > 0:
            return instance_list[0]
def check_auto_release_time_ready(instance_id):
    detail = describe_instance_detail(instance_id=instance_id)
    if detail is not None:
        release_time = detail.get('AutoReleaseTime')
        return release_time
```

## Cancel the automatic release {#section_c52_yqk_kfb .section}

If you want to cancel the automatic release due to service changes, run the following command to set the automatic release time to null.

```
set_instance_auto_release_time('i-1111')
```

## Complete example code {#section_odm_zqk_kfb .section}

**Note:** Proceed with caution when releasing ECS instances.

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. DeleteInstanceRequest import DeleteInstanceRequest
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. ModifyInstanceAutoReleaseTimeRequest import \
    ModifyInstanceAutoReleaseTimeRequest
from aliyunsdkecs.request.v20140526. StopInstanceRequest import StopInstanceRequest
# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
def stop_instance(instance_id, force_stop=False):
    '''
    stop one ecs instance.
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param force_stop: if force stop is true, it will force stop the server and not ensure the data
    write to disk correctly.
    :return:
    '''
    request = StopInstanceRequest()
    request.set_InstanceId(instance_id)
    request.set_ForceStop(force_stop)
    logging.info("Stop %s command submit successfully.", instance_id)
    _send_request(request)
def describe_instance_detail(instance_id):
    '''
    describe instance detail
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :return:
    '''
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps([instance_id]))
    response = _send_request(request)
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        if len(instance_list) &gt; 0:
            return instance_list[0]
def check_auto_release_time_ready(instance_id):
    detail = describe_instance_detail(instance_id=instance_id)
    if detail is not None:
        release_time = detail.get('AutoReleaseTime')
        return release_time
def release_instance(instance_id, force=False):
    '''
    delete instance according instance id, only support after pay instance.
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param force:
    if force is false, you need to make the ecs instance stopped, you can
    execute the delete action.
    If force is true, you can delete the instance even the instance is running.
    :return:
    '''
    request = DeleteInstanceRequest();
    request.set_InstanceId(instance_id)
    request.set_Force(force)
    _send_request(request)
def set_instance_auto_release_time(instance_id, time_to_release = None):
    '''
    setting instance auto delete time
    :param instance_id: instance id of the ecs instance, like 'i-***'.
    :param time_to_release: if the property is setting, such as '2017-01-30T00:00:00Z'
    it means setting the instance to be release at that time.
    if the property is None, it means cancel the auto delete time.
    :return:
    '''
    request = ModifyInstanceAutoReleaseTimeRequest()
    request.set_InstanceId(instance_id)
    if time_to_release is not None:
        request.set_AutoReleaseTime(time_to_release)
    _send_request(request)
    release_time = check_auto_release_time_ready(instance_id)
    logging.info("Check instance %s auto release time setting is %s. ", instance_id, release_time)
def _send_request(request):
    '''
    send open api request
    :param request:
    :return:
    '''
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)
if __name__ == '__main__':
    logging.info("Release ecs instance by Aliyun OpenApi!")
    set_instance_auto_release_time('i-1111', '2017-01-28T06:00:00Z')
    # set_instance_auto_release_time('i-1111')
    # stop_instance('i-1111')
    # release_instance('i-1111')
    # release_instance('i-1111', True)
```

If you want to learn other API operations in ECS, see [ECS API operation](../../../../reseller.en-US/API Reference/Introduction.md#).

