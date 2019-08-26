# 弹性创建ECS实例 {#concept_t42_k4d_kfb .concept}

本文以Python SDK为例，为您演示如何通过CreateInstance等阿里云API弹性地创建和管理ECS实例。

## API列表 {#section_lcb_5rf_chb .section}

本文创建ECS实例时使用的API如下所示：

-   [CreateInstance](../../../../../cn.zh-CN/API参考/实例/CreateInstance.md#)：创建ECS实例
-   [DescribeInstances](../../../../../cn.zh-CN/API参考/实例/DescribeInstances.md#)：查询实例列表
-   [StartInstance](../../../../../cn.zh-CN/API参考/实例/StartInstance.md#)：启动ECS实例
-   [StopInstance](../../../../../cn.zh-CN/API参考/实例/StopInstance.md#)：停止ECS实例
-   [AllocatePublicIpAddress](../../../../../cn.zh-CN/API参考/网络/AllocatePublicIpAddress.md#)：分配公网IP地址

## 创建按量付费ECS实例 {#section_tpq_cx3_kfb .section}

**前提条件**

使用按量付费服务，您的账户账号不得少于100元，您可以在[阿里云费用中心](https://expense.console.aliyun.com/?spm=5176.100239.blogcont69142.17.FdjaVS#/account/home)完成账号充值。

**必选属性**

-   SecurityGroupId：安全组ID。安全组相当于虚拟防火墙，通过安全组规则控制和保护实例的网络出入请求。建议按需开放和设置安全组出入规则时，不要默认开放所有的出入规则。更多详情，请参见[CreateSecurityGroup](../../../../../cn.zh-CN/API参考/安全组/CreateSecurityGroup.md#)。
-   InstanceType：实例规格。例如，选择1核2GiB n1.small则入参为ecs.n1.small。更多详情，请参见[实例规格族汇总](../../../../../cn.zh-CN/实例/实例规格族/实例规格族汇总.md#)。
-   ImageId：镜像ID。您可以使用公共镜像或者自定义镜像。更多详情，请参见[DescribeImages](../../../../../cn.zh-CN/API参考/镜像/DescribeImages.md#)。

**步骤1：创建ECS实例**

如以下代码所示，创建一台VPC类型的ECS实例，使用SSD云盘做系统盘，对应参数值为cloud\_ssd，选择I/O优化实例则传入optimized属性。CreateInstance还提供了其他请求参数，您可以根据[CreateInstance文档](../../../../../cn.zh-CN/API参考/实例/CreateInstance.md#)进行调整。

```
# create one after pay ecs instance.
def create_after_pay_instance(image_id, instance_type, security_group_id):
    request = CreateInstanceRequest();
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId('vsw-vswitchid')
    request.set_VSwitchId('vsw-vswitchid')
    request.set_SystemDiskCategory('cloud_ssd')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id;
```

创建成功返回相应的实例ID和请求ID：

```
{"InstanceId":"i-***","RequestId":"006C1303-BAC5-48E5-BCDF-7FD5C2E6395D"}
```

创建失败返回对应的错误码和错误信息：

```
{ "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx", "HostId": "ecs.aliyuncs.com", "Code": "InvalidSecurityGroupId.NotFound", "Message": "The specified SecurityGroupId does not exist." }

```

**步骤2：查询ECS实例状态**

有关ECS实例的状态信息，请参见[实例生命周期介绍](../../../../../cn.zh-CN/实例/实例生命周期/实例生命周期介绍.md#)。其中：

-   仅Stopped状态的实例可以执行StartInstance操作。
-   仅Running状态的实例可以执行StopInstance操作。

查询ECS实例状态可以通过实例ID（InstanceId）过滤。在DescribeInstances请求中通过传入JSON数组格式的String参数来查询实例状态。以下代码会检查实例的状态，并返回相应的实例信息：

```
# output the instance owned in current region.
def get_instance_detail_by_id(instance_id, status='Stopped'):
    logging.info("Check instance %s status is %s", instance_id, status)
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps([instance_id]))
    response = _send_request(request)
    instance_detail = None
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        for item in instance_list:
            if item.get('Status') == status:
                instance_detail = item
                break;
        return instance_detail;
```

**步骤3：启动ECS实例**

创建成功后的ECS实例默认状态为Stopped。如果需要实例进入Running状态，可以通过StartInstance完成。

```
def start_instance(instance_id):
    request = StartInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)
```

**（可选）步骤4：停止ECS实例**

如果需要运行中的实例进入Stopped状态，可以通过StopInstance完成。

```
def stop_instance(instance_id):
    request = StopInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)
```

**如何创建实例时自动检测并启动ECS实例**

ECS实例的启动和停止都是异步操作，您可以在脚本创建并同时检测ECS实例符合状态时执行相应操作。以下示例代码的逻辑是：

1.  得到实例ID后，自动检测实例是否处于Stopped的状态。
2.  如果是Stopped，发起StartInstance指令。
3.  等待ECS实例进入Running状态。

```
def check_instance_running(instance_id):
    detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING)
    index = 0
    while detail is None and index &lt; 60:
        detail = get_instance_detail_by_id(instance_id=instance_id);
        time.sleep(10)
    if detail and detail.get('Status') == 'Stopped':
        logging.info("instance %s is stopped now.")
        start_instance(instance_id=instance_id)
        logging.info("start instance %s job submit.")
    detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING)
    while detail is None and index &lt; 60:
        detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING);
        time.sleep(10)
    logging.info("instance %s is running now.", instance_id)
    return instance_id;
```

**如何分配公网IP**

如果在创建ECS实例的过程中，指定了公网带宽，若需要公网的访问权限请调用API来分配公网IP。更多详情，请参见[AllocatePublicIpAddress](../../../../../cn.zh-CN/API参考/网络/AllocatePublicIpAddress.md#)。

## 创建包年包月ECS实例 {#section_lw3_wz3_kfb .section}

通过API创建包年包月ECS实例的流程与ECS控制台创建流程不同，API流程使用的是自动扣费的模式。请在创建ECS实例之前确保账号支付方式有足够的余额或者信用额度，在创建ECS实例时实行直接扣费。

与创建按量付费ECS实例相比，您需要指定计费方式和计费时长。以下示例的时长为一个月。

```
request.set_Period(1)
request.set_InstanceChargeType(‘PrePaid’)
```

创建包年包月实例的示例代码如下：

```
# create one prepay ecs instance.
def create_prepay_instance(image_id, instance_type, security_group_id):
    request = CreateInstanceRequest();
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId('vsw-vswitchid')
    request.set_SystemDiskCategory('cloud_ssd')
    request.set_Period(1)
    request.set_InstanceChargeType('PrePaid')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id;
```

## 完整代码 {#section_ymz_b1j_kfb .section}

本文的完整代码如下所示，您可以自行根据实际情况修改和设置参数取值。

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.CreateInstanceRequest import CreateInstanceRequest
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.StartInstanceRequest import StartInstanceRequest
# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
IMAGE_ID = 'ubuntu1404_64_40G_cloudinit_20160727.raw'
INSTANCE_TYPE = 'ecs.s2.large'  # 2c4g generation 1
SECURITY_GROUP_ID = 'sg-****'
INSTANCE_RUNNING = 'Running'
def create_instance_action():
    instance_id = create_after_pay_instance(image_id=IMAGE_ID, instance_type=INSTANCE_TYPE,
                                            security_group_id=SECURITY_GROUP_ID)
    check_instance_running(instance_id=instance_id)
def create_prepay_instance_action():
    instance_id = create_prepay_instance(image_id=IMAGE_ID, instance_type=INSTANCE_TYPE,
                                         security_group_id=SECURITY_GROUP_ID)
    check_instance_running(instance_id=instance_id)
# create one after pay ecs instance.
def create_after_pay_instance(image_id, instance_type, security_group_id):
    request = CreateInstanceRequest();
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId('vsw-vswitchid')
    request.set_SystemDiskCategory('cloud_ssd')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id;
# create one prepay ecs instance.
def create_prepay_instance(image_id, instance_type, security_group_id):
    request = CreateInstanceRequest();
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_VSwitchId('vsw-vswitchid')
    request.set_SystemDiskCategory('cloud_ssd')
    request.set_Period(1)
    request.set_InstanceChargeType('PrePaid')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id;
def check_instance_running(instance_id):
    detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING)
    index = 0
    while detail is None and index &lt; 60:
        detail = get_instance_detail_by_id(instance_id=instance_id);
        time.sleep(10)
    if detail and detail.get('Status') == 'Stopped':
        logging.info("instance %s is stopped now.")
        start_instance(instance_id=instance_id)
        logging.info("start instance %s job submit.")
    detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING)
    while detail is None and index &lt; 60:
        detail = get_instance_detail_by_id(instance_id=instance_id, status=INSTANCE_RUNNING);
        time.sleep(10)
    logging.info("instance %s is running now.", instance_id)
    return instance_id;
def start_instance(instance_id):
    request = StartInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)
# output the instance owned in current region.
def get_instance_detail_by_id(instance_id, status='Stopped'):
    logging.info("Check instance %s status is %s", instance_id, status)
    request = DescribeInstancesRequest()
    request.set_InstanceIds(json.dumps([instance_id]))
    response = _send_request(request)
    instance_detail = None
    if response is not None:
        instance_list = response.get('Instances').get('Instance')
        for item in instance_list:
            if item.get('Status') == status:
                instance_detail = item
                break;
        return instance_detail;
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
    logging.info("Create ECS by OpenApi!")
    create_instance_action()
    # create_prepay_instance_action()
```

