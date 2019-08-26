# 弹性创建ECS实例 {#concept_t42_k4d_kfb .concept}

除了可以在 ECS 控制台或售卖页创建 ECS 实例外，您还可以使用 API 代码来弹性地创建和管理ECS实例。本页面使用 Python 为例进行说明。

创建 ECS 时需关注以下 API：

-   [创建ECS实例](../../../../intl.zh-CN/API 参考/实例/CreateInstance.md#)
-   [查询实例列表](../../../../intl.zh-CN/API 参考/实例/DescribeInstances.md#)
-   [启动ECS实例](../../../../intl.zh-CN/API 参考/实例/StartInstance.md#)
-   [分配公网IP地址](../../../../intl.zh-CN/API 参考/网络/AllocatePublicIpAddress.md#)

## 创建按量云服务器 {#section_tpq_cx3_kfb .section}

-   **创建ECS实例时的必选属性**

    -   SecurityGroupId：安全组 ID。安全组通过防火墙规则实现对一组实例的配置，保护实例的网络出入请求。在设置安全组出入规则时，建议按需开放而不要默认开放所有的出入规则。您也可以通过 ECS 控制台创建安全组。
    -   InstanceType：实例规格。参考 ECS [售卖页](https://ecs-buy.aliyun.com/?spm=5176.100239.blogcont69142.22.kjorRF#/postpay)的选项，界面上 1 核 2GB n1.small则入参为 ecs.n1.small。
    -   ImageId：镜像 ID。参考[ECS控制台](https://ecs.console.aliyun.com/?spm=5176.100239.blogcont69142.23.v8HSGG#/image/region/cn-beijing)的镜像列表，您可以过滤系统公共镜像或者自定义镜像。
    更多参数设置请参考[创建ECS实例](../../../../intl.zh-CN/API 参考/实例/CreateInstance.md#)。

-   **创建云服务器**

    如下面的代码所示，创建一台经典网络的ECS，使用系统盘ssd，盘参数为cloud\_ssd，选择io优化实例optimized。

    ```
    # create one after pay ecs instance.
    def create_after_pay_instance(image_id, instance_type, security_group_id):
        request = CreateInstanceRequest();
        request.set_ImageId(image_id)
        request.set_SecurityGroupId(security_group_id)
        request.set_InstanceType(instance_type)
        request.set_IoOptimized('optimized')
        request.set_SystemDiskCategory('cloud_ssd')
        response = _send_request(request)
        instance_id = response.get('InstanceId')
        logging.info("instance %s created task submit successfully.", instance_id)
        return instance_id;
    ```

    创建成功后将返回相应的实例 ID，失败的话也会有对应的 ErrorCode。由于参数较多，您可以参考 ECS 的[售卖页](https://ecs-buy.aliyun.com/?spm=5176.100239.blogcont69142.22.kjorRF#/postpay)进行调整。

    ```
    {"InstanceId":"i-***","RequestId":"006C1303-BAC5-48E5-BCDF-7FD5C2E6395D"}
    ```

-   **云服务器生命周期**

    对于云服务器的状态操作, 请参考云服务器[实例生命周期](../../../../intl.zh-CN/产品简介/实例/实例生命周期.md#)。

    只有Stopped状态的实例可以执行 Start 操作。也只有Running状态的 ECS 可以执行Stop操作。查询云服务器的状态可以通过查询实例列表传入 InstanceId 进行过滤。在DescribeInstancesRequest时可以通过传入一个 JSON 数组格式的 String 就可以查询这个资源的状态。查询单个实例的状态建议使用DescribeInstances而不要使用DescribeInstanceAttribute，因为前者比后者返回更多的属性和内容。

    下面的代码会检查实例的状态，只有实例的状态符合入参才会返回实例的详情。

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

-   **启动云服务器**

    创建成功后的 ECS 默认状态是Stopped。如果要启动 ECS 实例为Running状态，只需要发送启动指令即可。

    ```
    def start_instance(instance_id):
        request = StartInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```

-   **停止云服务器**

    停止云服务器只需传入instanceId即可。

    ```
    def stop_instance(instance_id):
        request = StopInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```

-   **创建时启动“自动启动云服务器”**

    服务器的启动和停止都是一个异步操作，您可以在脚本创建并同时检测云服务器符合状态时执行相应操作。

    创建资源后得到实例ID，首先判断实例是否处于Stopped的状态，如果处于Stopped状态，下发Start服务器的指令，然后等待服务器的状态变成Running。

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

-   **分配公网IP**

    如果在创建云服务器的过程中，指定了公网带宽，若需要公网的访问权限还要调用API来分配公网IP。详情请参考[分配公网IP地址](../../../../intl.zh-CN/API 参考/网络/AllocatePublicIpAddress.md#)。


## 创建包年包月云服务器 {#section_lw3_wz3_kfb .section}

除了创建按量服务的云服务器，您的API还支持创建包年包月的服务器。包年包月的创建和官网的创建流程不同，使用的是自动扣费的模式，也就是说您需要在创建服务器之前确保账号有足够的余额或者信用额度，在创建的时候将直接扣费。

和按量付费的 ECS 相比，只需要指定付费类型和时长即可，下面的时长为1个月。

```
request.set_Period(1)    request.set_InstanceChargeType(‘PrePaid’)
```

创建包年包月实例的整体的代码如下：

```
# create one prepay ecs instance.
def create_prepay_instance(image_id, instance_type, security_group_id):
    request = CreateInstanceRequest();
    request.set_ImageId(image_id)
    request.set_SecurityGroupId(security_group_id)
    request.set_InstanceType(instance_type)
    request.set_IoOptimized('optimized')
    request.set_SystemDiskCategory('cloud_ssd')
    request.set_Period(1)
    request.set_InstanceChargeType('PrePaid')
    response = _send_request(request)
    instance_id = response.get('InstanceId')
    logging.info("instance %s created task submit successfully.", instance_id)
    return instance_id;
```

## 完整的代码 {#section_ymz_b1j_kfb .section}

完整的代码如下，您可以按照自己的资源参数进行设置。

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

