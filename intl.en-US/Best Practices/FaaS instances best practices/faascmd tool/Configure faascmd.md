# Configure faascmd {#task_ny2_wqz_sfb .task}

Before using faascmd, you need to configure the related environment variable and the AccessKey of the RAM user.

1.  Log on to your instance and configure the PATH environment variable by running the following command: 

    ```
    export PATH=$PATH:<path where faascmd is located>
    ```

2.  Configure the AccessKey \(that is, the AccessKeyId and AccessKeySecret\) by running the following command: 

    ```
    faascmd config --id=<yourAccessKeyID> --key=<yourAccessKeySecret>
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61538/154398723130983_en-US.png)


