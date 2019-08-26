# ECS disk encryption {#concept_udk_5wj_ydb .concept}

When you need to encrypt the data stored on your ECS disks for security or compliance purposes, you can use Alibaba Cloud ECS disk encryption without the need to build, maintain, or protect your own key management infrastructure. This way you can protect data privacy based on your specific needs.

ECS disks in this topic refer to cloud disks and Shared Block Storage unless otherwise specified.

The system disk is encrypted by using image encryption. For more information, see [Image encryption](intl.en-US/ECS/BYOK documentation/Image encryption.md#).

## What is ECS disk encryption? {#concept .section}

ECS disk encryption automatically encrypts the data sent to your ECS disks from ECS instances and decrypts the data when the system reads it. Moreover, the encryption and decryption processes have little impact on ECS disk performance. For information on how to test the performance of your ECS disks, see [Storage parameters and performance tests](../../../../../intl.en-US/Block storage/Storage parameters and performance tests.md#).

After an encrypted ECS disk is created and attached to an ECS instance, the system encrypts the following data:

-   Static data stored on the ECS disk
-   Data transmitted between the ECS disk and the instance \(Data in the instance operating system is not encrypted.\)
-   All snapshots created from the encrypted ECS disk \(namely, encrypted snapshots\)
-   All ECS disks created from the encrypted snapshot \(namely, encrypted ECS disks\)

## ECS disk encryption methods {#dependencies .section}

When creating an encrypted ECS disk, the system must use the Customer Master Key \(CMK\) provided by the Key Management Service \(KMS\) in the same region. Therefore, before you can use the ECS disk encryption feature for the first time by using the ECS console or the API, you must activate the [Key Management Service](https://www.alibabacloud.com/product/key-management-service).

After activating KMS, you can use the CMK by using either of the methods described in the following table.

|Method|Description|Billing|
|:-----|:----------|:------|
|Use the ECS-created CMK.|When you use the ECS disk encryption feature in a region for the first time, ECS automatically creates a CMK specially for ECS in the region of KMS. You can view this CMK in the KMS console, but you cannot delete this CMK.|Free of charge. Moreover, ECS-created CMKs are not counted as part of your quota of CMKs allowed for each region.|
|Bring Your Own Key \(BYOK\).|You can create your own CMK in Alibaba Cloud KMS and use it to encrypt your ECS disks.**Note:** Creating your own CMK can allow for greater flexibility in that you can create, change, and disable your CMK to implement access control in line with your own specific requirements.

|Such keys are charged. For more information, see [Billing](#).|

## Key management for ECS disk encryption {#kms .section}

ECS disk encryption uses the standard AES-256 algorithm and encrypts your volumes by using data keys. Each Alibaba Cloud account has a unique CMK in each Alibaba Cloud region. This CMK is separated from your data and is stored in a system that is under strict control both physically and logically.

Each new ECS disk in a region is encrypted by using a unique 256-bit key \(derived from the CMK\) in the region. This key is also associated with all snapshots created using this ECS disk and any ECS disks subsequently created using these snapshots. These keys are protected by the key management infrastructure provided by Alibaba Cloud KMS. This approach implements strong logical and physical security controls to prevent unauthorized access. The key management infrastructure of Alibaba Cloud complies with the NIST 800-57 recommendations and uses the FIPS 140-2 compliant algorithms.

ECS disk encryption keys are only used in the memory of the host where your ECS instance runs. These keys are never stored in plain text in any permanent media \(such as an ECS disk\).

## Limits {#limits .section}

-   Only basic cloud disks, ultra cloud disks, SSD cloud disks, and Shared Block Storage can be encrypted. Local disks and ESSD cloud disks cannot be encrypted.
-   Existing unencrypted disks cannot be directly encrypted.
-   Encrypted disks cannot be directly unencrypted.
-   ECS Bare Metal Instances \(X-Dragon\) are not supported.

## Billing {#section_r4l_5r5_q8y .section}

|Item|Billing|
|:---|:------|
|ECS disk encryption|Free of charge.|
|CMKs created by ECS in each region|Free of charge. Moreover, ECS-created CMKs are not counted as part of your quota of CMKs allowed for each region.|
|CMKs that you create|Such CMKs incur fees.|
|All read and write operations on cloud disks, including mounting, unmounting, partitioning, and formatting disks|Free of charge.|
|ECS disk management operations, which are counted to the number of times that you call the KMS API in the corresponding region, regardless of whether you perform such management operations by using the ECS console or the APIManagement operations on encrypted ECS disks include:

-   Create an encrypted disk \([RunInstances](../../../../../intl.en-US/API Reference/Instances/RunInstances.md#), [CreateInstance](../../../../../intl.en-US/API Reference/Instances/CreateInstance.md#), or [CreateDisk](../../../../../intl.en-US/API Reference/Disk/CreateDisk.md#)\).
-   Mount a disk \([AttachDisk](../../../../../intl.en-US/API Reference/Disk/AttachDisk.md#)\).
-   Unmount a disk \([../../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9887.md\#](../../../../../intl.en-US/API Reference/Disk/DetachDisk.md#)\)
-   Create a snapshot \([../../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9905.md\#](../../../../../intl.en-US/API Reference/Snapshots/CreateSnapshot.md#)\).
-   Roll back a disk \([ResetDisk](../../../../../intl.en-US/API Reference/Disk/ResetDisk.md#)\).
-   Reinitialize a disk \([ReInitDisk](../../../../../intl.en-US/API Reference/Disk/ReInitDisk.md#)\).

 | Free of charge.

 |

Warning:

Make sure that your payment is successful. Otherwise, operations will fail and additional fees will occur.

## Create an encrypted ECS disk in the ECS console {#howtocreate .section}

**Method 1: Create an encrypted ECS disk along with an instance**

When you [create an instance](../../../../../intl.en-US/Instances/ECS instance life cycle/Create an instance/Create an instance by using the wizard.md#), you can create an encrypted ECS disk by using an encrypted snapshot or the CMK, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/127723/155385234141784_en-US.png)

**Method 2: Create an encrypted ECS disk separately**

On the **Disks** page, you can create an encrypted ECS disk by using an encrypted snapshot or the CMK. For information on how to create an ECS disk separately, see [Create a cloud disk](../../../../../intl.en-US/Block storage/Block storage/Create a cloud disk/Create a cloud disk.md#).

## Create an encrypted ECS disk by calling APIs {#section_ern_2w4_xgb .section}

-   Create an ECS disk along with an instance: When you call [RunInstances](../../../../../intl.en-US/API Reference/Instances/RunInstances.md#) or [CreateInstance](../../../../../intl.en-US/API Reference/Instances/CreateInstance.md#), set the DataDisk.n.Encrypted parameter to true and specify a KMSKeyId.
-   Create an ECS disk separately: When you call [CreateDisk](../../../../../intl.en-US/API Reference/Disk/CreateDisk.md#), set the Encrypted parameter to true and specify a KMSKeyId.
-   Create an ECS disk by using an encrypted snapshot: When you call [RunInstances](../../../../../intl.en-US/API Reference/Instances/RunInstances.md#), [CreateInstance](../../../../../intl.en-US/API Reference/Instances/CreateInstance.md#), or [CreateDisk](../../../../../intl.en-US/API Reference/Disk/CreateDisk.md#), specify the SnapshotId of the encrypted snapshot.

## Change the encryption status {#convert .section}

For ECS disks that you have created, you cannot directly change their encryption status. The following table shows how to change the encryption status of your disk data.

|Encryption status change|Windows|Linux|
|:-----------------------|:------|:----|
|Change unencrypted data to encrypted data.|Run the robocopy command to copy data from an unencrypted disk to a newly created encrypted disk.|Run the rsync command to copy data from an unencrypted disk to a newly created encrypted disk.|
|Change encrypted data to unencrypted data.|Run the robocopy command to copy data from an encrypted disk to a newly created unencrypted disk.|Run the rsync command to copy data from an encrypted disk to a newly created unencrypted disk.|

