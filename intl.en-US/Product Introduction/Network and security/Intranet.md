# Intranet {#concept_qrd_2z2_5db .concept}

Currently, Alibaba Cloud servers communicate over an intranet. They use a gigabit of shared bandwidth for non I/O optimized instances, and 10 gigabits of shared bandwidth for I/O optimized instances, with no special restrictions. However, because this is a shared network, the bandwidth may fluctuate.

If you have to transmit data between two ECS instances in the same region, use an intranet connection. Intranet connections can also be used to connect any combination of ECS, RDS, SLB, and OSS if they are deployed in the same region. The Internet speed of these products is based on a gigabit of shared bandwidth.

The network types, owners, regions, and security groups affect the intranet communication of ECS instances. See the following table for details.

|Network type|Owners|Regions|Security groups|How to enable intranet communication|
|:-----------|:-----|:------|:--------------|:-----------------------------------|
|VPC, same VPC|One account or different accounts|Same|Same|Enabled by default.|
|Different|Authorize security groups for each other.|
|VPC, different VPCs|One account or different accounts|Same|Either the same or different|Use Express Connect. For more information, see [Application scenarios from Product Introduction to Express Connect](../../../../reseller.en-US/Product Introduction/Scenarios.md).|
|Different|Different|
|Classic|One account|Same|Same|Enabled by default.|
|Different accounts|Either the same or different|Authorize security groups for each other. For more information, see [Scenarios of security groups](../../../../reseller.en-US/User Guide/Security groups/Scenarios.md).|

Private IP addresses are used for intranet communication. You cannot [change the private IP address](../../../../reseller.en-US/User Guide/Instances/Change IP addresses/Change the private IP of an ECS instance.md#) of an instance of the Classic network type, but you can change the private IP address of a VPC-Connected ECS instance. Private and public addresses of ECS instances do not support virtual IP \(VIP\) configuration.

By default, instances of different network types cannot communicate with one another in one intranet. VPC provides the [ClassicLink](../../../../reseller.en-US/User Guide/ClassicLink/ClassicLink overview.md) function, which allows you to link an ECS instance in the classic network to cloud resources in a VPC through the intranet.

