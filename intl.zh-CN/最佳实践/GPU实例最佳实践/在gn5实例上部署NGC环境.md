# 在gn5实例上部署NGC环境 {#concept_69102_zh .task}

本文以搭建TensorFlow深度学习框架为例详细介绍如何在gn5实例上搭建NGC环境。

在开始搭建TensorFlow环境之前，您必须先完成以下工作：

-   注册阿里云账号，并完成实名认证。具体步骤，请参见[注册阿里云账号](https://www.alibabacloud.com/help/zh/doc-detail/42448.htm)和[实名认证](https://www.alibabacloud.com/help/zh/doc-detail/52595.htm) 。
-   登录[NGC网站](https://ngc.nvidia.com/signup/register)，注册NGC账号。
-   登录[NGC网站](https://ngc.nvidia.com/signin/email)，获取NGC API key并保存到本地。登录NGC容器环境时需要验证您的NGC API Key。

NGC（NVIDIA GPU CLOUD）是NVIDIA开发的一套深度学习生态系统，可以使开发者免费访问深度学习软件堆栈，建立适合深度学习的开发环境。

目前NGC在阿里云gn5实例作了全面部署，并且在镜像市场提供了针对NVIDIA Pascal GPU优化的NGC容器镜像。通过部署镜像市场的NGC容器镜像，开发者能简单快速地搭建NGC容器环境，即时访问优化后的深度学习框架，大大缩减产品开发以及业务部署的时间，实现开发环境的预安装；同时支持调优后的算法框架，并且保持持续更新。

[NGC网站](https://ngc.nvidia.com)提供了目前主流深度学习框架不同版本的镜像（例如Caffe、Caffe2、CNTK、MxNet、TensorFlow、Theano、Torch），您可以选择需要的镜像搭建环境。

1.  创建一台gn5实例。具体操作，请参见[创建ECS实例](../../../../intl.zh-CN/个人版快速入门/创建ECS实例.md#)。 在配置参数时，您需要注意以下几点：
    -   **地域**：只能选择华北1（青岛）、华北2（北京）、华北5（呼和浩特）、华东1（杭州）、华东2（上海）、华南1（深圳）、香港、新加坡、澳大利亚（悉尼）、美国（硅谷）、美国（弗吉尼亚）、德国（法兰克福）。
    -   **实例**：选择gn5实例规格。
    -   **镜像**：单击**镜像市场**，在弹出对话框里，找到**NVIDIA GPU Cloud VM Image**后，单击**使用**。

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/69102/cn_zh/1522653649466/%E9%80%89%E6%8B%A9%E9%95%9C%E5%83%8F.png)

    -   **公网带宽**：选择**分配公网IP地址**。

        **说明：** 如果这里没有分配公网IP地址，则在实例创建成功后，需要绑定EIP地址。

    -   **安全组**：选择一个安全组。安全组里必须开放 TCP 22 端口。如果您的实例需要支持HTTPS 或 DIGIT 6 服务，必须开放TCP 443（用于HTTPS）或TCP 5000（用于DIGITS 6）端口。
2.  连接ECS实例。 根据创建实例时选择的登录凭证选择以下任一方式连接ECS实例：
    -   [使用密码验证连接ECS实例](../../../../intl.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)
    -   [使用SSH密钥对验证连接ECS实例](../../../../intl.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md#)
3.  按界面提示输入NGC官网获取的NGC API Key后按回车键，即可登录NGC容器环境。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679926111904_zh-CN.png)

4.  运行`nvidia-smi`命令。 您能查看当前GPU的信息，包括GPU型号、驱动版本等，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679926411905_zh-CN.png)

5.  按以下步骤搭建TensorFlow环境。 
    1.  登录[NGC网站](https://ngc.nvidia.com/signin/email)，在TensorFlow镜像页面，获取`docker pull`命令。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679926411906_zh-CN.png)

    2.  下载TensorFlow镜像。 

        ``` {#codeblock_vbu_n2d_uno .language-bash}
        docker pull nvcr.io/nvidia/tensorflow:18.03-py3                    
        ```

    3.  查看下载的镜像。 

        ``` {#codeblock_y3m_v3i_tev .language-bash}
        docker image ls                   
        ```

    4.  运行容器，完成TensorFlow开发环境的部署。 

        ``` {#codeblock_7qv_6n8_td0 .language-bash}
        nvidia-docker run --rm -it nvcr.io/nvidia/tensorflow:18.03-py3              
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679926611907_zh-CN.png)

6.  选择以下任一种方式测试TensorFlow。 
    -   简单测试TensorFlow。

        ``` {#codeblock_28l_edd_gl0 .language-bash}
        $python
        ```

        ``` {#codeblock_o01_c2d_gbx .language-python}
        >>> import tensorflow as tf
        >>> hello = tf.constant('Hello, TensorFlow!')
        >>> sess = tf.Session()
        >>> sess.run(hello)
        ```

        如果TensorFlow正确加载了GPU设备，返回结果如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679926611908_zh-CN.png)

    -   下载TensorFlow模型并测试TensorFlow。

        ``` {#codeblock_44c_ovd_qkk .language-bash}
        git clone https://github.com/tensorflow/models.git
        cd models/tutorials/image/alexnet
        python alexnet_benchmark.py --batch_size 128 --num_batches 100
        						
        ```

        运行状态如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/156679927011909_zh-CN.png)

7.  保存TensorFlow镜像的修改。否则，下次登录时配置会丢失。

