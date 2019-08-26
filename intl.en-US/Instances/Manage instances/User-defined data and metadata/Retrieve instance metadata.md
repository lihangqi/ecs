# Retrieve instance metadata {#concept_dwj_y1x_wgb .concept}

This topic describes how to retrieve the metadata of a Linux or Windows instance.

## Limits {#section_udb_rj4_xdb .section}

Only the metadata of a VPC instance can be obtained.

**Note:** Manually changing instance information will not change the relevant metadata.

## Retrieve the metadata of a Linux instance {#section_akf_lwh_1gb .section}

1.  Connect to your Linux instance. For more information, see [Overview of connecting to an ECS instance](reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Run the following command to access the root directory of the metadata.

    ```
    curl http://100.100.100.200/latest/meta-data/
    ```

3.  Add a specific metadata name to the preceding command to access the specified metadata. For more information, see [Instance metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#section_yjf_jk4_xdb) and [Dynamic instance metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#section_uww_nvm_hfb). For example:
    -   Run the following command to get the ID of an ECS instance.

        ```
        curl http://100.100.100.200/latest/meta-data/instance-id
        ```

    -   Run the following command to get the image ID of an ECS instance.

        ```
        curl http://100.100.100.200/latest/meta-data/image-id
        ```

    -   Run the following command to get the active system events.

        ```
        curl http://100.100.100.200/latest/maintenance/active-system-events
        ```

    -   Run the following command to get the instance identity document.

        ```
        curl http://100.100.100.200/latest/dynamic/instance-identity/document
        ```

    -   Run the following command to get the instance user data.

        ```
        curl http://100.100.100.200/latest/user-data
        ```


## Retrieve the metadata of a Windows instance {#section_ejx_tj4_xdb .section}

1.  Connect to your Windows instance. For more information, see [Overview of connecting to an ECS instance](reseller.en-US/Instances/Connect to instances/Overview.md#).
2.  Run the following command by using PowerShell to get instance metadata.

    ```
    Invoke-RestMethod http://100.100.100.200/latest/meta-data/
    ```

3.  Add a specific metadata name to the preceding command to access the specified metadata. For more information, see [Instance metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#section_yjf_jk4_xdb) and [Dynamic instance metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#section_uww_nvm_hfb). For example:
    -   Run the following command to get the ID of an ECS instance.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/meta-data/instance-id
        ```

    -   Run the following command to get the image ID of an ECS instance.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/meta-data/image-id
        ```

    -   Run the following command to get the active system events.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/maintenance/active-system-events
        ```

    -   Run the following command to get the instance identity document.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/dynamic/instance-identity/document
        ```

    -   Run the following command to get the instance user data.

        ```
        Invoke-RestMethod http://100.100.100.200/latest/user-data
        ```


