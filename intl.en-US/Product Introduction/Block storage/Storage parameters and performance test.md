# Storage parameters and performance test {#concept_ytm_vwj_ydb .concept}

This document describes the performance index of block storage, performance testing methods, and how to interpret the testing results.

## Performance index of block storage {#section_b5z_vzv_ydb .section}

The main index for measuring storage performance include IOPS, throughput, and latency.

-   **IOPS**

    IOPS stands for Input/Output Operations per Second, which means the number of write or read operations that can be performed each second. Transaction-intensive applications, such as database applications, are sensitive to IOPS.

    The following table lists common performance characteristics that are measured.

    |IOPS performance characteristics|Description|
    |:-------------------------------|:----------|
    |Total IOPS|The total number of I/O operations per second|
    |Random read IOPS|The average number of random read I/O operations per second|Random access to locations on storage devices|
    |Random write IOPS|The average number of random write I/O operations per second|
    |Sequential read IOPS|The average number of sequential read I/O operations per second|Sequential access to locations on storage devices|
    |Sequential write IOPS|The average number of sequential write I/O operations per second|

-   **Throughput**

    Throughput measures the data size successfully transferred per second.

    Applications that require mass read or write operations \(such as Hadoop offline computing applications\) are sensitive to throughput.

-   **Latency**

    Latency is the period that is needed to complete an I/O request.

    For latency-sensitive applications \(such as databases\) in which high latency may lead to performance reduction or error reports in applications, we recommend that you use SSD disks, SSD Shared Block Storage, or local SSD disks.

    For throughput-sensitive applications \(such as Hadoop offline computing\) that are less sensitive to latency, we recommend that you use ECS instances with local HDD disks, such as instances of the d1 or d1ne instance type family.


## Performance {#section_i5z_vzv_ydb .section}

This section describes the performance of various block storage products.

Block Storage capacity is measured in binary units, such as kibibyte \(KiB\), mebibyte \(MiB\), gibibyte \(GiB\), or Tebibyte \(TiB\).

**Note:** 1 KiB is *1,024 bytes*. 1MiB is 1,024 KiB. 1GiB is 1,024 MiB. 1TiB is 1,024 GiB.

-   **Cloud disks**

    The following table lists the features and typical scenarios of different types of cloud disks.

    |Parameter|ESSD Cloud Disk|SSD Cloud Disk|Ultra Cloud Disk|Basic Cloud Disk|
    |:--------|:--------------|:-------------|:---------------|:---------------|
    |Capacity of a single disk|32,768 GiB|32,768 GiB |32,768 GiB |2,000 GiB|
    |Max. IOPS|1,000,000|25,000\*|5,000|Several hundreds|
    |Max. throughput|4,000 MBps|300 MBps\*|140 MBps|30−40 MBps|
    |Formulas to calculate performance of a single disk\*\*|IOPS = min\{1800 + 50 x capacity, 1,000,000\}|IOPS = min\{1800 + 30 x capacity, 25,000\}|IOPS = min\{1800 + 8 x capacity, 5,000\}|N/A|
    |Throughput = min \{120 + 0.5 x capacity, 4,000\} MBps|Throughput = min\{120 + 0.5 x capacity, 300\} MBps|Throughput = min\{100 + 0.15 x capacity, 140\} MBps|N/A|
    |Data reliability|99.9999999%|99.9999999%|99.9999999%|99.9999999%|
    |API name|cloud\_essd|cloud\_ssd|cloud\_efficiency|cloud|
    |Scenarios|     -   OLTP databases: relational databases such as MySQL, PostgreSQL, Oracle, and SQL Server
    -   NoSQL databases: non-relational databases such as MongoDB, HBase, and Cassandra
    -   ElasticSearch distributed logs: Elasticsearch, Logstash and Kibana \(ELK\) log analysis
 |     -   Large and medium-sized relational databases, such as MySQL, SQL Server, PostgreSQL, and Oracle
    -   Large or medium-sized development or testing applications that require high data reliability
 |     -   Small or medium-sized relational databases, such as MySQL, SQL Server, and PostgreSQL
    -   Large or medium-sized development or testing applications that require high data reliability and medium performance
 |     -   Applications with infrequent access or low I/O load. If higher I/O performance is needed, we recommend that you use SSD disks.
    -   Applications that require low costs and random read and write I/O operations
 |

    \* The performance of an SSD Cloud Disk varies with the data block size. Smaller data blocks result in lower throughput and higher IOPS, as shown in the following table. An SSD Cloud Disk can achieve the expected performance only when it is attached to an I/O-optimized instance. In other words, an SSD Cloud Disk cannot achieve the expected performance if it is not attached to an I/O-optimized instance.

    |Data block size|Maximum IOPS|Throughput|
    |:--------------|:-----------|:---------|
    |4 KiB|About 25,000|Far smaller than 300 MBps|
    |16 KiB|About 17,200|Close to 300 MBps|
    |32 KiB|About 9,600|
    |64 KiB|About 4,800|

    \*\* An SSD Cloud Disk is taken as an example to describe the performance of a single disk:

    -   The maximum IOPS: The baseline is 1,800 IOPS. It increases by 30 IOPS per GiB of storage. The maximum IOPS is 25,000.
    -   The maximum throughput: The baseline is 120 MBps. It increases by 0.5 MBps per GiB of storage. The maximum throughput is 300 MBps.
    The random write latency varies with the disk categories as follows:

    -   ESSD disks: 0.1−0.2 ms
    -   SSD disks: 0.5−2 ms
    -   Ultra Cloud Disks: 1−3 ms
    -   Basic Cloud Disks: 5−10 ms
-   **Shared Block Storage**

    The following table lists the features and typical scenarios of different types of Shared Block Storage.

    |Parameter|SSD Shared Bock Storage|Ultra Shared Block Storage|
    |:--------|:----------------------|:-------------------------|
    |Capacity|     -   Singe disk: 32,768 GiB
    -   Single instance: 128 TiB
 |     -   Singe disk: 32,768 GiB
    -   Single instance: 128 TiB
 |
    |Maximum random read/write IOPS\*|30,000|5,000|
    |Maximum sequential read/write throughput\*|512 MBps|160 MBps|
    |Formulas to calculate performance of a single disk\*\*|IOPS = min\{1600 + 40 x capacity, 30,000\}|IOPS = min\{1000 + 6 x capacity, 5,000\}|
    |Throughput = min\{100 + 0.5 x capacity, 512\} MBps|Throughput = min\{50 + 0.15 x capacity, 160\} MBps|
    |Scenarios|     -   Oracle RAC
    -   SQL Server
    -   Failover cluster
    -   High-availability architecture of servers
 |     -   High-availability architecture of servers
    -   High-availability architecture of development and testing databases
 |

    \* The maximum IOPS and throughput listed in the preceding table are the maximum performance of a bare shared block storage device that is attached to two or more instances at the same time during stress tests.

    \*\* An SSD Shared Block Storage is used as an example to describe the performance of a single disk:

    -   The maximum IOPS: The baseline is 1,600 IOPS. It increases by 40 IOPS per GiB of storage. The maximum IOPS is 30,000.
    -   The maximum throughput: The baseline is 100 MBps. It increases by 0.5 MBps per GiB of storage. The maximum throughput is 512 MBps.
    The latency varies with the shared block storage categories as follows:

    -   SSD Shared Block Storage: 0.5−2 ms
    -   Ultra Shared Block Storage: 1−3 ms
-   **Local disks**

    For the performance of local disks, see [Local disks](reseller.en-US/Product Introduction/Block storage/Local disks.md#).


## Test disk performance {#section_jvz_vzv_ydb .section}

fio in recommended to test disk performance.

**Note:** The disk benchmark tested by different tools varies with different operating systems. The performance parameters in this article are the results tested by fio with a Linux instance, and are used as the index reference of block storage product performance.

This section describes how to test disk performance, taking the fio tool used with a Linux instance as an example. Before you test the disk, verify that the disk is 4 KiB aligned.

**Warning:** You can test bare disks to obtain more accurate performance data, but the structure of the file system will be damaged. Make sure that you back up your data before testing. We recommend that you use a new ECS instance without data to test the disks to avoid data loss.

-   Test random write IOPS:

    ```
    fio -direct=1 -iodepth=128 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
    ```

-   Test random read IOPS:

    ```
    fio -direct=1 -iodepth=128 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
    ```

-   Test write throughput:

    ```
    fio -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
    ```

-   Test read throughput:

    ```
    fio -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
    ```


The command for testing random read IOPS is used as an example to describe the meaning of the parameters of a fio command, as shown in the following table.

|Parameter|Meaning|
|:--------|:------|
|-direct=1|Ignore I/O buffer when testing. Data is written directly.|
|-iodepth=128|Indicates that when you use AIO, the maximum number of I/O issues at the same time is 128.|
|-rw=randwrite|Indicates that the read and write policy is random write. Other options include:-   randread \(random read\)
-   read \(sequential read\)
-   write \(sequential write\)
-   randrw \(random read and write\)

|
|-ioengine=libaio|Use libaio as the testing method \(Linux AIO, Asynchronous I/O\). Usually there are two ways for an application to use I/O:-   Synchronous

Synchronous I/O only sends out one I/O request at a time, and returns only after the kernel is completed. In this case, the iodepth is always less than 1 for a single job, but can be resolved by multiple concurrent jobs. Usually 16−32 concurrent jobs can fill up the iodepth.

-   Asynchronous

The asynchronous method uses libaio to submit a batch of I/O requests each time, thus reducing interaction times and making interactions more effective.


|
|-bs=4k| Indicates the size of each block for one I/O is 4 KiB. If not specified, the default value 4 KiB is used.

 When IOPS is tested, we recommend that you set `bs` to a small value, for example, such as 4k in this example command.

 When throughput is tested, we recommend that you set `bs` to a large value, such as 1024k in this example command.

 |
|-size=1G|Indicates the size of the testing file is 1 GiB.|
|-numjobs=1|The number of testing jobs is 1.|
|-runtime=1000|Testing time is 1,000 seconds. If not specified, the test will write data of the file whose size is specified by `-size` block by block, with the data block size specified by `-bs`.|
|-group\_reporting|The display mode for showing the testing results. Group\_reporting means the statistics of each job are summed up, instead of all statistics of each job being shown.|
|-filename=iotest|The output path and name of the test files, for example, iotest. You can test bare disks to obtain more accurate performance data, but the test causes damage to the structure of the file system. Make sure that you back up your data before testing.|
|-name=Rand\_Write\_Testing|The name of the testing task.|

