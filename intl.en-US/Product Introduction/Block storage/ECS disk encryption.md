# ECS disk encryption {#concept_udk_5wj_ydb .concept}

ECS disks in this article refer to **cloud disks** and **Shared Block Storage devices**. They are referred to as **ECS disks** in the following contents, unless otherwise specified.

## What is ECS disk encryption? {#concept .section}

The ECS disk encryption feature allows you to encrypt new ECS disks so that you can meet encryption needs for scenarios such as certification requirements and business security. The ECS disk encryption feature means you do not have to create, maintain, or protect your own key management infrastructure, nor change any of your existing applications or maintenance processes. In addition, no extra encryption or decryption operations are required, making ECS disk encryption operations invisible to your applications or other operations.

Encryption and decryption processes hardly degrade ECS disk performance. For information on the performance testing method, see [storage parameters and performance test](reseller.en-US/Product Introduction/Block storage/Storage parameters and performance test.md#).

After an encrypted ECS disk is created and attached to an ECS instance, you can encrypt data that is:

-   Stored directly on the ECS disk.
-   Transmitted between the ECS disk and the instance. However, data in the instance operating system is not encrypted.
-   Created from the encrypted ECS disk, such as snapshots. These snapshots are called encrypted snapshots.

Encryption and decryption are performed on the host that runs the ECS instance, so the data transmitted from the ECS instance to the cloud disk is encrypted.

ECS disk encryption supports all available cloud disks \(Basic Cloud Disks, Ultra Cloud Disks, SSD Cloud Disks, and ESSDs\) and shared block storage \(Ultra Shared Block Storage and SSD Shared Block Storage\).

ECS disk encryption supports all available instance types and is supported in all regions.

## ECS disk encryption dependencies {#dependencies .section}

ECS disk encryption is dependent on the Key Management Service \(KMS\), which must be in the same region. However, you do not need to perform any additional operations in the KMS console to activate ECS disk encryption.

The first time you use the ECS disk encryption function \(such as when you are creating ECS instances or ECS disks\), you must first authorize and activate KMS. Otherwise, you cannot create encrypted ECS disks or instances with encrypted disks.

If you use an API or the CLI to use the ECS disk encryption function, such as [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#) or [CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#), you must first activate KMS on the Alibaba Cloud console.

The first time you encrypt a disk in a target region, Alibaba Cloud automatically creates a Customer Master Key \(CMK\) in the KMS region, exclusively for ECS. The CMK cannot be deleted. You can query the CMK in the KMS console.

## Key management for ECS disk encryption {#kms .section}

ECS disk encryption handles key management for you. Each new ECS disk is encrypted by using a unique 256-bit key \(derived from the CMK\). This key is also associated with all snapshots created from this ECS disk and any ECS disks subsequently created from these snapshots. These keys are protected by the key management infrastructure of Alibaba Cloud provided by KMS. This approach implements strong logical and physical security controls to prevent unauthorized access. Your data and the associated keys are encrypted based on the industry standard AES-256 algorithm.

You cannot change the CMK associated with encrypted ECS disks and snapshots.

The key management infrastructure of Alibaba Cloud conforms to the recommendations in \(NIST\) 800-57 and uses cryptographic algorithms that comply with the \(FIPS\) 140-2 standard.

Each Alibaba Cloud account has a unique CMK in each region. This key is separate from the data and is stored in a system protected by strict physical and logical security controls. Each encrypted disk and its snapshots use an encryption key that is unique to the specific disk. The encryption key is created from and encrypted by the CMK for the current user in the current region. The disk encryption key is only used in the memory of the host that runs your ECS instance. The key is never stored in plaintext in any permanent storage media \(such as an ECS disk\).

## Fees {#section_r4l_5r5_q8y .section}

The ECS disk encryption features incur no additional fees.

The CMK that ECS creates for you in each region is a service key. It does not consume your master key quota in a given region, meaning no additional fees are incurred.

**Note:** No additional fees are charged for any **read/write** operations on a disk, such as mounting/umounting, partitioning, and formatting. However, if you perform operations on a disk in the ECS console or by using APIs, KMS APIs are called and such calls consume the KMS API quota in the current region.

These operations include:

-   Creating encrypted disks by calling [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#) or [CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#).
-   Attaching an encrypted disk to an instance by calling [AttachDisk](../../../../reseller.en-US/API Reference/Disk/AttachDisk.md#).
-   Detaching an encrypted disk from an instance by calling [DetachDisk](../../../../reseller.en-US/API Reference/Disk/DetachDisk.md#).
-   Creating a snapshot by calling [CreateSnapshot](../../../../reseller.en-US/API Reference/Snapshots/CreateSnapshot.md#).
-   Restoring a disk by calling [ResetDisk](../../../../reseller.en-US/API Reference/Disk/ResetDisk.md#).
-   Re-initializing a disk by calling [ReInitDisk](../../../../reseller.en-US/API Reference/Disk/ReInitDisk.md#).

## Create an encrypted ECS disk {#howtocreate .section}

Currently, only cloud disks can be encrypted. You can create an encrypted cloud disk in the following ways:

-   Create a cloud disk as a data disk when creating an ECS instance or :

    -   Check Encrypted to create a encrypted blank cloud disk.
    -   Select an encrypted screenshot to create a cloud disk.
-   When using APIs or the CLI:

    -   Set the parameter `DataDisk.n.Encrypted` \([CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#)\) or `Encrypted` \([CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#)\) to `true`.
    -   Specify the `SnapshotId` parameter of the encrypted snapshot in CreateInstance or CreateDisk.

## Convert unencrypted data to encrypted data {#convert .section}

You cannot directly convert an **unencrypted disk** to an **encrypted disk**, or perform the converse operation.

You cannot convert a snapshot created from an **unencrypted disk** to an **encrypted snapshot**, or perform the converse operation.

Therefore, if you must switch the existing data from status **unencrypted** to **encrypted**, we recommend that you use the `rsync` command in a Linux instance or the `robocopy` command in a Windows instance to copy data from an **unencrypted** disk to a \(new\) **encrypted** disk.

Therefore, if you must switch the existing data from status **encrypted** to **unencrypted**, we recommend that you use the `rsync` command in a Linux instance or the `robocopy` command in a Windows instance to copy data from an **encrypted disk** to a \(new\) **unencrypted disk** .

## Limits {#limits .section}

ECS disk encryption has the following limits:

-   You can only encrypt ECS disks, not local disks or ephemeral disks.
-   You can only encrypt data disks, not system disks.
-   You cannot directly convert existing unencrypted disks into encrypted disks.
-   You cannot convert encrypted disks into unencrypted disks.
-   You cannot convert unencrypted snapshots to encrypted snapshots.
-   You cannot convert encrypted snapshots to unencrypted snapshots.
-   You cannot share images created from encrypted snapshots.
-   You cannot copy images created from encrypted snapshots across regions.
-   You cannot export images created from encrypted snapshots.
-   You cannot define CMKs for each region. They are generated by the system.
-   The ECS system creates CMKs for each region. You cannot delete these keys, and you do not incur fees from them.
-   After a cloud disk is encrypted, you cannot change the CMK used for encryption and decryption.

