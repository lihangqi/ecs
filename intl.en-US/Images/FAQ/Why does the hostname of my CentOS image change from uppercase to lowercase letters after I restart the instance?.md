# Why does the hostname of my CentOS image change from uppercase to lowercase letters after I restart the instance? {#concept_ulc_fxf_1hb .concept}

After an ECS instance is restarted for the first time, the hostname \(hostname\) of some CentOS 7 instances is changed from uppercase letters to lowercase letters. This topic lists the impacted image types and the solution.

## Examples of hostname changes {#section_pcd_3xf_1hb .section}

The following table shows examples of changes before and after the initial restart of a CentOS instance with an uppercase hostname.

|Instance hostname example|Hostname change after the initial restart|Do the lowercase letters remain in subsequent restarts?|
|:------------------------|:----------------------------------------|:------------------------------------------------------|
|iZm5e1qe09gy5sxx1ps5zX|izm5e1qe09gy5sxx1ps5z6x|Yes|
|ZZHost|zzhost|Yes|
|NetworkNode|networknode|Yes|

## Impact scope {#section_ps5_kxf_1hb .section}

**Impacted images**

The following CentOS public images and the custom images created by using these public images are impacted.

-   centos\_7\_2\_64\_40G\_base\_20170222.vhd
-   centos\_7\_3\_64\_40G\_base\_20170322.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170503.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170523.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170625.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170710.vhd
-   centos\_7\_02\_64\_20G\_alibase\_20170818.vhd
-   centos\_7\_03\_64\_20G\_alibase\_20170818.vhd
-   centos\_7\_04\_64\_20G\_alibase\_201701015.vhd

**Impacted hostname types**

If the applications deployed in your instance are case-sensitive to the hostname, and you restart the target instance, your services will be impacted. To resolve this issue, you can use an appropriate method described in this topic to fix this error according to the required hostname type or types:

|Hostname convention|Is the name changed?|When does the change occur?|Do I proceed with this topic?|
|:------------------|:-------------------|:--------------------------|:----------------------------|
|The hostname has some uppercase letters in the instance that you create in the ECS console or by using the API.|Yes|Initial restart|Yes|
|The hostname has only lowercase letters in the instance that you create in the ECS console or by using the API.|No|N/A|No|
|The hostname had some uppercase letters, but were changed to lowercase letters after you log on to the instance.|No|N/A|Yes|

## Solution {#section_igh_hxf_1hb .section}

To retain a hostname with uppercase letters after you restart the instance, follow these steps:

1.  Connect to the instance.
2.  Run the following command to view the current hostname:

    ```
    [root@izbp193nf1pk3i161uynzzx ~]# hostname
    izbp193nf1pk3i161uynzzx
    ```

3.  Run the following command to set the hostname:

    ```
    hostnamectl set-hostname --static iZbp193nf1pk3i161uynzzX
    ```

4.  Run the following command to view the updated hostname:

    ```
    [root@izbp193nf1pk3i161uynzzx ~]# hostname
    iZbp193nf1pk3i161uynzzX
    ```


## What to do next {#section_eb3_1bh_1hb .section}

If you are using a custom image, update the cloud-init tool to the latest version, and then create the custom image again. Otherwise, the same error occurs when you use the original custom image to create a new instance. For more information, see [Install cloud-init for Linux images](reseller.en-US/Images/Custom image/Import images/Install cloud-init for Linux images.md#) and [Create a custom image by using an instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

