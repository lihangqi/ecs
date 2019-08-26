# Renew an instance {#concept_qhn_2sk_kfb .concept}

Lifecycle is important to ECS instances of the Subscription billing method. In addition to the ECS console or the ECS purchase page, Alibaba Cloud provides you with APIs to view the resource expiration time and renew your instance.

This topic involves the following key functions:

-   Query ECS instances by expiration time.
-   Renew instances.
-   Query the automatic renewal time of an ECS instance.
-   Set the automatic renewal time of an ECS instance.

Lifecycle is important to ECS instances in the Subscription mode. If you fail to renew your ECS instance on time, the instance may be locked or even released, thus affecting your service continuity. You can use APIs to view the resource expiration time and renew your instance.

This article covers the following APIs:

-   [DescribeInstances](../../../../intl.en-US/API Reference/Instances/DescribeInstances.md#)
-   [ModifyInstanceAutoRenewAttribute](../../../../intl.en-US/API Reference/Instances/RenewInstance.md#)

## Query the instances that will expire within the specified time range {#section_mby_lsk_kfb .section}

Use the DescribeInstances interface to query the instances that will expire within the specified time range by setting the filter parameters ExpiredStartTime and ExpiredEndTime. The time parameters follow the ISO8601 standard in UTC time, using the format yyyy-MM-ddTHH:mmZ. The system returns a list of instances that will expire within the specified time range. If you want to filter by security group, add the security group ID.

```
INSTANCE_EXPIRED_START_TIME_IN_UTC_STRING = '2017-01-22T00:00Z'
INSTANCE_EXPIRE_END_TIME_IN_UTC_STRING = '2017-01-28T00:00Z'
def describe_need_renew_instance(page_size=100, page_number=1, instance_id=None,
                                 check_need_renew=True, security_group_id=None):
    request = DescribeInstancesRequest()
    if check_need_renew is True:
        request.set_Filter3Key("ExpiredStartTime")
        request.set_Filter3Value(INSTANCE_EXPIRED_START_TIME_IN_UTC_STRING)
        request.set_Filter4Key("ExpiredEndTime")
        request.set_Filter4Value(INSTANCE_EXPIRE_END_TIME_IN_UTC_STRING)
    if instance_id is not None:
        request.set_InstanceIds(json.dumps([instance_id]))
    if security_group_id:
        request.set_SecurityGroupId(security_group_id)
    request.set_PageNumber(page_number)
    request.set_PageSize(page_size)
    return _send_request(request)
```

## Renew ECS instances {#section_ycv_nsk_kfb .section}

Only ECS instances in the Subscription mode can be renewed. Pay-As-You-Go instances cannot be renewed. Renewals must be paid by account balance or credit. Fee deduction and order creation are in sync with API execution. Make sure that there is sufficient balance in your account.

```
def _renew_instance_action(instance_id, period='1'):
    request = RenewInstanceRequest()
    request.set_Period(period)
    request.set_InstanceId(instance_id)
    response = _send_request(request)
    logging.info('renew %s ready, output is %s ', instance_id, response)
```

Fees are automatically deducted when the instance is renewed. After the renewal is completed, you can query the resource expiration time of the instance based on InstanceId. Because the API is executed asynchronously, the expiration time is updated in 10 seconds.

## Enable automatic ECS instance renewal {#section_fyq_psk_kfb .section}

Alibaba Cloud provides the [automatic renewal function](../../../../intl.en-US/Pricing/Renew instances/Auto-renewal.md#) for ECS instances in the Subscription mode to help you reduce the cost of expired resource maintenance. Fee deduction for automatic renewal starts at 08:00:00 nine days before the expiration date. If fee deduction fails on the first day, the deduction process repeats on the following days in sequence until fees are deducted successfully or resources are locked after the nine-day period. Make sure that you have sufficient balance or credit amount in your account.

-   **Query automatic renewal setting**

    You can use OpenAPI to query and set automatic renewal. The API supports only ECS instances in the Subscription mode. If you use the API on a Pay-As-You-Go instance, an error is returned. You can query the automatic renewal status of up to 100 ECS instances of the Subscription billing method at a time. Use commas to separate multiple instance IDs.

    The input parameter of DescribeInstanceAutoRenewAttribut is the instance ID.

    InstanceId: You can query up to 100 ECS instances in the Subscription mode at a time. Use commas to separate multiple instance IDs.

    ```
    # check the instances is renew or not
    def describe_auto_renew(instance_ids, expected_auto_renew=True):
        describe_request = DescribeInstanceAutoRenewAttributeRequest()
        describe_request.set_InstanceId(instance_ids)
        response_detail = _send_request(request=describe_request)
        failed_instance_ids = ''
        if response_detail is not None:
            attributes = response_detail.get('InstanceRenewAttributes').get('InstanceRenewAttribute')
            if attributes:
                for item in attributes:
                    auto_renew_status = item.get('AutoRenewEnabled')
                    if auto_renew_status ! = expected_auto_renew:
                        failed_instance_ids += item.get('InstanceId') + ','
    
    describe_auto_renew('i-1111,i-2222')
    ```

    The following content is returned:

    ```
    {"InstanceRenewAttributes":{"InstanceRenewAttribute":[{"Duration":0,"InstanceId":"i-1111","AutoRenewEnabled":false},{"Duration":0,"InstanceId":"i-2222","AutoRenewEnabled":false}]},"RequestId":"71FBB7A5-C793-4A0D-B17E-D6B426EA746A"}
    ```

    If automatic renewal is set, the returned attribute AutoRenewEnabled is true. If automatic renewal is not set, the attribute is false.

-   **Enable and cancel automatic renewal for ECS instances**

    To enable automatic renwal for ECS instances, three input parameters are required:

    -   InstanceId: You can set automatic renewal for up to 100 ECS instances of the Subscription billing method at a time. Use commas to separate multiple instance IDs.
    -   Duration: Set to 1, 2, 3, 6, or 12, in unit of Month.
    -   AutoRenew: Set to true to enable automatic renewal. Set to false to disable automatic renewal.
    ```
    def setting_instance_auto_renew(instance_ids, auto_renew = True):
        logging.info('execute enable auto renew ' + instance_ids)
        request = ModifyInstanceAutoRenewAttributeRequest();
        request.set_Duration(1);
        request.set_AutoRenew(auto_renew);
        request.set_InstanceId(instance_ids)
        _send_request(request)
    ```

    When the operation is successful, the following response is returned:

    ```
    {"RequestId":"7DAC9984-AAB4-43EF-8FC7-7D74C57BE46D"}
    ```

    You can perform a query after successful renewal. The system returns the renewal duration and the status of automatic renewal \(true/false\).

    ```
    {"InstanceRenewAttributes":{"InstanceRenewAttribute":[{"Duration":1,"InstanceId":"i-1111","AutoRenewEnabled":true},{"Duration":1,"InstanceId":"i-2222","AutoRenewEnabled":true}]},"RequestId":"7F4D14B0-D0D2-48C7-B310-B1DF713D4331"}
    ```


## Complete example code {#section_nv5_xsk_kfb .section}

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526. DescribeInstanceAutoRenewAttributeRequest import \
    DescribeInstanceAutoRenewAttributeRequest
from aliyunsdkecs.request.v20140526. DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526. ModifyInstanceAutoRenewAttributeRequest import \
    ModifyInstanceAutoRenewAttributeRequest
from aliyunsdkecs.request.v20140526. RenewInstanceRequest import RenewInstanceRequest
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S')
clt = client.AcsClient('Your Access Key Id', 'Your Access Key Secrect', 'cn-beijing')
# data format in UTC, only support passed the value for minute, seconds is not support.
INSTANCE_EXPIRED_START_TIME_IN_UTC_STRING = '2017-01-22T00:00Z'
INSTANCE_EXPIRE_END_TIME_IN_UTC_STRING = '2017-01-28T00:00Z'
def renew_job(page_size=100, page_number=1, check_need_renew=True, security_group_id=None):
    response = describe_need_renew_instance(page_size=page_size, page_number=page_number,
                                            check_need_renew=check_need_renew,
                                            security_group_id=security_group_id)
    response_list = response.get('Instances').get('Instance')
    logging.info("%s instances need to renew", str(response.get('TotalCount')))
    if response_list > 0:
        instance_ids = ''
        for item in response_list:
            instance_id = item.get('InstanceId')
            instance_ids += instance_id + ','
            renew_instance(instance_id=instance_id)
        logging.info("%s execute renew action ready", instance_ids)
def describe_need_renew_instance(page_size=100, page_number=1, instance_id=None,
                                 check_need_renew=True, security_group_id=None):
    request = DescribeInstancesRequest()
    if check_need_renew is True:
        request.set_Filter3Key("ExpiredStartTime")
        request.set_Filter3Value(INSTANCE_EXPIRED_START_TIME_IN_UTC_STRING)
        request.set_Filter4Key("ExpiredEndTime")
        request.set_Filter4Value(INSTANCE_EXPIRE_END_TIME_IN_UTC_STRING)
    if instance_id is not None:
        request.set_InstanceIds(json.dumps([instance_id]))
    if security_group_id:
        request.set_SecurityGroupId(security_group_id)
    request.set_PageNumber(page_number)
    request.set_PageSize(page_size)
    return _send_request(request)
# check the instances is renew or not
def describe_instance_auto_renew_setting(instance_ids, expected_auto_renew=True):
    describe_request = DescribeInstanceAutoRenewAttributeRequest()
    describe_request.set_InstanceId(instance_ids)
    response_detail = _send_request(request=describe_request)
    failed_instance_ids = ''
    if response_detail is not None:
        attributes = response_detail.get('InstanceRenewAttributes').get('InstanceRenewAttribute')
        if attributes:
            for item in attributes:
                auto_renew_status = item.get('AutoRenewEnabled')
                if auto_renew_status ! = expected_auto_renew:
                    failed_instance_ids += item.get('InstanceId') + ','
    if len(failed_instance_ids) > 0:
        logging.error("instance %s auto renew not match expect %s.", failed_instance_ids,
                      expected_auto_renew)
def setting_instance_auto_renew(instance_ids, auto_renew=True):
    logging.info('execute enable auto renew ' + instance_ids)
    request = ModifyInstanceAutoRenewAttributeRequest();
    request.set_Duration(1);
    request.set_AutoRenew(auto_renew);
    request.set_InstanceId(instance_ids)
    _send_request(request)
    describe_instance_auto_renew_setting(instance_ids, auto_renew)
# if using the instance id can be found means the instance is not renew successfully.
def check_instance_need_renew(instance_id):
    response = describe_need_renew_instance(instance_id=instance_id)
    if response is not None:
        return response.get('TotalCount') == 1
    return False
# Renew an instance for a month
def renew_instance(instance_id, period='1'):
    need_renew = check_instance_need_renew(instance_id)
    if need_renew:
        _renew_instance_action(instance_id=instance_id, period=period)
        # describe_need_renew_instance(instance_id=instance_id, check_need_renew=False)
def _renew_instance_action(instance_id, period='1'):
    request = RenewInstanceRequest()
    request.set_Period(period)
    request.set_InstanceId(instance_id)
    response = _send_request(request)
    logging.info('renew %s ready, output is %s ', instance_id, response)
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
    logging.info("Renew ECS Instance by OpenApi!")
    # Query whether there is any instance that needs to be renewed within the specified time range.
    describe_need_renew_instance()
    # Renew an instance by direct fee deduction
    renew_instance('i-1111')
    # Query the status of automatic renewal
    # describe_instance_auto_renew_setting('i-1111,i-2222')
    # Set automatic instance renewal
    # setting_instance_auto_renew('i-1111,i-2222')
```

If you want to learn other API operations in ECS, see [ECS API operation](../../../../intl.en-US/API Reference/Introduction.md#).

