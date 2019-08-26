# Create an ECS instance {#concept_t42_k4d_kfb .concept}

This topic describes how to create and manage an Alibaba Cloud ECS instance \(either a Pay-As-You-Go or Subscription instance\) by using Alibaba Cloud APIs.

The APIs described in this topic allow you to:

-   [Create an ECS instance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#)
-   [Query the status of an ECS instance](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#)
-   [Start an ECS instance](../../../../reseller.en-US/API Reference/Instances/StartInstance.md#)
-   [Stop an ECS instance](../../../../reseller.en-US/API Reference/Instances/StopInstance.md#)
-   [Allocate a public IP address](../../../../reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#)

## Create a Pay-As-You-Go ECS instance {#section_tpq_cx3_kfb .section}

**Required parameters**

-   SecurityGroupId: Security group ID. A security group is similar to a firewall and uses security group rules to control network access requests of instances. We recommend that you configure access rules only according to the actual needs. For more information, see [CreateSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/CreateSecurityGroup.md#).
-   InstanceType: Instance type. The option “one-core 2GiB n1.small” indicates that the input parameter is ecs.n1.small. For more information, see [Instance type families](../../../../reseller.en-US/Instances/Instance type families.md#).
-   ImageId: Image ID. You can use public images or custom images. For more information, see [DescribeImages](../../../../reseller.en-US/API Reference/Images/DescribeImages.md#).

 **Step 1: Create an ECS instance** 

The following code example shows the parameters optimized and cloud\_ssd, which indicate the creation of an I/O optimized VPC instance with SSD as the system disk. For more information about other supported request parameters, see [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#).

```
# create one postpaid ecs instance.
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

After an ECS instance is created, the corresponding instance ID and request ID are returned as follows:

```
{"InstanceId":"i-***","RequestId":"006C1303-BAC5-48E5-BCDF-7FD5C2E6395D"}
```

If the creation of an ECS instance fails, a corresponding error code and error message are returned as follows:

```
{ "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx", "HostId": "ecs.aliyuncs.com", "Code": "InvalidSecurityGroupId.NotFound", "Message": "The specified SecurityGroupId does not exist." }
					
```

**Step 2: Query ECS instance status**

Before you query the status of an ECS instance, note the following:

-   The StartInstance operation can be performed on Stopped instances only.
-   The StopInstance operation can be performed on Running instances only.

**Note:** For more information about different ECS status, see [ECS instance lifecycle](../../../../reseller.en-US/Instances/ECS instance life cycle.md#).

To query the status of a specific ECS instance, you can specify its InstanceId. Specifically, when using DescribeInstances, you can pass the parameters in the form of a JSON array to query the instance status. The following code queries instance details:

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

 **Step 3: Start an ECS instance** 

After an ECS instance is created, the default instance status is **Stopped**. To change the instance to the **Running** status, call StartInstance:

```
def start_instance(instance_id):
    request = StartInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)
```

 **\(Optional\) Step 4: Stop an ECS instance** 

To stop an ECS instance, call StopInstance:

```
def stop_instance(instance_id):
    request = StopInstanceRequest()
    request.set_InstanceId(instance_id)
    _send_request(request)
```

 **Enable “ECS automatic startup” when creating an ECS instance** 

The ECS start and stop operations are asynchronous. You can use scripts to create an ECS instance, check its status, and perform the required operations. Specifically, the following code:

1.  Checks whether the specified instance is in the **Stopped** status after obtaining an instance ID.
2.  Calls StartInstance if it is in the **Stopped** status.
3.  Waits for the instance to change to the **Running** status.

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

 **Allocate a public IP address** 

If you specify the Internet bandwidth when you create an ECS instance, you need to call an API to allocate a public IP address to the instance for Internet access. For more information, see [AllocatePublicIpAddress](../../../../reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#).

## Create a Subscription ECS instance {#section_lw3_wz3_kfb .section}

Alibaba Cloud APIs also support the creation of Subscription ECS instances. If you want to create a Subscription ECS instance, make sure that you have a sufficient account balance or credit amount associated to your account so that the fees can be deducted directly during instance creation.

When you create a Subscription ECS instance, you only need to specify the payment option and duration. In the following code example, the billing duration of the instance is set to one month.

```
request.set_Period(1) 
request.set_InstanceChargeType(‘PrePaid’)
```

The complete code for the creation of a Subscription ECS instance is as follows:

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

## Example {#section_ymz_b1j_kfb .section}

The following example uses Python to describe the creation of an ECS instance.

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import time
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. CreateInstanceRequest import CreateInstanceRequest
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. StartInstanceRequest import StartInstanceRequest
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

