# Install faascmd {#concept_blq_4qz_sfb .concept}

This topic describes how to download and install faascmd.

## Preparations {#section_rjw_wzz_sfb .section}

-   Perform the following steps on the instance for which you want to run faascmd:
    1.  Run the following command to check that the Python version is 2.7.x.

        ```
        python -V
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61535/154398719233505_en-US.png)

    2.  Install the Python module by running the following commands:

        ```
        pip -q install oss2
        pip -q install aliyun-python-sdk-core
        pip -q install aliyun-python-sdk-faas
        pip -q install aliyun-python-sdk-ram
        ```

    3.  Run the following command to check that the aliyun-python-sdk-core version is 2.11.0 or later.

        ```
        cat /usr/lib/python2.7/sitepackages/aliyunsdkcore/__init__.py
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61535/154398719233507_en-US.png)

        **Note:** If the version is earlier than 2.11.0, run `pip install --upgrade aliyun-python-sdk-core` to upgrade aliyun-python-sdk-core to the latest version.

-   [Obtain the AccessKeyID and AccessKeySecret of the RAM user.](../../../../intl.en-US/General Reference/Create an AccessKey.md#)

## Procedure {#section_b4w_yb1_tfb .section}

1.  Log on to your instance and run `wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/faascmd` in the current or any other directory to download faascmd.

    **Note:** When you [configure faascmd](intl.en-US/Best Practices/FaaS instances best practices/faascmd tool/Configure faascmd.md#), you need to add the absolute path of the directory where faascmd is installed to the PATH variable.

2.  Add executable permissions to faascmd by running the following command:

    ```
    chmod +x faascmd
    ```


