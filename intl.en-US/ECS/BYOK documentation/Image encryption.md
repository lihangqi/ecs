# Image encryption {#concept_gmr_nnr_bhb .concept}

The ECS image encryption function allows you to add or replace keys to generate a new encrypted image when you copy an image. You can use Customer Master Keys \(CMKs\) generated automatically by the system or use the Bring Your Own Key \(BYOK\) model.

## What is image encryption? {#section_ijf_131_chb .section}

Image encryption is in the beta phase and only available in China \(Hong Kong\).

When you need to encrypt the data in an image for security or compliance purposes, you can use the Alibaba Cloud ECS image encryption function to protect your data privacy without the need to build, maintain, or protect your own key management infrastructure.

The Key Management Service \(KMS\) provides system generated CMKs and supports the BYOK model. Specifically, you can upload the key material to generate CMKs and host the CMKs in the KMS. Then, when you encrypt an image, you can choose the CMK provided by the system or use your own key.

Therefore, before you can use the ECS image encryption function for the first time \(either by using the ECS console or the API\), you must activate the [Key Management Service](https://www.alibabacloud.com/product/key-management-service). Additionally, if you use the CMK provided by the system, you also must activate access control for system operation permissions.

## Image encryption methods {#dependencies .section}

The following image encryption methods are supported:

-   Copy an unencrypted custom image to an unencrypted custom image.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136784/156644533141604_en-US.png)

    The image copying process does not change the encryption status of the target image.

-   Copy an unencrypted custom image to an encrypted custom image.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136784/156644533441606_en-US.png)

    The image copying process changes the encryption status of the target image. During the image copying process, you must provide a new encryption key. After encryption, you need to use this key to access the instance that is created by using the target image.

-   Copy an encrypted custom image to an encrypted custom image \(the key is not replaced\).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136784/156644533641607_en-US.png)

    The image copying process does not change the encryption status of the target image or replace the key. That is, the encrypted source image remains encrypted in the target image. In this case, you must use the original key to access the instance that is created by using the target image.

-   Copy an encrypted custom image to an encrypted custom image \(the key is replaced\).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/136784/156644533841608_en-US.png)

    The image copying process does not change the encryption status of the image, but replaces the key. This means that during the image copying process, you must provide a new encryption key. After encryption, you need to use this key to access the instance that is created by using the target image.


## Limits {#limits .section}

-   Only custom images are supported. Encrypted images cannot be copied into unencrypted images, copied across regions, shared, or exported.
-   If you use the CMK that is generated automatically by the system, the CMK cannot be deleted, but it can be retained free of charge.
-   ECS Bare Metal Instances \(X-Dragon\) are not supported.

## Billing {#section_r4l_5r5_q8y .section}

|Item|Billing|
|:---|:------|
|ECS image encryption|Free to use \(no fees are charged\).|
|CMKs created by ECS in each region|Free to use \(no fees are charged. Furthermore, ECS-created CMKs are not included in your quota of CMKs allowed for each region.|
|CMKs that you create on KMS|Such CMKs incur fees.|
|Image management operations, which are billed by the number of times that you call the KMS API in the corresponding region that exceed the quota \(regardless of whether you perform such management operations by using the ECS console or the API\)| Free to use \(no fees are charged\).

 |

Warning:

Make sure that your payment is successful. Otherwise, image encryption will fail and additional fees will be incurred.

## Encrypt an image by using the ECS console {#howtocreate .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
3.  In the top navigation bar, select a region.
4.  On the Custom Images tab page, select the target image, and then click **Copy Image**.

    **Note:** If the selected custom image is larger than 200 GiB, the system will prompt you to open a ticket when you click **Copy Image**.

5.  In the Copy Image dialog box, complete the following encryption settings:
    1.  Select the **Target Region**.
    2.  Enter the **Custom Image Name** and **Custom Image Description**.

        **Note:** By default, the description includes information about the source image, but can be modified accordingly.

    3.  Select **Encrypted** and select a key.

        You can select the CMK provided by the system or use your own key to encrypt or replace the key.

    4.  Click **OK**.

After, you can switch to the target region to check the copying progress of the custom image. When the progress is 100% completed, it means that the image is copied.

## Encrypt an image by using the API {#section_ern_2w4_xgb .section}

You can also call the [CopyImage](intl.en-US/API Reference/Images/CopyImage.md#) API to copy an image and specify the KMSKeyId to encrypt the image.

