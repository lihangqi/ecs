# 在gn5实例上部署NGC环境 {#concept_69102_zh .concept}

本文以搭建TensorFlow深度学习框架为例详细介绍如何在gn5实例上搭建NGC环境。

## 背景信息 {#section_bhf_f4l_qgb .section}

NGC（NVIDIA GPU CLOUD）是NVIDIA开发的一套深度学习生态系统，可以使开发者免费访问深度学习软件堆栈，建立适合深度学习的开发环境。

目前NGC在阿里云gn5实例作了全面部署，并且在镜像市场提供了针对NVIDIA Pascal GPU优化的NGC容器镜像。通过部署镜像市场的NGC容器镜像，开发者能简单快速地搭建NGC容器环境，即时访问优化后的深度学习框架，大大缩减产品开发以及业务部署的时间，实现开发环境的预安装；同时支持调优后的算法框架，并且保持持续更新。

 [NGC网站](https://ngc.nvidia.com) 提供了目前主流深度学习框架不同版本的镜像（比如Caffe、Caffe2、CNTK、MxNet、TensorFlow、Theano、Torch），您可以选择需要的镜像搭建环境。

## 前提条件 {#section_wjx_fq5_qgb .section}

在开始搭建TensorFlow环境之前，必须先完成以下工作：

-    [注册阿里云账号](https://www.alibabacloud.com/help/zh/doc-detail/42448.htm)，并完成 [实名认证](https://www.alibabacloud.com/help/zh/doc-detail/52595.htm) 。
-   登录 [NGC网站](https://ngc.nvidia.com/signup/register)，注册NGC账号。
-   登录 [NGC网站](https://ngc.nvidia.com/signin/email)，获取NGC API key并保存到本地。登录NGC容器环境时需要验证您的NGC API Key。

## 操作步骤 {#section_lfd_ztk_ngb .section}

1.  创建gn5实例。参考 [创建ECS实例](../../../../../intl.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#) 创建一台gn5实例，注意以下配置信息：

    -   **地域**：只能选择 华北1、华北2、华北5、华东1、华东2、华南1、香港、亚太东南1（新加坡）、亚太东南2（悉尼）、美国西部1（硅谷）、美国东部1（弗吉尼亚）、欧洲中部1（法兰克福）。 
    -   **实例**：选择gn5实例规格。
    -   **镜像**：单击 **镜像市场**，在弹出对话框里，找到 **NVIDIA GPU Cloud VM Image** 后，单击 **使用**。

        ![NVIDIA GPU Cloud镜像](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/69102/cn_zh/1522653649466/%E9%80%89%E6%8B%A9%E9%95%9C%E5%83%8F.png)

    -   **公网带宽**：选择 **分配公网IP地址**。

        **说明：** 如果这里不分配公网IP地址，则在实例创建成功后，绑定EIP地址。

    -   **安全组**：选择一个安全组。安全组里必须开放 TCP 22 端口。如果您的实例需要支持HTTPS或 [DIGITS 6](https://developer.nvidia.com/digits) 服务，必须开放TCP 443（用于HTTPS）或TCP 5000（用于DIGITS 6）端口。
    ECS实例创建成功后，[登录ECS管理控制台](https://ecs.console.aliyun.com/#/home)，记录实例的公网IP地址。

2.  连接ECS实例：根据创建实例时选择的登录凭证，[使用密码验证连接ECS实例](../../../../../intl.zh-CN/实例/实例生命周期/连接实例/使用用户名密码验证连接Linux实例.md#) 或者 [使用SSH密钥对验证连接ECS实例](../../../../../intl.zh-CN/实例/实例生命周期/连接实例/使用SSH密钥对连接Linux实例.md#) 。
3.  按界面提示输入NGC官网获取的NGC API Key后按回车键，即可登录NGC容器环境。

    ![输入NGC API Key](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309511904_zh-CN.png)

4.  运行 `nvidia-smi`。您能查看当前GPU的信息，包括GPU型号、驱动版本等，如下图所示。

    ![nvidia-smi运行结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309511905_zh-CN.png)

5.  按以下步骤搭建TensorFlow环境：
    1.  登录 [NGC网站](https://ngc.nvidia.com/signin/email)，找到TensorFlow镜像页面，获取 `docker pull` 命令。

        ![TensorFlow镜像页面](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309511906_zh-CN.png)

    2.  下载TensorFlow镜像。

        ```language-bash
        docker pull nvcr.io/nvidia/tensorflow:18.03-py3
        
        ```

    3.  查看下载的镜像。

        ```language-bash
        docker image ls
        
        ```

    4.  运行容器，完成TensorFlow开发环境的部署。

        ```language-bash
        nvidia-docker run --rm -it nvcr.io/nvidia/tensorflow:18.03-py3
        
        ```

        ![运行容器](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309511907_zh-CN.png)

6.  选择以下任一种方式测试TensorFlow：
    -   简单测试TensorFlow。

        ```language-bash
        $python
        
        ```

        ```language-python
        >>> import tensorflow as tf
        >>> hello = tf.constant('Hello, TensorFlow!')
        >>> sess = tf.Session()
        >>> sess.run(hello)
        
        ```

        如果TensorFlow正确加载了GPU设备，返回结果如下图所示。

        ![简单测试结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309611908_zh-CN.png)

    -   下载TensorFlow模型并测试TensorFlow。

        ```language-bash
        git clone https://github.com/tensorflow/models.git
        cd models/tutorials/image/alexnet
        python alexnet_benchmark.py --batch_size 128 --num_batches 100
        
        ```

        运行状态如下图所示。

        ![模型测试](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107309611909_zh-CN.png)

7.  保存TensorFlow镜像的修改。否则，下次登录时配置会丢失。

