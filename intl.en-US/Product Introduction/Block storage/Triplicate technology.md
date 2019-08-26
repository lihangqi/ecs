# Triplicate technology {#concept_pnm_hdw_ydb .concept}

The Alibaba Cloud Distributed File System provides stable and efficient data access and reliability for ECS. Triplicate technology, that is, the process of making and distributing three copies of data, is the principle concept implemented in the Alibaba Cloud Distributed File System.

When you perform read and write operations on cloud disks, the operations are translated into the corresponding processes on the files stored in Alibaba Cloud data storage system. The Distributed File System of Alibaba Cloud uses a flat design in which a linear address space is divided into slices, also called chunks. Each chunk has three copies stored on different server nodes on different racks. This guarantees data reliability.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9559/15379629265222_en-US.png)

## How triplicate technology works {#section_ngj_jdw_ydb .section}

Triplicate technology involves three key components: Master, Chunk Server, and Client. To demonstrate how triplicate technology works, in this example, the write operation of an ECS user undergoes several conversions before being executed by the Client. The process is as follows:

1.  The Client determines the location of a chunk corresponding to a write operation.
2.  The Client sends a request to the Master to query the storage locations \(that is, the Chunk Servers\) of the three copies of the chunk.
3.  The Client sends write requests to the corresponding three Chunk Servers according to the results returned from the Master.
4.  The Client returns a message that indicates whether the operation was successful.

This strategy guarantees that all the copies of a chunk are distributed on different Chunk Servers on different racks, effectively reducing the potential of total data loss caused by failure of a Chunk Server or a rack.

## Data protection {#section_pgj_jdw_ydb .section}

If a system failure occurs because of a corrupted node or hard drive failure, some chunks may lose one or more of the three valid chunk copies associated with them. If this occurs and triplicate technology is enabled, the Master replicates data between Chunk Servers to replace the missing chunk copies across different nodes.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9559/15379629265223_en-US.png)

To summarize, all your operations \(additions, modifications, or deletions\) on cloud disk data are synchronized to the three chunk copies at the bottom layer. This mode ensures the reliability and consistency of your data.

Furthermore, we recommend you implement appropriate backup strategies, [snapshots](../../../../reseller.en-US/User Guide/Snapshots/Create snapshots.md#), and other precautionary actions to restore and protect your data and guarantee its availability against other types of failures, such as viruses, human error, or malicious activity on your account. No single technology can solve all the problems, so you must choose appropriate data protection measures to establish a solid defense line for your valuable business data.

