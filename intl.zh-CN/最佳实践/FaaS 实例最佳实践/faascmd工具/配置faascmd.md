# 配置faascmd {#task_ny2_wqz_sfb .task}

在使用faascmd之前，您需要配置相关环境变量和RAM用户的AccessKey。

1.  登录您的实例后，运行以下命令配置PATH环境变量。 

    ```
    export PATH=$PATH:<faascmd工具所在路径>
    ```

2.  运行下列命令配置AccessKey ID和AccessKey Secret。 

    ```
    faascmd config --id=<yourAccessKeyID> --key=<yourAccessKeySecret>
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61538/154398722830983_zh-CN.png)


