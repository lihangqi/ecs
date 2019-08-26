# Matching rules of Reserved Instances {#concept_af1_zxq_dgb .concept}

Reserved Instances \(RIs\) provide a billing benefit only when they match Pay-As-You-Go instances. This topic describes the matching rules of RIs and provides some examples.

## Matching rules of RIs {#section_pqc_yyq_dgb .section}

The matching status between an RI and a Pay-As-You-Go instance cannot be manually managed. After you purchase an RI, the RI automatically matches one or more Pay-As-You-Go instances that have certain attributes within its term. The matching elements include operating system, instance type, and scope.

If you do not have any Pay-As-You-Go instances under your account, the RI will be idle while continuing to incur fees. After you purchase one or more applicable Pay-As-You-Go instances, the RI will automatically match with the instances immediately. Successful matching leads to an immediate billing discount to your Pay-As-You-Go instances. For more information, see [Reserved Instance billing](reseller.en-US/Pricing/Billing of Reserved Instances.md#).

An RI takes effect and is billed on the hour upon successful purchase. It expires at 00:00:00 the day after the term end date. For example, you purchased an RI on February 26, 2019 13:45:00 PM, with a term of one year. The RI took effect on 2019-02-26 13:00:00, and its billing also started from that time. It will expire on 2020-02-27 00:00:00. If you had matchable instances when you purchased the RI, the billing discount first applied to the bill generated from 13:00 to 14:00 on February 26, 2019 till the expiration of the RI.

We recommend that you purchase RIs in advance according to your business needs. You can also manage your RIs flexibly to maximize your billing discount.

The following table describes the features of regional RIs and zonal RIs.

|Feature|Regional RI|Zonal RI|Example|
|-------|-----------|--------|-------|
|Instance size flexibility|Supported. A regional RI can match different sizes of Pay-As-You-Go instances that are of the same instance type family in the same region.|Not supported. A zonal RI must match one or more Pay-As-You-Go instances of a specified size.|You have the following running Pay-As-You-Go instances: Two ecs.c5.xlarge Linux instances in China \(Qingdao\). The instance names are C5PAYG-1 and C5PAYG-2 respectively.

 You purchase the following RI:

 One regional ecs.c5.2xlarge RI in China \(Qingdao\). The RI name is C5RI.

 After the purchase, C5RI matches C5PAYG1 and C5PAYG2 simultaneously to provide a billing discount.|
|Zone flexibility|Supported. A regional RI can match all Pay-As-You-Go instances in the same region.|Not supported. A zonal RI must match one or more Pay-As-You-Go instances in a specified zone.|You have the following running Pay-As-You-Go instance: One ecs.c5.xlarge Linux instance in zone B of China \(Qingdao\). The instance name is C5PAYG-b.

 You purchase the following RI:

 One regional ecs.c5.xlarge RI in China \(Qingdao\). The RI name is C5RI.

 After the purchase, C5RI matches C5PAYG-b to provide a billing discount. You release C5PAYG-b, and then start another Linux instance named C5PAYG-c, which is of the same instance type as C5PAYG-b, in zone C. C5RI then matches C5PAYG-c to provide the same billing discount.

 |
|Resource Reservation|Not supported. If there is a shortage of available instances, you may need to wait for instances to become available.|Supported. A specified number of Pay-As-You-Go instances are reserved so that these instances can be created successfully.|You purchase the following RIs: Five zonal ecs.c5.xlarge RIs in zone B of China \(Qingdao\). The term is 1 year and the instance count is 2.

 Ten ecs.c5.xlarge instances will be reserved in zone B of China \(Qingdao\) for one year.|

