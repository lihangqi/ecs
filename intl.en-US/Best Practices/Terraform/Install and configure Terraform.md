# Install and configure Terraform {#task_bts_tlz_dfb .task}

This article describes how to install Terraform.

1.  Go to the [Terraform website](https://www.terraform.io/downloads.html) to download the package for your operating system. 
2.  Decompress the package to /usr/local/bin. If you decompress the executable file to another directory, define a global path for the file as follows:
    -   Linux: See [How to define a global path on Linux](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix).
    -   Windows: See [How to define a global path on Windows](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).
    -   Mac: See [How to define a global path on Mac](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix).
3.  Run the `terraform`command to verify the path. 

    A list of available Terraform options is displayed as follows, indicating that the installation is completed.

    ```
    username:~$ terraform
    Usage: terraform [-version] [-help] <command> [args]
    ```

4.  For higher flexibility and security of rights management, it is recommended that you create and authorize a RAM user. 
    1.  Log on to the [RAM console](https://ram.console.aliyun.com/#/overview).
    2.  Create a RAM user named Terraform and create an AccessKey for the user. For detailed steps, see [Create a RAM user](../../../../reseller.en-US/Quick Start/Create a RAM user.md#).
    3.  Authorize the RAM user. In this example, the user Terraform is granted the `AliyunECSFullAccess` and `AliyunVPCFullAccess` permissions. For detailed steps, see [Attach policies to a RAM user](../../../../reseller.en-US/Quick Start/Attach policies to a RAM user.md#).
5.  Create an environment variable to store identity authentication information. 

    ```
    export ALICLOUD_ACCESS_KEY="LTAIUrZCw3********"
    export ALICLOUD_SECRET_KEY="zfwwWAMWIAiooj14GQ2*************"
    export ALICLOUD_REGION="cn-beijing"
    ```


