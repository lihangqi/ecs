# Create an instance {#concept_t42_k4d_kfb .concept}

In addition to the ECS Console or Buy Page, you can also use API code to elastically create and manage ECS instances. This topic describes how to create an ECS instance using Python.

When creating an ECS instance, focus on the following APIs:

-   [Create an ECS instance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#)
-   [Query an instance list](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#)
-   [Start an ECS instance](../../../../reseller.en-US/API Reference/Instances/StartInstance.md#)
-   [Allocate a public IP address](../../../../reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#)

## Create a Pay-As-You-Go ECS instance {#section_tpq_cx3_kfb .section}

-   **Required attributes**

    -   SecurityGroupId: Security group ID. A security group is used to implement the configurations of a group of instances based on firewall rules to protect the network access requests of the instances. We recommend that only necessary access rules, rather than all access rules, be enabled when you configure security group access rules. You can create a security group in the ECS console.
    -   InstanceType: Instance type. See the ECS Buy Page. The option “one-core 2GB n1.small” indicates that the input parameter is “ecs.n1.small”.
    -   ImageId: Image ID. See the image list in the [ECS console](https://ecs.console.aliyun.com/?spm=5176.100239.blogcont69142.23.v8HSGG#/image/region/cn-beijing). You can filter public images or custom images.
    For more parameter settings, see [create an ECS instance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#).

-   **Create an ECS instance**

    The following code shows creating an I/O optimized classic-network ECS instance with SSD as system disk and “cloud\_ssd” as disk parameter.

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

    An instance ID is returned after the ECS instance is created successfully. If creation fails, an error code is returned. Since there are many parameters, you can make adjustments by visiting the ECS Buy Page.

    ```
    {"InstanceId":"i-***","RequestId":"006C1303-BAC5-48E5-BCDF-7FD5C2E6395D"}
    ```

-   **ECS lifecycle**

    For more information about the operations in different ECS status, see ECS [ECS instance life cycle](../../../../reseller.en-US/Product Introduction/Instances/ECS instance life cycle.md#).

    Only when an instance is in the **Stopped** status, can the Start operation be performed and only when it is in the **Running** status, can the Stop operation be performed. To query the ECS status, you can filter the instance list by inputting the parameter Instance ID. When you call DescribeInstancesRequest, input a JSON array of strings to query the resource status. When you query the status of a single instance, we recommend that you use DescribeInstances rather than DescribeInstanceAttribute, because the former API returns more attributes and content than the latter.

    The following code is used to check the instance status. The system returns instance details only when the instance status conforms to the input parameters.

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

-   **Start an ECS instance**

    After an ECS instance is created successfully, the default instance status is **Stopped**. To change to the **Running** status, send the Start command.

    ```
    def start_instance(instance_id):
        request = StartInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```

-   **Stop an ECS instance**

    To stop an ECS instance, use the input instance ID.

    ```
    def stop_instance(instance_id):
        request = StopInstanceRequest()
        request.set_InstanceId(instance_id)
        _send_request(request)
    ```

-   **Enable “ECS automatic startup” when creating an ECS instance**

    The ECS Start and Stop operations are asynchronous. You can perform the operation when the script is creating an ECS instance and detecting if it is in an appropriate status.

    After you obtain the ID of a successfully created ECS instance, check whether the instance is in the **Stopped** status. If it is in the **Stopped** status, send the Start ECS command and wait until the ECS status changes to **Running**.

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

-   **Allocate a public IP address**

    If you specify the public network bandwidth when creating an ECS instance, you need to call an API to allocate a public IP address to the instance for public network access. For more information, see [allocate a public IP address.](../../../../reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#).


## Create an ECS instance in the Subscription mode {#section_lw3_wz3_kfb .section}

API also supports creating ECS instances in the Subscription mode, in addition to Pay-As-You-Go ECS instances. The process for creating an ECS instance in the Subscription mode is different from that on Alibaba Cloud’s website. Fees are automatically deducted for an ECS instance created in the Subscription mode. Before you create an ECS instance, make sure that you have sufficient account balance or credit amount, so that the fees can be deducted directly during creation.

When creating an ECS instance in Subscription mode, you only need to specify the payment option and duration. In the following code, the duration is set to one month.

```
request.set_Period(1)    request.set_InstanceChargeType(‘PrePaid’)
```

The complete code for creating an ECS instance in the Subscription mode is as follows:

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

## Complete code {#section_ymz_b1j_kfb .section}

See the complete code as follows. You can use your resource parameters for configuration.

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

