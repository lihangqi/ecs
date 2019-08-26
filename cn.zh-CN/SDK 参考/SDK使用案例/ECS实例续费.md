# ECS实例续费 {#concept_qhn_2sk_kfb .concept}

除了通过 ECS控制台或售卖页进行云服务器续费外，阿里云还支持直接通过 API 进行续费查询和续费管理

本文主要涉及如下关键功能：

-   按照过期时间查询云服务器
-   续费实例
-   查询云服务器自动续费时间
-   设置云服务器自动续费时间

对于包年包月的云服务器，生命周期非常重要。如果云服务器资源不能按时续费，将可能导致服务器被锁定甚至被释放，从而影响业务持续性。API 帮助您及时了解和检查资源的到期时间，并完成续费充值功能。

本篇需关注如下 API：

-   [查询实例列表](../../../../intl.zh-CN/API 参考/实例/DescribeInstances.md#)
-   [续费实例](../../../../intl.zh-CN/API 参考/实例/RenewInstance.md#)

## 查询指定范围内到期的云服务器 {#section_mby_lsk_kfb .section}

查询实例列表的 API，通过过滤参数，您可以查询一定时间范围内到期的实例信息。通过设置过滤参数 ExpiredStartTime 和 ExpiredEndTime（时间参数 按照 ISO8601 标准表示，并需要使用 UTC 时间。 格式为：yyyy-MM-ddTHH:mmZ） ，可以方便地查询该时间范围内到期的实例列表。如果需要通过安全组进行过滤，只需加上安全组 ID 即可。

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

## 续费云服务器 {#section_ycv_nsk_kfb .section}

续费实例只支持包年包月的服务器类型，不支持按量付费的服务器，同时要求用户必须支持账号的余额支付或信用支付。执行 API 的时候将执行同步的扣费和订单生成。因此，执行 API 的时候必须保证您的账号有足够的资金支持自动扣费。

```
def _renew_instance_action(instance_id, period='1'):
    request = RenewInstanceRequest()
    request.set_Period(period)
    request.set_InstanceId(instance_id)
    response = _send_request(request)
    logging.info('renew %s ready, output is %s ', instance_id, response)
```

续费实例将会自动完成扣费。在完成续费后，您可以根据InstanceId查询实例的资源到期时间。由于 API 为异步任务，查询资源到期时间可能需要延迟 10 秒才会变化。

## 开启云服务器自动续费 {#section_fyq_psk_kfb .section}

为了减少您的资源到期维护成本，针对包年包月的 ECS 实例，阿里云还推出了 [自动续费功能](../../../../intl.zh-CN/产品定价/续费实例/自动续费.md#)。 自动续费扣款日为服务器到期前第 9 天的 08:00:00。如果前一日执行自动扣费失败，将会继续下一日定时执行，直到完成扣费或者 9 天后到期资源锁定。您只需要保证自己的账号余额或者信用额度充足即可。

-   **查询自动续费设置**

    您可以通过 OpenAPI 来查询和设置自动续费。该 API 仅支持包年包月的实例，按量付费的实例执行将会报错。查询实例的自动续费状态支持一次最多查询 100 个包年包月的实例，多个实例 ID 以逗号连接。

    DescribeInstanceAutoRenewAttribute 的入参为实例 ID。

    InstanceId：支持最多查询 100 个包年包月的实例，多个实例 ID 以逗号连接。

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
                    if auto_renew_status != expected_auto_renew:
                        failed_instance_ids += item.get('InstanceId') + ','
    
    describe_auto_renew('i-1111,i-2222')
    ```

    返回内容如下：

    ```
    {"InstanceRenewAttributes":{"InstanceRenewAttribute":[{"Duration":0,"InstanceId":"i-1111","AutoRenewEnabled":false},{"Duration":0,"InstanceId":"i-2222","AutoRenewEnabled":false}]},"RequestId":"71FBB7A5-C793-4A0D-B17E-D6B426EA746A"}
    ```

    如果设置自动续费，则返回的属性AutoRenewEnabled为 true，否则返回 false。

-   **设置和取消云服务器的自动续费**

    设置自动续费有三个入参：

    -   InstanceId： 支持最多查询100个包年包月的实例，多个实例 ID 以逗号连接。
    -   Duration：支持 1、2、3、6、12，单位为月。
    -   AutoRenew：true/false， true为开启自动续费，false为取消自动续费。
    ```
    def setting_instance_auto_renew(instance_ids, auto_renew = True):
        logging.info('execute enable auto renew ' + instance_ids)
        request = ModifyInstanceAutoRenewAttributeRequest();
        request.set_Duration(1);
        request.set_AutoRenew(auto_renew);
        request.set_InstanceId(instance_ids)
        _send_request(request)
    ```

    执行成功返回 Response 如下：

    ```
    {"RequestId":"7DAC9984-AAB4-43EF-8FC7-7D74C57BE46D"}
    ```

    续费成功后，您可以再执行一次查询。如果续费成功将返回续费时长以及是否开启自动续费。

    ```
    {"InstanceRenewAttributes":{"InstanceRenewAttribute":[{"Duration":1,"InstanceId":"i-1111","AutoRenewEnabled":true},{"Duration":1,"InstanceId":"i-2222","AutoRenewEnabled":true}]},"RequestId":"7F4D14B0-D0D2-48C7-B310-B1DF713D4331"}
    ```


## 完整代码 {#section_nv5_xsk_kfb .section}

```
#  coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
from aliyunsdkcore import client
from aliyunsdkecs.request.v20140526.DescribeInstanceAutoRenewAttributeRequest import \
    DescribeInstanceAutoRenewAttributeRequest
from aliyunsdkecs.request.v20140526.DescribeInstancesRequest import DescribeInstancesRequest
from aliyunsdkecs.request.v20140526.ModifyInstanceAutoRenewAttributeRequest import \
    ModifyInstanceAutoRenewAttributeRequest
from aliyunsdkecs.request.v20140526.RenewInstanceRequest import RenewInstanceRequest
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
                if auto_renew_status != expected_auto_renew:
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
# 续费一个实例一个月
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
    # 查询在指定的时间范围内是否有需要续费的实例。
    describe_need_renew_instance()
    # 续费一个实例, 直接执行扣费
    renew_instance('i-1111')
    # 查询实例自动续费的状态
    # describe_instance_auto_renew_setting('i-1111,i-2222')
    # 设置实例自动续费
    # setting_instance_auto_renew('i-1111,i-2222')
```

如您想了解 ECS 中 API 的其它操作，请参考 [ECS中的API操作](../../../../intl.zh-CN/API 参考/简介.md#)。

