# 在GPU实例上使用RAPIDS加速机器学习任务 {#concept_262229 .concept}

本文介绍了如何在GPU实例上基于NGC环境使用RAPIDS加速库，加速数据科学和机器学习任务，提高计算资源的使用效率。

## 背景信息 {#section_koh_7rx_iga .section}

RAPIDS，全称Real-time Acceleration Platform for Integrated Data Science，是NVIDIA针对数据科学和机器学习推出的GPU加速库。更多RAPIDS信息请参见[官方网站](https://rapids.ai/)。

NGC，全称NVIDIA GPU CLOUD，是NVIDIA推出的一套深度学习生态系统，供开发者免费访问深度学习和机器学习软件堆栈，快速搭建相应的开发环境。[NGC网站](https://ngc.nvidia.com/)提供了RAPIDS的Docker镜像，预装了相关的开发环境。

JupyterLab是一套交互式的开发环境，帮助您高效地浏览、编辑和执行服务器上的代码文件。

Dask是一款轻量级大数据框架，可以提升并行计算效率。

本文提供了一套基于NVIDIA的RAPIDS Demo代码及数据集修改的示例代码，演示了在GPU实例上使用RAPIDS加速一个从ETL到ML Training端到端任务的过程。其中，ETL时使用RAPIDS的cuDF，ML Training时使用XGBoost。本文示例代码基于轻量级大数据框架Dask运行，为一套单机运行的代码。

**说明：** NVIDIA官方RAPIDS Demo代码请参见[Mortgage Demo](https://github.com/rapidsai/notebooks-contrib)。

RAPIDS预装镜像已经发布到阿里云镜像市场，创建GPU实例时，您可以在镜像市场中搜索NVIDIA RAPIDS并使用RAPIDS预装镜像。

**说明：** 该RAPIDS预装镜像使用Ubuntu 16.04 64-bit操作系统。

gn5优惠活动详情请参见[异构计算GPU实例活动页](https://promotion.aliyun.com/ntms/act/gpufreetier.html)。

## 前提条件 {#section_qz1_22r_qt8 .section}

-   注册阿里云账号并完成实名认证，请参见[阿里云账号注册流程](https://help.aliyun.com/knowledge_detail/37195.html)和[个人实名认证](https://help.aliyun.com/knowledge_detail/48263.html) 。
-   在[NGC注册页面](https://ngc.nvidia.com/signup/register)注册NGC账号。
-   获取NGC API Key。
    1.  登录[NGC网站](https://ngc.nvidia.com/signin/email)。
    2.  前往CONFIGURATION，单击**Get API Key**。
    3.  单击**Generate API Key**。
    4.  在Generate a New API Key中，单击**Confirm**。

        **说明：** 新的NGC API Key会覆盖旧的NGC API Key。如果您已持有NGC API Key，请确保不再需要旧的NGC API Key。

    5.  复制API Key并保存到本地。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533546989_zh-CN.png)


## 操作步骤 {#section_4st_emv_868 .section}

如果您创建GPU实例时使用了RAPIDS预装镜像，只需运行RAPIDS Demo，从[启动JupyterLab服务](#section_jlv_sqz_hzk)开始操作即可。

如果您创建GPU实例时没有使用RAPIDS预装镜像，按照以下步骤使用RAPIDS加速机器学习任务：

1.  [获取RAPIDS镜像下载命令](#section_6nn_fh6_3ro)。
2.  [部署RAPIDS环境](#section_4tf_rho_1gy)。
3.  [运行RAPIDS Demo](#section_jlv_sqz_hzk)。

## 步骤一：获取RAPIDS镜像下载命令 {#section_6nn_fh6_3ro .section}

1.  登录[NGC网站](https://ngc.nvidia.com/signin/email)。
2.  打开MACHINE LEARNING页面，单击**RAPIDS**镜像。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533546841_zh-CN.png)

3.  获取docker pull命令。

    本文示例代码基于RAPIDS 0.8版本镜像编写，因此在运行本示例代码时，使用Tag为0.8版本的镜像。实际操作时，请选择您匹配的版本。

    1.  选择Tags页签。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533747242_zh-CN.png)

    2.  找到并复制Tag信息。本示例中，选择`0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6`。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533747223_zh-CN.png)

    3.  返回页面顶部，复制**Pull Command**中的命令到文本编辑器，将镜像版本替换为对应的Tag信息，并保存。 本示例中，将`cuda9.2-runtime-ubuntu16.04`替换为`0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6`。

        保存的docker pull命令用于在[步骤二](#section_4tf_rho_1gy)中下载RAPIDS镜像。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533746842_zh-CN.png)


## 步骤二：部署RAPIDS环境 {#section_4tf_rho_1gy .section}

1.  创建一台GPU实例。

    详细步骤请参见[使用向导创建实例](../../../../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。

    -   **实例**：RAPIDS仅适用于特定的GPU型号（采用NVIDIA Pascal及以上架构），因此您需要选择GPU型号符合要求的实例规格，目前有gn6i、gn6v、gn5和gn5i，详细的GPU型号请参见[实例规格族](../../../../cn.zh-CN/实例/实例规格族.md#)。建议您选择显存更大的gn6i、gn6v或gn5实例。本示例中，选用了显存为16 GB的GPU实例。
    -   **镜像**：在镜像市场中搜索并使用`NVIDIA GPU Cloud VM Image`。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533846839_zh-CN.png)

    -   **公网带宽**：选择**分配公网IPv4地址**或者在实例创建成功后[绑定EIP地址](../../../../cn.zh-CN/网络/弹性网卡/绑定弹性网卡.md#)。
    -   **安全组**：选择的安全组需要开放以下端口：
        -   TCP 22 端口，用于SSH登录
        -   TCP 8888端口，用于支持访问JupyterLab服务
        -   TCP 8787端口、TCP 8786端口，用于支持访问Dask服务
2.  连接GPU实例。

    连接方式请参见[连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接方式导航.md#section_fjm_rgx_wdb)。

3.  输入NGC API Key后按回车键，登录NGC容器环境。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687533846840_zh-CN.png)

4.  （可选）运行nvidia-smi查看GPU型号、GPU驱动版本等GPU信息。

    建议您了解GPU信息，预判规避潜在问题。例如，如果NGC的驱动版本太低，新Docker镜像版本可能会不支持。

5.  运行在[步骤一](#section_6nn_fh6_3ro)中获取的docker pull命令下载RAPIDS镜像。

    ``` {#codeblock_rcd_vmp_ael}
    docker pull nvcr.io/nvidia/rapidsai/rapidsai:0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```

6.  （可选）查看下载的镜像。

    建议您查看Docker镜像信息，确保下载了正确的镜像。

    ``` {#codeblock_yj1_6j4_m5a}
    docker images
    ```

7.  运行容器部署RAPIDS环境。

    ``` {#codeblock_dej_q4v_i2t}
    docker run --runtime=nvidia \
            --rm -it \
            -p 8888:8888 \
            -p 8787:8787 \
            -p 8786:8786 \
            nvcr.io/nvidia/rapidsai/rapidsai:0.8-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```


## 步骤三：运行RAPIDS Demo {#section_jlv_sqz_hzk .section}

1.  在GPU实例上下载数据集和Demo文件。

    ``` {#codeblock_0rf_yf8_v2q}
    # Get apt source address and download demos.
    source_address=$(curl http://100.100.100.200/latest/meta-data/source-address|head -n 1)
    source_address="${source_address}/opsx/ecs/linux/binary/machine_learning/"
    cd /rapids
    wget $source_address/rapids_notebooks_v0.8.tar.gz
    tar -xzvf rapids_notebooks_v0.8.tar.gz
    cd /rapids/rapids_notebooks_v0.8/xgboost
    wget $source_address/data/mortgage/mortgage_2000_1gb.tgz
    ```

2.  在GPU实例上启动JupyterLab服务。

    推荐直接使用命令启动。

    ``` {#codeblock_c8o_gs1_8lq}
    # Run the following command to start JupyterLab and set the password.
    cd /rapids/rapids_notebooks_v0.8/xgboost
    jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token='YOUR PASSWORD'
    # Exit JupyterLab.
    sh ../utils/stop-jupyter.sh
    ```

    -   除使用命令外，您也可以执行脚本`sh ../utils/start-jupyter.sh`启动jupyter-lab，此时无法设置登录密码。
    -   您也可以连续按两次`Ctrl+C`退出JupyterLab服务。
3.  打开浏览器，在地址栏输入`http://您的GPU实例IP地址:8888`远程访问JupyterLab 。

    **说明：** 推荐使用Chrome浏览器。

    如果您在启动JupyterLab服务时设置了登录密码，会跳转到密码输入界面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534146852_zh-CN.png)

4.  运行NoteBook代码。

    该案例是一个抵押贷款回归的任务，详细信息请参见[代码执行过程](#section_88w_0mw_i43)。登录成功后，可以看到NoteBook代码的代码包括以下内容：

    -   xgboost\_E2E.ipynb文件： XGBoost Demo文件。双击文件可以查看文件详情，单击下图中的执行按钮可以逐步执行代码，每次执行一个Cell。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534346845_zh-CN.png)

    -   mortgage\_2000\_1gb.tgz文件： 2000年的抵押贷款回归训练数据（1G分割的perf文件夹下的文件不会大于1G，使用1G分割的数据可以更有效的利用GPU显存）。

## 代码执行过程 {#section_88w_0mw_i43 .section}

该案例基于XGBoost演示了数据预处理到训练的端到端的过程，主要分为三个阶段：

-   ETL（Extract-Transform-Load）：主要在GPU实例上进行。将业务系统的数据经过抽取、清洗转换之后加载到数据仓库。
-   Data Conversion：在GPU实例上进行。将在ETL阶段处理过的数据转换为用于XGBoost训练的DMatrix格式。
-   ML-Training：默认在GPU实例上进行。使用XGBoost训练梯度提升决策树 。

NoteBook代码的执行过程如下：

1.  准备数据集。

    本案例的Shell脚本会默认下载2000年的抵押贷款回归训练数据（mortgage\_2000\_1gb.tgz）。

    如果您想获取更多数据用于XGBoost模型训练，可以设定参数download\_url指定下载路径，具体下载地址请参见[Mortgage Data](https://docs.rapids.ai/datasets/mortgage-data)。

    示例效果如下 ：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534446846_zh-CN.png)

2.  设定相关参数。

    |参数名称|说明|
    |----|--|
    |start\_year|指定选择训练数据的起始时间，ETL时会处理start\_year到end\_year之间的数据。|
    |end\_year|指定选择训练数据的结束时间，ETL时会处理start\_year到end\_year之间的数据。|
    |train\_with\_gpu|是否使用GPU进行XGBoost模型训练，默认为True。|
    |gpu\_count|指定启动worker的数量，默认为1。您可以按需要设定参数值，但不能超出GPU实例的GPU数量。|
    |part\_count|指定用于模型训练的performance文件的数量，默认为 2 \* gpu\_count。如果参数值过大，在Data Conversion阶段会报错超出GPU内存限制，错误信息会在NoteBook后台输出。|

    示例效果如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534546847_zh-CN.png)

3.  启动Dask服务。

    代码会启动Dask Scheduler，并根据gpu\_count参数启动worker用于ETL和模型训练。启动Dask服务后，您也可以通过Dask Dashboard直观地监控任务，打开方法请参见[Dask Dashboard](#section_x15_g1t_2f7)。

    示例效果如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534746848_zh-CN.png)

4.  启动ETL。

    ETL阶段会进行到表关联、分组、聚合、切片等操作，数据格式采用cuDF库的DataFrame格式（类似于pandas的DataFrame格式）。

    示例效果如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687534846849_zh-CN.png)

5.  启动Data Conversion。

    将DataFrame格式的数据转换为用于XGBoost训练的DMatrix格式，每个worker处理一个DMatrix对象。

    示例效果如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687535146850_zh-CN.png)

6.  启动ML Training。

    使用dask-xgboost启动模型训练，dask-xgboost负责多个dask worker间的通信协同工作，底层仍然调用xgboost执行模型训练。

    示例效果如下：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/156687535646851_zh-CN.png)


## Dask Dashboard {#section_x15_g1t_2f7 .section}

Dask Dashboard支持任务进度跟踪、任务性能问题识别和故障调试。

Dask服务启动后，在浏览器地址栏中访问`http://您的GPU实例IP地址:8787/status`即可进入Dashboard主界面。

![](images/57733_zh-CN.gif)

## 相关函数 {#section_whh_v8f_nnc .section}

|函数功能|函数名称|
|----|----|
|下载文件|def download\_file\_from\_url\(url, filename\):|
|解压文件|def decompress\_file\(filename, path\):|
|获取当前机器的GPU个数|def get\_gpu\_nums\(\):|
|管理GPU内存| -   def initialize\_rmm\_pool\(\):
-   def initialize\_rmm\_no\_pool\(\):
-   def run\_dask\_task\(func, \*\*kwargs\):

 |
|提交DASK任务| -   def process\_quarter\_gpu\(year=2000, quarter=1, perf\_file=""\):
-   def run\_gpu\_workflow\(quarter=1, year=2000, perf\_file="", \*\*kwargs\):

 |
|使用cuDF从CSV中加载数据| -   def gpu\_load\_performance\_csv\(performance\_path, \*\*kwargs\):
-   def gpu\_load\_acquisition\_csv\(acquisition\_path, \*\*kwargs\):
-   def gpu\_load\_names\(\*\*kwargs\):

 |
|处理和提取训练数据的特征| -   def null\_workaround\(df, \*\*kwargs\):
-   def create\_ever\_features\(gdf, \*\*kwargs\):
-   def join\_ever\_delinq\_features\(everdf\_tmp, delinq\_merge, \*\*kwargs\):
-   def create\_joined\_df\(gdf, everdf, \*\*kwargs\):
-   def create\_12\_mon\_features\(joined\_df, \*\*kwargs\):
-   def combine\_joined\_12\_mon\(joined\_df, testdf, \*\*kwargs\):
-   def final\_performance\_delinquency\(gdf, joined\_df, \*\*kwargs\):
-   def join\_perf\_acq\_gdfs\(perf, acq, \*\*kwargs\):
-   def last\_mile\_cleaning\(df, \*\*kwargs\):

 |

## 更多信息 {#section_2v1_q0o_h4k .section}

GPU实例和RAPIDS组合适用于加速更多类型的任务，请参见[在GPU实例上使用RAPIDS加速图像搜索任务](cn.zh-CN/最佳实践/GPU实例最佳实践/在GPU实例上使用RAPIDS加速图像搜索任务.md#)。

