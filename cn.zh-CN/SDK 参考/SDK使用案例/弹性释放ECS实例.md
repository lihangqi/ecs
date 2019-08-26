# 弹性释放ECS实例 {#concept_smk_npk_kfb .concept}

云服务器 ECS 的一个重要特性就是按需创建资源。您可以在业务高峰期按需弹性地进行自定义资源创建，完成业务计算时释放资源。本篇将提供若干 Tips 帮助您更加便捷地完成云服务器的释放以及弹性设置。

本文将涉及到几个重要功能和相关API：

-   [释放按量付费的云服务器](../../../../intl.zh-CN/API 参考/实例/DeleteInstance.md#)
-   [设置按量付费实例的自动释放时间](../../../../intl.zh-CN/API 参考/实例/ModifyInstanceAutoReleaseTime.md#)
-   [停止服务器](../../../../intl.zh-CN/API 参考/实例/StopInstance.md#)
-   [查询实例列表](../../../../intl.zh-CN/API 参考/实例/DescribeInstances.md#)

释放后，实例所使用的物理资源将被回收，包括磁盘及快照，相关数据将全部丢失且永久不可恢复。如果您还想继续使用相关的数据，建议您释放云服务器之前一定要对磁盘数据做快照，下次创建 ECS 时可以直接通过快照创建资源。

## 释放云服务器 {#section_asf_mqk_kfb .section}

释放服务器，首先要求您的服务器处于停止状态。当服务器停止后，若影响到应用，您可以将服务器重新启动。

## 停止云服务器 {#section_axd_nqk_kfb .section}

停止服务器的指令非常简单，且对于按量付费和包年包月都是一样的。停止云服务器的一个参数是 ForceStop，若属性设置为 true，它将类似于断电，直接停止服务器，但不承诺数据能写到磁盘中。如果仅仅为了释放服务器，这个可以设置为 true。

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

## 释放云服务器 {#section_v1w_pqk_kfb .section}

如果您没有停止服务器直接执行释放，可能会有如下报错：

```
{"RequestId":"3C6DEAB4-7207-411F-9A31-6ADE54C268BE","HostId":"ecs-cn-hangzhou.aliyuncs.com","Code":"IncorrectInstanceStatus","Message":"The current status of the resource does not support this operation."}
```

当服务器处于Stopped状态时，您可以执行释放服务器。释放服务器的方法比较简单，参数如下：

-   InstanceId: 实例的 ID。
-   force: 如果将这个参数设置为 true，将会执行强制释放。即使云服务器不是Stopped状态也可以释放。执行的时候请务必小心，以防错误释放影响您的业务。

释放云服务器的Request如下：

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

释放云服务器成功的 Response 如下：

```
{"RequestId":"689E5813-D150-4664-AF6F-2A27BB4986A3"}
```

## 设置云服务器的自动释放时间 {#section_wpt_tqk_kfb .section}

为了更加简化对云服务器的管理，您可以自定义云服务器的释放时间。当定时时间到后，阿里云将自动为您完成服务器的释放, 无需手动执行释放。

**说明：** 自动释放时间按照 ISO8601 标准表示，并需要使用 UTC 时间。 格式为：yyyy-MM-ddTHH:mm:ssZ。 如果秒不是 00，则自动取为当前分钟开始时。自动释放的时间范围：当前时间后 30 分钟 ~ 当前时间起 3 年。

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

执行 `set_instance_auto_release_time(‘i-1111’, ‘2017-01-30T00:00:00Z’)` 后完成设置。

执行设置成功后，您可以通过DescribeInstances来查询自动释放的时间设置。

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

## 取消自动释放设置 {#section_c52_yqk_kfb .section}

如果您的业务有变化，需要取消自动释放设置。只需执行命令将自动释放时间设置为空即可。

```
set_instance_auto_release_time('i-1111')
```

## 完整代码 {#section_odm_zqk_kfb .section}

**说明：** 释放云服务器需谨慎。

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DeleteInstanceRequest import DeleteInstanceRequest
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.ModifyInstanceAutoReleaseTimeRequest import \
    ModifyInstanceAutoReleaseTimeRequest
from aliyunsdkecs.request.v20140526.StopInstanceRequest import StopInstanceRequest
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

如您想了解 ECS 中 API 的其它操作，请参考 [ECS中的API操作](../../../../intl.zh-CN/API 参考/简介.md#)。

