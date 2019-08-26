# Multi-queue for NICs {#concept_xwg_mjw_ydb .concept}

A single CPU is not sufficient for handling network interruptions. Therefore, you should route NIC interruptions in the ECS instances to different CPUs. Results of network PPS and bandwidth tests show that a solution that uses two queues instead of one queue can enhance network performance by 50% to 100%. A solution that uses four queues can bring further significant increases in network performance.

## ECS instance types supporting multi-queue {#section_bgd_bkw_ydb .section}

See [Instance type families](reseller.en-US/Product Introduction/Instance type families.md#) to find instance types supporting multi-queue and the number of queues that are supported.

## Images supporting multi-queue {#section_cgd_bkw_ydb .section}

The following public images officially provided by Alibaba Cloud support multi-queue:

**Note:** Whether an image supports multi-queue is not related to the memory address width of the operating system.

-   CentOS 6.8/6.9/7.2/7.3/7.4
-   Ubuntu 14.04/16.04
-   Debian 8.9
-   SUSE Linux Enterprise Server 12 SP1
-   Windows 2012 R2 and Windows 2016: You may be invited to test this feature in the future.

The SUSE Linux Enterprise Server 12 SP2 edition will be available soon.

## Configure multi-queue support for NICs on a Linux ECS instance {#section_egd_bkw_ydb .section}

We recommend that you use one of the latest Linux distributions, such as CentOS 7.2, to configure multi-queue for the NICs.

Here we take CentOS 7.2 as an example to illustrate how to configure multi-queue for the NIC. In this example, we want to configure two queues, and the NIC name is eth0.

-   To check whether the NIC supports multi-queue, run the command: `ethtool -l eth0`.

-   To enable multi-queue for the NIC, run the command: `ethtool -L eth0 combined 2`.

-   If you are using more than one NIC, configure each NIC.

    ```
    
        [root@localhost ~]# ethtool -l eth0
        Channel parameters for eth0:
        Pre-set maximums:
        RX: 0
        TX: 0
        Other: 0
        Combined: 2 # This line indicates that a maximum of two queues can be configured
        Current hardware settings:
        RX: 0
        TX: 0
        Other: 0
        Combined: 1 #It indicates that one queue is currently taking effect
        [root@localhost ~]# ethtool -L eth0 combined 2 # It sets eth0 to use two queues currently
    ```

-   We recommend that you enable the irqbalance service so that the system can automatically adjust the allocation of the NIC interrupts on multiple CPU cores. Run the command: `systemctl start irqbalance` \(this feature is enabled by default in CentOS 7.2\).

-   If the network performance is not improved as expected after the multi-queue feature is enabled, you can enable the RPS feature. See the following Shell script.

    ```
    
        #!/bin/bash
        cpu_num=$(grep -c processor /proc/cpuinfo)
        quotient=$((cpu_num/8))
        if [ $quotient -gt 2 ]; then
            quotient=2
        elif [ $quotient -lt 1 ]; then
            quotient=1
        fi
        for i in $(seq $quotient)
        do
            cpuset="${cpuset}f"
        done
        for rps_file in $(ls /sys/class/net/eth*/queues/rx-*/rps_cpus)
        do
            echo $cpuset > $rps_file
        done
    ```


## Configure multi-queue support for NICs on a Windows ECS instance {#section_qgd_bkw_ydb .section}

**Note:** We are inviting Windows users to test the performance improvement. Windows systems see improved network performance after using multi-queue for NICs, but the improvement is not as much as for Linux systems.

If you are using a Windows instance, you must install the driver to use the multi-queue feature for NICs.

To install the driver for Windows systems, follow these steps:

1.  Open a ticket to request and download the driver installation package.
2.  Unzip the driver installation package. For Windows 2012/2016 systems, use the driver in the Win8/amd64 folder.
3.  Upgrade the NIC driver:
    1.  Select **Device Manager** \> **Network adapters**.
    2.  Right click **Red Hat VirtIO Ethernet Adapter** and select **Update Driver**.
    3.  Select the Win8/admin64 directory of the driver directory that you have unzipped, and update the driver.
4.  Recommended: Restart the Windows system after the driver is upgraded.

The multi-queue feature for NICs is now ready to use.

