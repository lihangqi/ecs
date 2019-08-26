# FAQs about ECS instances {#concept_gqy_fyx_wgb .concept}

-   FAQs about purchasing ECS instances
    -   [What can I do if there are no resources for sale when I buy an instance?](#section_lxw_bwz_qgb)
-   FAQs about instance billing
    -   [Are fees still incurred after a pay-as-you-go ECS instance is automatically stopped due to overdue payments or is manually stopped?](#section_utf_tx2_zdb)
    -   [What can I do if the order fails to be placed when switching the billing method from pay-as-you-go to subscription?](#section_bsy_tnq_wgb)
    -   [How long does it take to switch the billing method after the order is paid for?](#section_lfq_vnq_wgb)
    -   [What can I do if the switch from pay-as-you-go to subscription fails?](#section_oml_wnq_wgb)
    -   [Does the billing method for bandwidth change after I switch from pay-as-you-go to subscription?](#section_ph2_xnq_wgb)
    -   [I have an unpaid order to switch the billing method of an instance from pay-as-you-go to subscription. If I upgrade the instance, will the order still be valid?](#section_mbf_ynq_wgb)
    -   [What can I do if the switch from subscription to pay-as-you-go fails?](#section_fzl_5jr_l2b)
-   FAQs about reserved instances
    -   [What is a reserved instance?](#section_et2_64u_fmh)
    -   [Will the pay-as-you-go instances that match a reserved instance be automatically reserved?](#section_5g6_eu4_b0f)
    -   [What platforms are supported on reserved instances?](#section_xoy_vzx_szv)
    -   [Which instance type families do reserved instances support?](#section_j7h_12a_tuy)
    -   [Can reserved instances be matched to preemptible instances to provide a billing discount?](#section_m9r_qk6_39q)
    -   [Can I adjust the instance type families of reserved instances?](#section_uee_304_jt3)
    -   [For what scenarios are zonal reserved instances applied?](#section_wcp_t5l_01b)
    -   [For what scenarios are regional reserved instances applied?](#section_rym_4rw_cl5)
    -   [How is the zone flexibility of reserved instances applied?](#section_6vd_nvw_m73)
    -   [How are flexible instance specifications of reserved instances applied?](#section_i9g_3my_drv)
    -   [Do zonal reserved instances support flexible instance specifications?](#section_tpd_tx9_9ri)
    -   [Do zonal reserved instances support zone flexibility?](#section_qdz_h5b_f91)
    -   [Can I change a zonal reserved instance to a regional one?](#section_wry_8lc_jj4)
    -   [Can I change the scope of reserved instances across regions?](#section_m89_45m_v6k)
    -   [Can I use reserved instances across accounts?](#section_6ta_i2c_mga)
    -   [Can I use reserved instances to pay for the storage and network bills of pay-as-you-go instances?](#section_prg_o9w_0de)
    -   [Can I use reserved instances to pay for the bill of a specified instance?](#section_30a_ovt_uhz)
    -   [How are reserved instances billed?](#section_whe_bza_0u2)
    -   [When does a reserved instance take effect after I purchase it?](#section_cdy_tt0_n68)
    -   [When do reserved instances take effect after I modify, split, or merge them?](#section_kfw_q23_shl)
    -   [Why the No Upfront payment option is not displayed on the purchase page?](#section_95a_y2p_hcl)
    -   [Can I modify the payment type for a reserved instance?](#section_1ps_ydr_o6o)
    -   [Can I request a refund for a reserved instance?](#section_vnd_a46_hbz)
    -   [Can I resell a reserved instance?](#section_j9e_1zq_35v)
-   FAQs about connecting to an instance
    -   [Can multiple users connect to the Management Terminal simultaneously?](#section_mdm_w4q_wgb)
    -   [What can I do if I forget my password for remote connection?](#section_tym_x4q_wgb)
    -   [Why am I unable connect to the Management Terminal even after resetting the password for remote connection?](#section_huk_e8x_b38)
    -   [What can I do when authentication failed on the Management Terminal?](#section_xl9_o6y_79k)
    -   [What can I do if a black screen appears when I am connected to the Management Terminal?](#section_xrm_6sm_10m)
    -   [What can I do when I am unable to access the Management Terminal?](#section_65w_3px_xpu)
    -   [Why can't I use Internet Explorer 8 to access the Management Terminal?](#section_82j_21b_xj0)
    -   [When I use Firefox to access the Management Terminal, an error appears indicating that the secure connection has failed. What can I do?](#section_l6t_kik_vmy)
    -   [How do I remotely log on to a Linux instance?](#section_tkz_v77_wbf)
-   FAQs about instance management
    -   [How do I use f1 instances?](#section_ug1_lb2_d7l)
    -   [How do I upload files with the FTP client in macOS?](#section_39c_w47_rds)
    -   [How do I register my domain name after buying an ECS instance?](#section_br4_f3k_1jw)
    -   [How do I change the logon password of an instance?](#section_5dx_x72_cb8)
    -   [Why can't I switch a pay-as-you-go instance to a subscription one?](#section_b1y_dqm_rzx)
-   FAQs about changing instance specifications
    -   [How do I upgrade my ECS resources?](#section_3c2_9re_bpi)
    -   [I have upgraded an instance and no changes have taken effect yet. Why?](#section_ftn_d7x_vk5)

## What can I do if there are no resources for sale when I buy an instance? {#section_lxw_bwz_qgb .section}

If there are no available resources when you are creating an instance, you can take the following measures:

-   Change the region
-   Change the zone
-   Change resource configurations

If there are still no available resources, try to purchase resources at another time. Instance resources are dynamic. When resources are insufficient, Alibaba Cloud replenishes them as soon as it is able to.

You can also use the arrival notice feature to be notified when resources are available.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156206093048634_en-US.png)

## Are fees still incurred after a pay-as-you-go ECS instance is automatically stopped due to overdue payments or is manually stopped? {#section_utf_tx2_zdb .section}

When the payment for a pay-as-you-go instance is overdue, the instance is automatically stopped and taken out of service. The status of the instance changes to **Expired**, and no new fees are incurred.

Pay-as-you-go ECS instances can be manually stopped through the ECS console or by calling the StopInstance operation. When an instance is stopped, its status will change to **Stopped**. Billing of an instance in the **Stopped** state varies based on the network type of the instance:

-   VPC: Stopped instances in a VPC will not be billed if the No fees for stopped instances feature is enabled. ECS instances in a VPC start being billed when they are created, stop being billed when they are in the **Stopped** state, and resume being billed when the instance is started again. While in the Stopped state, the vCPUs, memory, and public IP addresses of an ECS instance will not incur any additional costs. However, data disks will continue to be billed. For more information, see [No fees for stopped VPC instances](../reseller.en-US/Pricing/No fees for stopped VPC instances.md#).
-   Classic network: ECS instances in a classic network will continue to be billed even while they are in the **Stopped** state.

## What can I do if the order fails to be placed when switching the billing method from pay-as-you-go to subscription? {#section_bsy_tnq_wgb .section}

A failure to switch billing methods may be caused for any of the following reasons:

-   The instance is in a state that does not support switching billing methods.
-   The instance is set to be automatically released and cannot switch billing methods.
-   The instance is in the **Expired** state.
-   The instance information has changed.
-   An order is unpaid for the instance.

If you are prompted with any of the preceding messages, adjust the instance accordingly.

## How long does it take to switch the billing method after the order is paid for? {#section_lfq_vnq_wgb .section}

After you have paid for the order, it takes about 1 to 4 seconds to switch the billing method of up to 20 instances. After the switch, the billing method of the instance is changed to **Subscription** in the console.

## What can I do if the switch from pay-as-you-go to subscription fails? {#section_oml_wnq_wgb .section}

Submit a ticket.

## Does the billing method for bandwidth change after I switch from pay-as-you-go to subscription? {#section_ph2_xnq_wgb .section}

No. You can only switch the billing method of instances and data disks. To change the billing method of bandwidth, see [Change public network bandwidth billing](reseller.en-US/Instances/Change configurations/Overview of configuration changes.md#ChangeBilling).

## I have an unpaid order to switch the billing method of an instance from pay-as-you-go to subscription. If I upgrade the instance, will the order still be valid? {#section_mbf_ynq_wgb .section}

A new order is created when you switch the billing method from pay-as-you-go to subscription. You must complete the payment for this order for the switch to take effect. If you upgrade the instance before the order is paid, the order payment cannot be completed because the instance components change and the original order amount does not meet the requirements of the new billing method. If you want to change the billing method, you must cancel the unpaid order and place a new order to switch the billing method.

## What can I do if the switch from subscription to pay-as-you-go fails? {#section_fzl_5jr_l2b .section}

A failure to switch billing methods may be caused for any of the following reasons:

-   The instance is in a state that does not support switching billing methods.
-   The instance is in the **Expired** state.
-   The instance information has changed.

If you are prompted with any of the preceding messages, adjust the instance accordingly. If this problem persists, submit a ticket.

## What is a reserved instance? {#section_et2_64u_fmh .section}

A reserved instance is a discount coupon that can be automatically applied to one or more pay-as-you-go instances \(excluding preemptible instances\) in your account as well as reserve instance resources. A combination of reserved and pay-as-you-go instances is more flexible and cost effective than just subscription instances.

## Will the pay-as-you-go instances that match a reserved instance be automatically reserved? {#section_5g6_eu4_b0f .section}

The system reserves resources to match reserved instances at the time of purchase only for zonal reserved instances. Regional reserved instances will not have resources reserved for them.

## What platforms are supported on reserved instances? {#section_xoy_vzx_szv .section}

Only Linux instances can be matched to reserved instances for a discount. To use reserved instances, make sure that the instances to be matched are running Linux, no matter which type of images you import, such as public images, custom images, shared images, or Marketplace images.

## Which instance type families do reserved instances support? {#section_j7h_12a_tuy .section}

Reserved instances support the following instance type families: sn1ne, sn2ne, se1ne, ic5, c5, g5, r5, hfc5, hfg5, and t5.

Reserved instances matching [t5 burstable instances \(t5\)](reseller.en-US/Instances/Instance type families/Burstable performance instances/Basic concepts.md#) are only available at the zone level. These reserved instances cannot be merged, split, or changed in scope.

## Can reserved instances be matched to preemptible instances to provide a billing discount? {#section_m9r_qk6_39q .section}

No.

## Can I adjust the instance type families of reserved instances? {#section_uee_304_jt3 .section}

No.

## For what scenarios are zonal reserved instances applied? {#section_wcp_t5l_01b .section}

We recommend that you purchase the zonal reserved instances when you have a specific reservation of instance resources.

## For what scenarios are regional reserved instances applied? {#section_rym_4rw_cl5 .section}

We recommend that you purchase the regional reserved instances when you want to make use of the zone flexibility and instance specifications flexibility of reserved instances.

## How is the zone flexibility of reserved instances applied? {#section_6vd_nvw_m73 .section}

Only regional reserved instances are zone-flexible. Example:

You hold the following running pay-as-you-go instance:

One ecs.c5.xlarge Linux instance in Qingdao Zone B. The instance name is C5PAYG-b.

You have purchased the following reserved instance:

One regional ecs.c5.xlarge reserved instance in China \(Qingdao\). The name of the reserved instance is C5RI.

C5RI matches the instance C5PAYG-b and applies a billing discount.

If you release C5PAYG-b, and start another instance of the same type named C5PAYG-c in Qingdao Zone C. C5RI matches the new instance C5PAYG-c and applies the same billing discount.

## How are flexible instance specifications of reserved instances applied? {#section_i9g_3my_drv .section}

Only regional reserved instances support flexible instance specifications. Example:

You hold one regional ecs.g5.4xlarge reserved instance to apply billing discounts for pay-as-you-go instances. It can match one ecs.g5.4xlarge instance, two ecs.g5.2xlarge instances, or four ecs.g5.xlarge instances.

You hold a one-year regional ecs.g5.xlarge reserved instance to apply billing discounts for pay-as-you-go instances. It can match one ecs.g5.xlarge instance running for one year, or one ecs.g5.2xlarge instance running for six months.

## Do zonal reserved instances support flexible instance specifications? {#section_tpd_tx9_9ri .section}

No. A zonal reserved instance can only match pay-as-you-go instances of the same instance type.

## Do zonal reserved instances support zone flexibility? {#section_qdz_h5b_f91 .section}

No. A zonal reserved instance can only match pay-as-you-go instances in the same zone.

## Can I change a zonal reserved instance to a regional one? {#section_wry_8lc_jj4 .section}

Yes. After you purchase a reserved instance, you can change its scope in the following manners:

-   From a zone level to a region level
-   From a region level to a zone level
-   From one zone to another in the same region

## Can I change the scope of reserved instances across regions? {#section_m89_45m_v6k .section}

No. For example, if you have a zonal reserved instance in Hangzhou Zone B, you can switch it to another zone or change it to a regional reserved instance in China \(Hangzhou\). However, you cannot change it to a regional or zonal reserved instance in another region.

## Can I use reserved instances across accounts? {#section_6ta_i2c_mga .section}

No.

## Can I use reserved instances to pay for the storage and network bills of pay-as-you-go instances? {#section_prg_o9w_0de .section}

No. Reserved instances are used to pay for the CPU and memory usage of pay-as-you-go instances.

## Can I use reserved instances to pay for the bill of a specified instance? {#section_30a_ovt_uhz .section}

No. When you have multiple instances that match a reserved instance, the discount of the reserved instance is applied automatically based on the optimized matching scheme.

## How are reserved instances billed? {#section_whe_bza_0u2 .section}

Reserved instances are billed separately and support the following payment options: All Upfront, Partial Upfront, and No Upfront.

The reserved instance term starts immediately after your purchase. You are charged based on your payment option regardless of whether pay-as-you-go instances are matched. The All Upfront option can save you the most money.

## When does a reserved instance take effect after I purchase it? {#section_cdy_tt0_n68 .section}

After purchase, the reserved instance takes effect on the hour of the current hour. It expires at 00:00:00 the day after the term end date. If you purchased a reserved instance with a term of one year at 2019-02-26 13:45:00, the reserved instance will take effect and be billed at 2019-02-26 13:00:00. The reserved instance will expire at 2020-02-27 00:00:00. If there are existing instances that match the purchased reserved instance at the time of purchase, the billing discount is applied to the hour bill generated from 13:00 on February 26, 2019 until the expiration of the reserved instance.

## When do reserved instances take effect after I modify, split, or merge them? {#section_kfw_q23_shl .section}

After a reserved instance is modified, split, or merged, a new reserved instance is generated, and the original one becomes invalid. The new reserved instance takes effect from the start of the hour. The original reserved instance becomes invalid at the same time. If you split an ecs.g5.2xlarge zonal reserved instance \(RI1\) into two zonal ecs.g5.xlarge reserved instances \(RI2 and RI3\) at 2019-02-26 13:45:00, then RI1 becomes invalid and RI2 and RI3 take effect at 2019-02-26 13:00:00. Starting 2019-02-26 13:00:00, the eligible reserved instance type changes from ecs.g5.2xlarge to ecs.g5.xlarge. If instances are matched immediately after RI2 and RI3 take effect, the hourly bill discount for ecs.g5.xlarge instances also starts to be applied at 2019-02-26 13:00:00.

## Why the No Upfront payment option is not displayed on the purchase page? {#section_95a_y2p_hcl .section}

The availability of this option depends on your ECS usage.

## Can I modify the payment type for a reserved instance? {#section_1ps_ydr_o6o .section}

No.

## Can I request a refund for a reserved instance? {#section_vnd_a46_hbz .section}

You can request a refund in the following cases:

-   You can request a no-hassle refund within five days of purchasing a reserved instance. Each account can only requests one no-hassle refund per year. Assume that you purchased an ECS instance and a reserved instance at the same time. If you request a no-hassle refund for one of the instances, you cannot request another no-hassle refund within the same year.
-   Instance resources are insufficient in the target region or zone after purchasing, splitting, merging, or changing the scope of reserved instances.

Incurred fees will be deducted from the requested refund, and a service fee of 15% of the refundable amount is charged. If you chose the Partial Upfront payment option and have hourly bills unpaid for the reserved instance, you must pay the bills before you can receive a refund.

## Can I resell a reserved instance? {#section_j9e_1zq_35v .section}

No.

## Can multiple users connect to the Management Terminal simultaneously? {#section_mdm_w4q_wgb .section}

No. Only one user can connect to the Management Terminal at a time.

## What can I do if I forget the password for remote connection? {#section_tym_x4q_wgb .section}

If you forgot your password, you can [modify the Management Terminal password](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#section_nmj_5mx_wdb).

## Why am I unable to connect to the Management Terminal even after resetting the password for remote connection? {#section_huk_e8x_b38 .section}

If the ECS instance that you are connecting to is not I/O optimized, you must [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console for the new password to take effect. If the ECS instance is restarted from within the instance itself, then the new password will not take effect.

## What can I do when authentication failed on the Management Terminal? {#section_xl9_o6y_79k .section}

This may be because you entered the wrong password. Follow these steps to troubleshoot the problem:

-   Enter the correct password.
-   If you forget your password, [modify the Management Terminal password](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#section_nmj_5mx_wdb) and try again.
-   If the ECS instance that you are connecting to is not I/O optimized, you must [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console for the new password to take effect.

## What can I do if a black screen appears when I am connected to the Management Terminal? {#section_xrm_6sm_10m .section}

The black screen indicates that the instance is in sleep mode. Perform the following operations based on your system:

-   For a Linux instance, click your mouse or press any key to activate the instance.
-   For a Windows instance, in the upper left corner of the Management Terminal, click **Send Remote Call** \> **CTRL+ALT+DELETE** to enter the logon interface.

## What can I do when I am unable to access the Management Terminal? {#section_65w_3px_xpu .section}

Use Google Chrome to connect to the Management Terminal, and press F12 to open the developer tool. Then go to the **Console** tab to analyze the information there and locate errors.

## Why can't I use Internet Explorer 8 to access the Management Terminal? {#section_82j_21b_xj0 .section}

The Management Terminal supports Internet Explorer 10 and later. You can download and use the latest versions of Internet Explorer or Google Chrome to access the Management Terminal.

We recommend that you use Google Chrome, as it offers the best support for the Management Terminal.

## When I use Firefox to access the Management Terminal, an error appears indicating that the secure connection has failed. What can I do? {#section_l6t_kik_vmy .section}

The version of Firefox that you are using may not use the same encryption algorithm as the Management Terminal.

We recommend that you use Google Chrome, as it offers the best support for the Management Terminal.

## How do I remotely log on to a Linux instance? {#section_tkz_v77_wbf .section}

Linux instances use SSH for remote connection. You can use any of the following methods to remotely log on to a Linux instance:

-   [Connect to an instance through the Management Terminal](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#)
-   [Connect to a Linux instance by using a password](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md#)
-   [Connect to a Linux instance by using SSH key pair](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md#)
-   [Connect to an instance through a mobile device](reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance on a mobile device.md#)

## How do I use f1 instances? {#section_ug1_lb2_d7l .section}

After your application for an f1 instance trial is approved, Alibaba Cloud will share an FPGA development image with you. This image supports CentOS 7u2. The image includes the complete Intel Quartus Prime suite of design software and the constraint files for the corresponding f1 device to provide a complete cloud development environment.

**Note:** The f1 instances can only be used in the China \(Hangzhou\) region.

The basic workflow when using f1 instances is as follows:

1.  After development, generate an intermediate QAR file during the compilation stage, and upload it to an OSS bucket. Then, register the QAR information to Alibaba Cloud through an API.

    We recommend that you use the free Intel Quartus Prime design software to complete development, compilation, and simulation operations on the cloud.

2.  Alibaba Cloud verifies the registration request of the QAR file. After the security of the QAR file is verified, Alibaba Cloud sends you an email that includes an FPGA image ID.
3.  When you deploy the image, call an API to associate the f1 instance with the FPGA image by specifying the IDs of the instance and image respectively.

    You can initiate the association operation in any scenario where ECS open APIs are available.

    -   As long as there is no FPGA image associated with the f1 instance, you can directly initiate the association operation.
    -   If the f1 instance has previously been associated with an FPGA image and has the image loaded, erase the FPGA image from the f1 instance before initiating the association operation.
4.  After the association, load the FPGA image by using APIs.

    You must initiate the load operation from the cloud server where the f1 instance is located. Then the underlying service of Alibaba Cloud burns the associated FPGA image to the corresponding FPGA on the instance.


If you want to restore the f1 instance to its initial state, call an API to erase the burned FPGA image from the f1 instance.

For more instructions on f1 instances, see:

-   [Create an f1 instance](reseller.en-US/Instances/Instance type families/Compute optimized type family with FPGA/Create an f1 instance.md#)
-   [Use OpenCL on an f1 instance](../reseller.en-US/Best Practices/FaaS instances best practices/Use OpenCL on an f1 instance.md#)
-   [Use RTL compiler on an f1 instance](../reseller.en-US/Best Practices/FaaS instances best practices/Use RTL compiler on an f1 instance.md#)

## How do I upload files with the FTP client in macOS? {#section_39c_w47_rds .section}

**Upload files by using the Terminal in macOS**

Open the Terminal in macOS or iTerm2 for Mac \(click [here](https://www.iterm2.com/) to download iTerm2\). Make sure that you select the correct path to be uploaded.

1.  Connect to the FTP server.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156206093043224_en-US.png)

2.  Enter the directory to be uploaded. If the directory is on a Windows instance, use this directory. If it is on a Linux instance, change the directory to htdocs.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156206093049119_en-US.png)

3.  Run the put command to upload files.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130429/156206093149120_en-US.png)


**Upload files by using a third-party tool**

1.  Click [here](https://www.yummysoftware.com/) to download Yummy FTP.
2.  Install Yummy FTP.
3.  Enter the server IP address, username, and password. Select Standard \(FTP\) in the Protocol field and 21 \(or a port number you are using\) in the Port field, and leave the SSH key field unselected.
4.  Click **Connect**.
5.  In the right section, select the directory where the files are to be uploaded. If the directory is on a Windows instance, use this directory. If it is on a Linux instance, change the directory to htdocs. In the left section, select the files and click the Upload icon to upload files.

    **Note:** If the prompt “Your security preferences only allow the installation of apps from the Mac App Store and authorized developers.” is displayed when you try to install Yummy FTP, follow these steps:

    1.  Choose **Preference** \> **Security and Privacy**.
    2.  Click the security lock at the lower-left corner of the window, and enter the administrator password.
    3.  Select **Anywhere** from the **Allow apps download from** menu.
    You can upload files with Yummy FTP.


If the problem still persists, submit a ticket.

## How do I register my domain name after buying an ECS instance? {#section_br4_f3k_1jw .section}

You can apply for a limited number of ICP Filing service codes for an instance. For more information, see [Prepare and check the instance or server](../../../../../reseller.en-US/Before ICP Filling/Host instances and service providers/Prepare and check the instance or server.md#).

For more information about the procedure of ICP filing, see [Quick start](../../../../../reseller.en-US/ICP Quick Start/Quick start.md#).

## How do I change the logon password of an instance? {#section_5dx_x72_cb8 .section}

For the detailed procedure, see [Change the instance logon password by connecting to the instance](reseller.en-US/Instances/Manage instances/Change the instance logon password by connecting to the instance.md#).

## Why can't I switch a pay-as-you-go instance to a subscription one? {#section_b1y_dqm_rzx .section}

To switch the billing method for an ECS instance, the instance must meet the following conditions:

## How do I upgrade my ECS resources? {#section_3c2_9re_bpi .section}

For information about upgrading ECS instances, see [Upgrade or downgrade instance configurations](reseller.en-US/Instances/Change configurations/Overview of configuration changes.md#).

-   With the exception of ECS instances using local storage, ECS instances support CPU scaling, memory scaling, and bandwidth upgrades while they are running.
-   You can attach a maximum of 16 data disks to an ECS instance. The disk size cannot be reduced after the data disks are upgraded.
-   The ECS bandwidth is measured in megabits per second \(Mbit/s\) and ranges between 0 and 200 Mbit/s. You can also temporarily upgrade the bandwidth, or downgrade the specifications of your ECS instances when you renew the subscription.

## I have upgraded an instance and no changes have taken effect yet. Why? {#section_ftn_d7x_vk5 .section}

To make the upgraded configuration take effect, you need to [Restart an instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#).

