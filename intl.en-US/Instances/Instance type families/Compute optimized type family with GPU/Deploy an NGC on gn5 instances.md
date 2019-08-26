# Deploy an NGC on gn5 instances {#concept_69102_zh .concept}

As a deep learning ecosystem from NVIDIA, NVIDIA GPU CLOUD \(NGC\) allows developers to access the deep learning software stack free of charge and is fit for creating a deep learning development environment.

At present, NGC has been fully deployed in the gn5 instances. Moreover, the image market also provides NGC container images optimized for NVIDIA Pascal GPU. By deploying NGC container images from the image market, developers can build an NGC container environment conveniently, and access optimized deep learning frameworks instantly, thus reducing the product development and business deployment time considerably. Other benefits include pre-installation of the development environment, support for optimized algorithm frameworks, and continuous updates.

The [NGC website](https://ngc.nvidia.com) provides images of different versions of the current mainstream deep learning frameworks \(such as Caffe, Caffe2, CNTK, MxNet, TensorFlow, Theano, and Torch\). You can select the desired image to build the environment. By taking the TensorFlow deep learning framework for example, this article describes how to build an NGC environment on gn5 instances.

Before building a TensorFlow environment, you must do the following:

-   Sign up with Alibaba Cloud and finish real-name registration.
-   Log on to the [NGC website](https://ngc.nvidia.com/signup/register) and create your NGC account.
-   Log on to the [NGC website](https://ngc.nvidia.com/signin/email), get the NGC API Key and save it locally. The NGC API Key will be verified when you log on to the NGC container environment.

## Procedure { .section}

1.  Create a gn5 instance by referring to [create an ECS instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). Pay attention to the following configurations:

    -   **Region**: Only China North 1, China North 2, China North 5, China East 1, China East 2, China South 1, Hong Kong, Asia Pacific SE 1 \(Singapore\), Asia Pacific SE 2 \(Sydney\), US West 1 \(Silicon Valley\), US East 1 \(Virginia\), and Germany 1 \(Frankfurt\) are available. 
    -   **Instance**: Select a gn5 instance type.
    -   **Image**: Select **Marketplace Image**. In the displayed dialog box, search for **NVIDIA GPU Cloud VM Image**, and then click **Continue**.
    -   **Network Billing Method**: Select **Assign Public IP**.

        **Note:** If you do not assign a public IP address here, you can bind an EIP address after the instance is created successfully.

    -   **Security Group**: Select a security group. Access to TCP port 22 must be allowed in the security group. If your instance needs to support HTTPS or [DIGITS 6](https://developer.nvidia.com/digits), access to TCP port 443 \(for HTTPS\) or TCP port 5000 \(for DIGITS 6\) must be allowed.
    After the ECS instance is created successfully, [log on to the ECS console](https://partners-intl.console.aliyun.com/#/ecs) and note down the public IP address of the instance.

2.  Connect to the ECS instance: Based on the logon credentials selected during instance creation, you can [connect to an ECS instance by using a password](../../../../../reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Linux instance by using a password.md#) or [connect to an ECS instance by using an SSH key pair](../../../../../reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Linux instance by using an SSH key pair.md#).
3.  Enter the NGC API Key obtained from the NGC website, and then press the Enter key to log on to the NGC container environment.

    ![Enter the NGC API Key](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310311904_en-US.png)

4.  Run `nvidia-smi`. You can view the information about the current GPU, including the GPU model, the driver version, and more, as shown below.

    ![Results of running nvidia-smi](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310311905_en-US.png)

5.  Follow the steps below to build the TensorFlow environment:
    1.  Log on to the [NGC website](https://ngc.nvidia.com/signin/email), go to the TensorFlow image page, and then get the `docker pull` command.

        ![TensorFlow mirror page](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310311906_en-US.png)

    2.  Download the TensorFlow image.

        ```language-bash
        docker pull nvcr.io/nvidia/tensorflow:18.03-py3
        
        ```

    3.  View the downloaded image.

        ```language-bash
        docker image ls
        
        ```

    4.  Run the container to deploy the TensorFlow development environment.

        ```language-bash
        nvidia-docker run --rm -it nvcr.io/nvidia/tensorflow:18.03-py3
        
        ```

        ![Run the container](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310311907_en-US.png)

6.  Test TensorFlow by using one of the following methods:
    -   Simple test of TensorFlow.

        ```language-bash
        $python
        
        ```

        ```language-python
        >>> import tensorflow as tf
        >>> hello = tf.constant('Hello, TensorFlow!')
        >>> sess = tf.Session()
        >>> sess.run(hello)
        
        ```

        If TensorFlow loads the GPU device correctly, the result is as shown below.

        ![Results of the simple test](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310311908_en-US.png)

    -   Download the TensorFlow model and test TensorFlow.

        ```language-bash
        git clone https://github.com/tensorflow/models.git
        cd models/tutorials/image/alexnet
        python alexnet_benchmark.py --batch_size 128 --num_batches 100
        
        ```

        The running status is as shown below.

        ![Model test](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9837/155107310411909_en-US.png)

7.  Save the changes made to the TensorFlow image. Otherwise, the configuration will be lost the next time you log on.

