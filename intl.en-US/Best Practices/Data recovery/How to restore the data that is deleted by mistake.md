# How to restore the data that is deleted by mistake {#concept_zzm_5qs_gfb .concept}

By taking CentOS 7 for example, this document introduces how to use Extundelete, an open source tool, to quickly restore accidentally deleted data.

## Overview {#section_gvz_vkx_gfb .section}

In practice, data may be deleted accidentally. In this case, how to restore the data quickly and effectively? Alibaba Cloud offers several ways to restore data, for example:

-   Roll back a [snapshot](../../../../reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) or [custom image](../../../../reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#) through the ECS console.
-   Purchase several ECS instances to implement [load balancing](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) and high availability for your services.
-   Use [Object Storage Service \(OSS\)](../../../../reseller.en-US/Product Introduction/What is OSS?.md#) to store a massive amount of data such as web pages, images, and videos.

There are a variety of open source data recovery tools for Linux, such as debugfs, R-Linux, ext3grep, Extundelete, and more. Of them, ext3grep and Extundelete are generally used. Both tools adopt the same recovery techniques, just that Extundelete is more powerful.

Extundelete is a Linux-based open source data recovery software. When using Linux instances, you can install this tool conveniently to quickly restore the data deleted accidentally as no Recycle Bin is available in Linux.

Extundelete can locate the position of an inode block by combining the inode information and logs so as to search for and restore the desired data. This powerful tool supports the disk-wide restoration of ext3/ext4 dual-format partitions.

Once data is deleted accidentally, firstly you need to unmount the disk or disk partition that contains the deleted data. This is because after a file is deleted, only the inode pointers of the file are zeroed while the actual file is still stored on the disk. If the disk is mounted in read/write mode, data blocks of the deleted file may be reallocated by the operating system. Once the data blocks are overwritten by new data, the original data will be lost completely, and cannot be restored by any means. Therefore, mounting a disk in read-only mode can reduce the risk of overwriting the data in blocks, thus improving the chances of restoring the data successfully.

**Note:** During the online restoration process, do not install Extundelete on the disk that has the deleted file. Otherwise, the data to be restored might be overwritten. Keep in mind to back up the disk by taking a snapshot before any operations.

## Intended audience {#section_gtk_qmx_gfb .section}

-   Users who accidentally delete files on a disk and no write operations have been performed on the disk after the deletion.
-   Users whose websites have low traffic and who have few ECS instances.

## Procedure {#section_jbx_rmx_gfb .section}

Software release: e2fsprogs-devel e2fsprogs gcc-c++ make \(compiler and more\) Extundelete-0.2.4.

**Note:** The libext2fs 1.39 or above is required for the normal operation of Extundelete. For ext4 support, however, make sure e2fsprogs 1.41 or higher is provided \(you can run the command dumpe2fs to check the version output\).

The above releases are available when this document is being written. Your downloads may be different.

-   **Deploy Extundelete**

    ```
    wget  http://zy-res.oss-cn-hangzhou.aliyuncs.com/server/extundelete-0.2.4.tar.bz2
    yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make    #Install related dependencies and libraries
    tar -xvjf extundelete-0.2.4.tar.bz2
    cd extundelete-0.2.4                                #Enter the program directory
    ./configure                                         #Installed successfully as shown below
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9801/154140567112896_en-US.png)

    ```
    make && make install
    ```

    At this point, the src directory appears. It contains an Extundelete executable file and a corresponding path. As shown below, the default file is installed in usr/local/bin, and the following demo is made in the usr/local/bin directory.

-   **Delete a file and use Extundelete to restore it**

    1.  Check the available disks and partitions of your ECS instance, then format and partition the /dev/vdb partition. For more information about formatting and partitioning, see [Format and mount a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).

        ```
        fdisk -l
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9801/154140567112898_en-US.png)

    2.  Mount the partitioned disk under the /zhuyun directory, and then create a file named hello.

        ```
        mkdir /zhuyun                                #Create the zhuyun directory.
        mount /dev/vdb1 /zhuyun                      #Mount the disk under the zhuyun directory.
        echo test > hello                            #Create a test file.
        ```

    3.  Run the md5sum command to generate the MD5 value of the file and note it down. You can compare the MD5 values of the file before and after the deletion to verify its integrity.

        ```
        md5sum hello
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9801/154140567112899_en-US.png)

    4.  Delete the hello file.

        ```
        rm -rf hello
        cd ~
        fuser -k /zhuyun                     #Terminate the process tree that uses a certain partition (skip this if you are sure that no resources are occupied).
        ```

    5.  Unmount the data disk

        ```
        umount /dev/vdb1                     #Before using any file restoration tool, unmount or mount the partitions to be restored in read-only mode to prevent their data from being overwritten.
        ```

    6.  Use Extundelete to restore the file.

        ```
        extundelete --inode 2 /dev/vdb1       #Query the contents in a certain inode. Using "2" means to search the entire partition. To  search a directory, just specify the inode and directory. Now you can see the deleted file and inode.
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9801/154140567112900_en-US.png)

        ```
        /usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1    #Restore the deleted file.
        ```

        At this point, the RECOVERED\_FILES directory appears under the directory where the command is executed. Check whether the file is restored.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9801/154140567112901_en-US.png)

        Check the MD5 values of the files before and after deletion. If they are the same, restoration is successful.

        ```
        --restore-inode 12                  # --restore-inode Restore by the specified inode.
        --extundelete --restore-all         # --restore-all   Restore all.
        ```


