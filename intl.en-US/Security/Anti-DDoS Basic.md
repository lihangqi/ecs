# Anti-DDoS Basic {#concept_j1h_3rw_ydb .concept}

Anti-DDoS Basic is a free Distributed Denial of Service \(DDoS\) protection service that safeguards data and applications on your ECS instance.

## How Anti-DDoS Basic works {#section_qxq_3rw_ydb .section}

When the Anti-DDoS Basic is enabled, Alibaba Cloud Security monitors the inbound traffic in real time. When massive traffic or abnormal traffic involving DDoS attacks is monitored, Alibaba Cloud Security redirects the traffic, removes malicious traffic, and passes clean traffic back to the target ECS instance. This process is called **flow cleaning**. For more information, see .

**Note:** If Anti-DDoS Basic is enabled for an ECS instance, when the inbound traffic from Internet is higher than 5 Gbit/s, to secure the global cluster, Alibaba Cloud Security triggers a black hole to receive such traffic. For more information, see .

Factors that can trigger flow cleaning include:

-   Attack types. When specified attacks are identified in the inbound traffic, flow cleaning is triggered.
-   Traffic size. Generally, traffic involving DDoS attacks is measured in Gbit/s. When the inbound traffic into an ECS instance exceeds the specified threshold, flow cleaning is triggered no matter whether the traffic is normal or not.

Methods to clean traffic include filtering ICMP packets, limiting the bit rate, and limiting the packet forwarding rate.

Therefore, when using Anti-DDoS Basic, you must set the following thresholds:

-   BPS threshold: When the inbound traffic exceeds the BPS threshold, flow cleaning is triggered.
-   PPS threshold: When the inbound packet forwarding rate exceeds the PPS threshold, flow cleaning is triggered.

## Cleaning thresholds of each instance type {#section_uxq_3rw_ydb .section}

|Instance type|Maximum BPS threshold \(Mbit/s\)|Maximum PPS threshold \(PPS\)|
|:------------|:-------------------------------|:----------------------------|
|ecs.g5.16xlarge|20,000|4,000,000|
|ecs.g5.22xlarge|30,000|4,500,000|
|ecs.g5.2xlarge|2,500|800,000|
|ecs.g5.4xlarge|5,000|1,000,000|
|ecs.g5.6xlarge|7,500|1,500,000|
|ecs.g5.8xlarge|10,000|2,000,000|
|ecs.g5.large|1,000|300,000|
|ecs.g5.xlarge|1,500|500,000|
|ecs.sn2ne. 14xlarge|10,000|4,500,000|
|ecs.sn2ne. 2xlarge|2,000|1,000,000|
|ecs.sn2ne. 4xlarge|3,000|1,600,000|
|ecs.sn2ne 8xlarge|6,000|2,500,000|
|ecs.sn2ne.large|1,000|300,000|
|ecs.sn2ne.xlarge|1,500|500,000|
|ecs.c5.16xlarge|20,000|4,000,000|
|ecs.c5.2xlarge|2,500|800,000|
|ecs.c5.4xlarge|5,000|1,000,000|
|ecs.c5.6xlarge|7,500|1,500,000|
|ecs.c5.8xlarge|10,000|2,000,000|
|ecs.c5.large|1,000|300,000|
|ecs.c5.xlarge|1,500|500,000|
|ecs.sn1ne. 2xlarge|2,000|1,000,000|
|ecs.sn1ne. 4xlarge|3,000|1,600,000|
|ecs.sn1ne. 8xlarge|6,000|2,500,000|
|ecs.sn1ne.large|1,000|300,000|
|ecs.sn1ne.xlarge|1,500|500,000|
|ecs.r5.16xlarge|20,000|4,000,000|
|ecs.r5.22xlarge|30,000|4,500,000|
|ecs.r5.2xlarge|2,500|800,000|
|ecs.r5.4xlarge|5,000|1,000,000|
|ecs.r5.6xlarge|7,500|1,500,000|
|ecs.r5.8xlarge|10,000|2,000,000|
|ecs.r5.large|1,000|300,000|
|ecs.r5.xlarge|1,500|500,000|
|ecs.re4.20xlarge|15,000|2,000,000|
|ecs.re4.40xlarge|30,000|4,000,000|
|ecs.se1ne. 14xlarge|10,000|4,500,000|
|ecs.se1ne. 2xlarge|2,000|1,000,000|
|ecs.se1ne. 4xlarge|3,000|1,600,000|
|ecs.se1ne. 8xlarge|6,000|2,500,000|
|ecs.se1ne.large|1,000|300,000|
|ecs.se1ne.xlarge|1,500|500,000|
|ecs.se1.14xlarge|10,000|1,200,000|
|ecs.se1.2xlarge|1,500|400,000|
|ecs.se1.4xlarge|3,000|500,000|
|ecs.se1.8xlarge|6,000|800,000|
|ecs.se1.large|500|100,000|
|ecs.d1ne. 2xlarge|6,000|1,000,000|
|ecs.d1ne. 4xlarge|12,000|1,600,000|
|ecs.d1ne. 6xlarge|16,000|2,000,000|
|ecs.d1ne. 8xlarge|20,000|2,500,000|
|ecs.d1ne. 14xlarge|35,000|4,500,000|
|ecs.d1.2xlarge|3,000|300,000|
|ecs.d1.4xlarge|6,000|600,000|
|ecs.d1.6xlarge|8,000|800,000|
|ecs.d1.8xlarge|10,000|1,000,000|
|ecs.d1-c8d3.8xlarge|10,000|1,000,000|
|ecs.d1.14xlarge|17,000|1,800,000|
|ecs.d1-c14d3.14xlarge|17,000|1,400,000|
|ecs.i2.xlarge|1,000|500,000|
|ecs.i2.2xlarge|2,000|1,000,000|
|ecs.i2.4xlarge|3,000|1,500,000|
|ecs.i2.8xlarge|6,000|2,000,000|
|ecs.i2.16xlarge|10,000|4,000,000|
|ecs.i1.xlarge|800|200,000|
|ecs.i1.2xlarge|1,500|400,000|
|ecs.i1.4xlarge|3,000|500,000|
|ecs.i1-c10d1.8xlarge|6,000|800,000|
|ecs.i1-c5d1.4xlarge|3,000|400,000|
|ecs.i1.14xlarge|10,000|1,200,000|
|ecs.hfc5.large|1,000|300,000|
|ecs.hfc5.xlarge|1,500|500,000|
|ecs.hfc5.2xlarge|2,000|1,000,000|
|ecs.hfc5.4xlarge|3,000|1,600,000|
|ecs.hfc5.6xlarge|4,500|2,000,000|
|ecs.hfc5.8xlarge|6,000|2,500,000|
|ecs.hfg5.large|1,000|300,000|
|ecs.hfg5.xlarge|1,500|500,000|
|ecs.hfg5.2xlarge|2,000|1,000,000|
|ecs.hfg5.4xlarge|3,000|1,600,000|
|ecs.hfg5.6xlarge|4,500|2,000,000|
|ecs.hfg5.8xlarge|6,000|2,500,000|
|ecs.hfg5.14xlarge|10,000|4,000,000|
|ecs.c4.2xlarge|3,000|400,000|
|ecs.c4.4xlarge|6,000|800,000|
|ecs.c4.xlarge|1,500|200,000|
|ecs.ce4.xlarge|1,500|200,000|
|ecs.cm4.4xlarge|6,000|800,000|
|ecs.cm4.6xlarge|10,000|1,200,000|
|ecs.cm4.xlarge|1,500|200,000|
|ecs.gn5-c28g1.14xlarge|10,000|4,500,000|
|ecs.gn5-c4g1.xlarge|3,000|300,000|
|ecs.gn5-c4g1.2xlarge|5,000|1,000,000|
|ecs.gn5-c8g1.2xlarge|3,000|400,000|
|ecs.gn5-c8g1.4xlarge|5,000|1,000,000|
|ecs.gn5-c28g1.7xlarge|5,000|2,250,000|
|ecs.gn5-c8g1.8xlarge|10,000|2,000,000|
|ecs.gn5-c8g1.14xlarge|25,000|4,000,000|
|ecs.gn5i-c2g1.large|1,000|100,000|
|ecs.gn5i-c4g1.xlarge|1,500|200,000|
|ecs.gn5i-c8g1.2xlarge|2,000|400,000|
|ecs.gn5i-c16g1.4xlarge|3,000|800,000|
|ecs.gn5i-c28g1.14xlarge|10,000|2,000,000|
|ecs.gn4-c4g1.xlarge|3,000|300,000|
|ecs.gn4-c8g1.2xlarge|3,000|400,000|
|ecs.gn4-c4g1.2xlarge|5,000|500,000|
|ecs.gn4-c8g1.4xlarge|5,000|500,000|
|ecs.gn4.8xlarge|6,000|800,000|
|ecs.gn4.14xlarge|10,000|1,200,000|
|ecs.ga1.xlarge|1,000|200,000|
|ecs.ga1.2xlarge|1,500|300,000|
|ecs.ga1.4xlarge|3,000|500,000|
|ecs.ga1.8xlarge|6,000|800,000|
|ecs.ga1.14xlarge|10,000|1,200,000|
|ecs.f1-c28f1.7xlarge|5,000|2,000,000|
|ecs.f1-c8f1.2xlarge|2,000|800,000|
|ecs.f2-c28f1.14xlarge|10,000|2,000,000|
|ecs.f2-c28f1.7xlarge|5,000|1,000,000|
|ecs.f2-c8f1.2xlarge|2,000|400,000|
|ecs.f2-c8f1.4xlarge|5,000|1,000,000|
|ecs.t5-c1m1.2xlarge|1,200|400,000|
|ecs.t5-c1m1.large|500|100,000|
|ecs.t5-c1m1.xlarge|800|200,000|
|ecs.t5-c1m1.4xlarge|1,200|600,000|
|ecs.t5-c1m2.2xlarge|1,200|400,000|
|ecs.t5-c1m2.large|500|100,000|
|ecs.t5-c1m2.xlarge|800|200,000|
|ecs.t5-c1m2.4xlarge|1,200|600,000|
|ecs.t5-c1m4.2xlarge|1,200|400,000|
|ecs.t5-c1m4.large|500|100,000|
|ecs.t5-c1m4.xlarge|800|200,000|
|ecs.t5-lc1m1.small|200|60,000|
|ecs.t5-lc1m2.large|400|100,000|
|ecs.t5-lc1m2.small|200|60,000|
|ecs.t5-lc1m4.large|400|100,000|
|ecs.t5-lc2m1.nano|1,000|40,000|
|ecs.ebmg4.8xlarge|10,000|4,500,000|
|ecs.ebmg5.24xlarge|10,000|4,500,000|
|ecs.sccg5.24xlarge|10,000|4,500,000|
|ecs.xn4.small|500|50,000|
|ecs.mn4.small|500|50,000|
|ecs.mn4.large|500|100,000|
|ecs.mn4.xlarge|800|150,000|
|ecs.mn4.2xlarge|1,200|300,000|
|ecs.mn4.4xlarge|2,500|400,000|
|ecs.n4.small|500|50,000|
|ecs.n4.large|500|100,000|
|ecs.n4.xlarge|800|150,000|
|ecs.n4.2xlarge|1,200|300,000|
|ecs.n4.4xlarge|2,500|400,000|
|ecs.n4.8xlarge|5,000|500,000|
|ecs.e4.small|500|50,000|
|ecs.sn1.medium|500|100,000|
|ecs.sn1.large|800|200,000|
|ecs.sn1.xlarge|1,500|400,000|
|ecs.sn1.3xlarge|3,000|500,000|
|ecs.sn1.7xlarge|6,000|800,000|
|ecs.sn2.medium|500|100,000|
|ecs.sn2.large|800|200,000|
|ecs.sn2.xlarge|1,500|400,000|
|ecs.sn2.3xlarge|3,000|500,000|
|ecs.sn2.7xlarge|6,000|800,000|
|ecs.sn2.13xlarge|10,000|120,000|

## Related operations {#section_u1r_3rw_ydb .section}

By default, Anti-DDoS Basic is enabled for an ECS instance after it is created. You can do the following:

-   Set a threshold for flow cleaning. After an ECS instance is created, the maximum threshold for the instance type is used for Anti-DDoS Basic by default. However, the maximum BPS threshold for some instance types may be too big to be safe. Therefore, you must set a threshold according to your business needs. For more information, see in the Anti-DDoS Basic documentation.

-   \(Not recommended\) Cancel flow cleaning. When the inbound traffic to an ECS instance reaches the cleaning threshold, the entire traffic \(including normal traffic\) is cleaned. This may interrupt the normal business. To avoid business interruptions, you can cancel flow cleaning. For more information, see .

    **Warning:** If you cancel flow cleaning, when the inbound traffic to an ECS instance exceeds 5 Gbit/s, all traffic is routed to a black hole. Proceed with caution.


