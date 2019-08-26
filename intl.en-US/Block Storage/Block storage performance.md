# Block storage performance {#concept_ytm_vwj_ydb .concept}

This topic describes the performance, metrics, and test methods of block storage devices such as disks, shared block storage, and local disks.

## Performance metrics {#section_yzi_wb6_9gc .section}

The metrics for measuring storage performance include IOPS, throughput, and latency.

-   IOPS

    Input/output operations per second \(IOPS\) measures the number of write/read operations that can be performed each second. IOPS directly affects the performance of transaction-intensive applications, such as databases.

    Common IOPS performance characteristics that are measured include sequential and random operations. The following table describes these performance characteristics.

    |Metric|Description|Data access method|
    |:-----|:----------|:-----------------|
    |Total IOPS|The total number of I/O operations per second|Randomly and sequentially access locations in storage devices|
    |Random read IOPS|The average number of random read I/O operations per second|Randomly access locations in storage devices|
    |Random write IOPS|The average number of random write I/O operations per second|
    |Sequential read IOPS|The average number of sequential read I/O operations per second|Sequentially access locations in storage devices|
    |Sequential write IOPS|The average number of sequential write I/O operations per second|

-   Throughput

    Throughput measures the size of data transferred per second. Unit: Mbit/s. Throughput directly affects the performance of applications that require a large number of read/write operations, such as Hadoop offline computing applications.

-   Latency

    Latency is the period of time required to process an I/O request. Unit: s, ms, or us. High latency may cause performance deterioration or errors in applications with high requirements for latency, such as databases.

    -   Therefore, we recommend that you use enhanced SSDs, standard SSDs, shared SSD block storage, or local SSDs for latency-sensitive applications.
    -   For applications that require high throughput but do not have high requirements for latency, such as Hadoop offline computing applications, we recommend that you use ECS instances equipped with local SATA HDDs in the d1 or d1ne instance family.

You cannot use capacity as a metric to measure the performance of block storage, but the performance of block storage devices varies with their capacities. The larger the capacity of a block storage device is, the more powerful data processing capability the device has. Block storage devices of the same type have the same I/O performance per unit capacity. However, the performance of each disk increases linearly with its capacity until the upper limit for a single disk is reached.

**Note:** Block storage capacity is measured in binary units, such as kibibyte \(KiB\), mebibyte \(MiB\), gibibyte \(GiB\), or tebibyte \(TiB\). 1 KiB equals 1,024 bytes. 1 MiB equals 1,024 KiB. 1 GiB equals 1,024 MiB. 1 TiB equals 1,024 GiB.

## Disks {#section_0hu_6dh_p6f .section}

The following table lists the performance and typical scenarios of different types of disks.

|Performance category|Enhanced SSD|Standard SSD|Ultra disk|Disk[\*\*\*](#cloud)|
|:-------------------|:-----------|:-----------|:---------|:-------------------|
|Performance Level \(PL\)|PL3|PL2|PL1|N/A|N/A|N/A|
|Capacity of a single disk|1,261 GiB to 32,768 GiB|461 GiB to 32,768 GiB|20 GiB to 32,768 GiB|32,768 GiB|32,768 GiB|2,000 GiB|
|Maximum IOPS|1,000,000|100,000|50,000|25,000[\*](#ssd)|5,000|Several hundreds|
|Maximum throughput|4,000 Mbit/s|750 Mbit/s|350 Mbit/s|300 Mbit/s[\*](#ssd)|140 Mbit/s|30 Mbit/s to 40 Mbit/s|
|Formulas for calculating the performance of a single disk[\*\*](#singledisk)|IOPS = min\{1,800 + 50 × capacity, 1,000,000\}|IOPS = min\{1,800 + 50 × capacity, 100,000\}|IOPS = min\{1,800 + 50 × capacity, 50,000\}|IOPS = min\{1,800 + 30 × capacity, 25,000\}|IOPS = min\{1,800 + 8 × capacity, 5,000\}|N/A|
|Throughput = min\{120 + 0.5 × capacity, 4,000\} Mbit/s|Throughput = min\{120 + 0.5 × capacity, 750\} Mbit/s|Throughput = min\{120 + 0.5 × capacity, 350\} Mbit/s|Throughput = min\{120 + 0.5 × capacity, 300\} Mbit/s|Throughput = min\{100 + 0.15 × capacity, 140\} Mbit/s|N/A|
|Data reliability|99.9999999%|99.9999999%|99.9999999%|99.9999999%|99.9999999%|99.9999999%|
|API name|cloud\_essd|cloud\_ssd|cloud\_efficiency|cloud|
|Scenarios| -   OLTP databases: relational databases such as MySQL, PostgreSQL, Oracle, and SQL Server databases
-   NoSQL databases: non-relational databases such as MongoDB, HBase, and Cassandra databases
-   Elasticsearch distributed logs: Elasticsearch, Logstash, and Kibana \(ELK\) log analysis

 |Large and medium-sized development and testing applications that require high data reliability| -   Development and testing applications
-   System disks

 | -   Applications that are not frequently accessed or have low I/O loads
-   Applications that require low costs and random read and write I/O operations

 |

\* The performance of standard SSDs varies according to the sizes of data blocks. Smaller data blocks result in lower throughput and higher IOPS, as described in the following table. A standard SSD can achieve the committed IOPS performance only when it is attached to an I/O optimized instance.

|Data block size|Maximum IOPS|Throughput|
|:--------------|:-----------|:---------|
|4 KiB|25,000|100 Mbit/s|
|16 KiB|17,200|260 Mbit/s|
|32 KiB|9,600|300 Mbit/s|
|64 KiB|4,800|300 Mbit/s|

\*\* A standard SSD is used as an example to describe how to calculate the performance of a single disk:

-   Maximum IOPS: The baseline is 1,800 IOPS. It increases by 30 IOPS per GiB of storage. The maximum IOPS is 25,000.
-   Maximum throughput: The baseline is 120 Mbit/s. It increases by 0.5 Mbit/s per GiB of storage. The maximum throughput is 300 Mbit/s.

\*\*\* Basic disks are the previous generation of disks and are no longer available for purchase. You can choose from a variety of disks, such as ultra disks, standard SSDs, or enhanced SSDs based on your actual needs.

The random write latency varies according to disk categories. For the test commands, see [Performance tests](#section_jvz_vzv_ydb):

-   Enhanced ESSDs: 0.2 ms
-   Standard SSDs: 0.5−2 ms
-   Ultra disks: 1−3 ms
-   Basic disks: 5−10 ms

## Shared block storage {#section_uwx_y1h_rgo .section}

The following table lists the performance and typical scenarios of different types of shared block storage.

|Performance category|Shared SSD block storage|Shared ultra block storage|
|:-------------------|:-----------------------|:-------------------------|
|Maximum capacity of a single disk|32,768 GiB|32,768 GiB|
|Maximum capacity of a single instance|128 TiB|128 TiB|
|Maximum random read/write IOPS[\*](#IOPS)|30,000|5,000|
|Maximum sequential read/write throughput[\*](#IOPS)|512 Mbit/s|160 Mbit/s|
|Formulas for calculating performance of a single disk[\*\*](#singledisk2)|IOPS = min\{1,600 + 40 × capacity, 30,000\}|IOPS = min\{1,000 + 6 × capacity, 5,000\}|
|Throughput = min\{100 + 0.5 × capacity, 512\} Mbit/s|Throughput = min\{50 + 0.15 × capacity, 160\} Mbit/s|
|Scenarios| -   Oracle RAC
-   Failover cluster
-   High-availability servers

 |High-availability architecture of servers|

\* The maximum IOPS and throughput listed in the preceding table are the maximum performance of a bare shared block storage device that is attached to two or more instances at the same time during stress tests.

\*\* A shared SSD block storage device is used as an example to describe how to calculate the performance of a single disk:

-   Maximum IOPS: The baseline is 1,600 IOPS. It increases by 40 IOPS per GiB of storage. The maximum IOPS is 30,000.
-   Maximum throughput: The baseline is 100 Mbit/s. It increases by 0.5 Mbit/s per GiB of storage. The maximum throughput is 512 Mbit/s.

The latency varies according to the shared block storage categories as follows:

-   Shared SSD block storage: 0.5−2 ms
-   Shared ultra block storage: 1−3 ms

## Local disks {#section_gnd_a61_bgu .section}

For the performance of local disks, see [Local disks](reseller.en-US/Block Storage/Local disks.md#).

## Performance tests {#section_jvz_vzv_ydb .section}

We recommend that you use the FIO tool to test block storage performance for both Linux and Windows instances.

**Note:** You can also use other tools to test block storage performance, but the obtained benchmark may be different. For example, tools such as dd, sysbench, and iometer may be affected by test parameter settings and file systems, so the tools may not reflect the actual disk performance. The performance results in this topic are all from a Linux instance tested by using FIO, and are used as the performance reference for block storage products.

This topic takes a Linux instance as an example to describe how to use the FIO tool to test block storage performance. Before you test a block storage device, ensure that it is 4 KiB aligned.

**Warning:** You can test bare block storage disks to obtain more accurate performance data, but such tests may damage the structures of the file systems. Make sure that you have backed up your data before the test. We recommend that you use a new ECS instance which contains no data to test block storage performance to avoid data loss.

-   Run the following command to test random write IOPS:

    ``` {#codeblock_zxh_hqo_q7p}
    fio -direct=1 -iodepth=128 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
    ```

-   Run the following command to test random read IOPS:

    ``` {#codeblock_mjp_yto_viq}
    fio -direct=1 -iodepth=128 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
    ```

-   Run the following command to test sequential write throughput:

    ``` {#codeblock_dx3_ysw_9vx}
    fio -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
    ```

-   Run the following command to test sequential read throughput:

    ``` {#codeblock_lpy_5uk_9dt}
    fio -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
    ```

-   Run the following command to test random write latency:

    ``` {#codeblock_rg8_bd1_1xw}
    fio -direct=1 -iodepth=1 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -group_reporting -filename=iotest -name=Rand_Write_Latency_Testing
    ```

-   Run the following command to test random read latency:

    ``` {#codeblock_bkn_212_7ls}
    fio -direct=1 -iodepth=1 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -group_reporting -filename=iotest -name=Rand_Read_Latency_Testingrandwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -group_reporting -filename=iotest -name=Rand_Write_Latency_Testing
    ```


The following table uses the command for testing random write IOPS as an example to describe the parameter settings in FIO commands.

|Parameter setting|Description|
|:----------------|:----------|
|-direct=1|Indicates that the I/O buffer is ignored during the test and data is written directly.|
|-iodepth=128|Indicates that when you use AIO, a maximum of 128 I/O requests can be made at the same time.|
|-rw=randwrite|Indicates that the read/write policy is random writes. Other valid values for rw: -   randread \(random reads\)
-   read \(sequential reads\)
-   write \(sequential writes\)
-   randrw \(random reads and writes\)

 |
|-ioengine=libaio|Indicates that libaio \(the Linux-native asynchronous I/O facility\) is used as the testing method. There are two ways for an application to use I/O: -   Synchronous

In synchronous I/O mode, a thread sends only one I/O request at a time and waits until the I/O request is completed. In this case, the iodepth value is always smaller than 1 for a single thread. You can increase the iodepth value by using multiple concurrent threads. The iodepth value will reach its upper limit when there are 16 to 32 threads running concurrently.

-   Asynchronous

In asynchronous I/O mode, a thread uses libaio to send multiple I/O requests to the kernel at a time and waits until all these I/O requests are completed. Asynchronous I/O reduces the number of interactions and increases interaction efficiency.


 |
|-bs=4k| Indicates that the size of each block for one I/O is 4 KB \(4k\). If this parameter is not specified, default value 4k is used.

 When IOPS is tested, we recommend that you set `-bs` to a small value, such as 4k in this example command.

 When throughput is tested, we recommend that you set `-bs` to a large value, such as 1024k in other example commands.

 |
|-size=1G|Indicates that the size of the testing file is 1 GiB.|
|-numjobs=1|Indicates that the number of testing threads is 1.|
|-runtime=1000|Indicates that the test duration is 1,000 seconds. If this parameter is not specified, the file of the size specified by `-size` is written in blocks of the size specified by `-bs`.|
|-group\_reporting|Indicates that in the testing results, the statistics are displayed for a group of threads as a whole, not for each individual thread.|
|-filename=iotest|Indicates that the name of the test file is iotest. You can test bare block storage disks to obtain more accurate performance data, but such tests may damage the structures of the file systems. Make sure that you have backed up your data before the test.|
|-name=Rand\_Write\_Testing|Indicates that the name of the testing task is Rand\_Write\_Testing. You can specify any name you want.|

