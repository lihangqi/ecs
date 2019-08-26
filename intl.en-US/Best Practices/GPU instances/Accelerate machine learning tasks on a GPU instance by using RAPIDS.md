# Accelerate machine learning tasks on a GPU instance by using RAPIDS {#concept_262229 .concept}

This topic describes how to use RAPIDS libraries \(based on the NGC environment\) that are installed on a GPU instance to accelerate tasks for data science and machine learning and improve the efficiency of computing resources.

## Background information {#section_koh_7rx_iga .section}

The following concepts are used in the example provided in this topic:

-   Real-time Acceleration Platform for Integrated Data Science \(RAPIDS\) is a software suite of GPU acceleration libraries developed by NVIDIA for data science and machine learning. For more information, visit [RAPIDS website](https://rapids.ai/).
-   NVIDIA GPU Cloud \(NGC\) is a deep learning ecosystem developed by NVIDIA to provide developers with free access to deep learning and machine learning software stacks that allows them to quickly build corresponding environments. The [NGC website](https://ngc.nvidia.com/) provides RAPIDS Docker images, which come with pre-installed environments.
-   JupyterLab is an interactive development environment that helps you browse, edit, and run code files on your servers.
-   Dask is a lightweight big data frame that can improve the efficiency of parallel computing.
-   In the example provided in this topic, modified code that is based on the NVIDIA RAPIDS Demo and corresponding dataset is provided to demonstrate how to use RAPIDS to accelerate an end-to-end task from ETL to ML Training on a GPU instance. The cuDF library of RAPIDS is used in the Extract-Transform-Load \(ETL\) phase whereas the XGBoost model is used in the ML Training phase. The example code is based on the Dask frame and runs on a single machine.

**Note:** To obtain the official RAPIDS Demo code of NVIDIA, see [Mortgage Demo](https://github.com/rapidsai/notebooks).

## Preparations {#section_qz1_22r_qt8 .section}

-   Register an Alibaba Cloud account and complete the real-name verification.
-   Go to the [NGC registration page](https://ngc.nvidia.com/signup/register) and register an account.
-   Obtain an NGC API Key by following these steps:
    1.  Log on to the [NGC website](https://ngc.nvidia.com/signin/email).
    2.  Go to the CONFIGURATION page, and then click **Get API Key**.
    3.  Click **Generate API Key**.
    4.  In the displayed dialog box, click **Confirm**.

        **Note:** A new NGC API Key overwrites any previous API key. Before you generate a new API Key, you must make sure that the previous API key is no longer being used.

    5.  Copy the API Key to your local disk.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027246989_en-US.png)


## Procedure 1: Obtain the RAPIDS image download command {#section_6nn_fh6_3ro .section}

1.  Log on to the [NGC website](https://ngc.nvidia.com/signin/email).
2.  Go to the MACHINE LEARNING page, and then click the **RAPIDS** image.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346841_en-US.png)

3.  Obtain the docker pull command.

    The example code in this topic is based on the RAPIDS v0.6 image. Note that if you use another image, the corresponding command may differ.

    1.  Click the Tags tab.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027347242_en-US.png)

    2.  Locate and copy the Tag information. In this example, select `0.6-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6`. Then, open a text editor and paste the Tag information.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027347223_en-US.png)

    3.  Find the **Pull Command** area and copy the displayed command. Then, paste the command to the text editor. After that, replace the image version with the Tag information from the preceding step, and save the TXT file. In this example, replace `cuda9.2-runtime-ubuntu16.04` with `0.6-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6`.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346842_en-US.png)


## Procedure 2: Deploy the RAPIDS environment {#section_4tf_rho_1gy .section}

1.  Create a GPU instance.

    For more information, see [Create an instance by using the wizard](../../../../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).

    -   **Instance Type**: RAPIDS can only be deployed on GPU instances that use NVIDIA Pascal or a later architecture. Currently, you can select the following instance types: gn6i, gn6v, gn5, and gn5i. For more information, see [Instance type families](../../../../reseller.en-US/Instances/Instance type families.md#). We recommend that you select an instance type that has a larger memory, such as gn6i, gn6v, and gn5. In this example, select the GPU instance that has a 16 GB memory.
    -   **Image**: In this example, use the `NVIDIA GPU Cloud VM Image`.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346839_en-US.png)

    -   **Network Billing Method**: Select **Assign public IP**, or [Attach an ENI](../../../../reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#) after you create a GPU instance.
    -   **Security Group**: Select a security group that enables the following ports:
        -   TCP port 22, which is used to enable logon through SSH
        -   TCP port 8888, which is used to access JupyterLab
        -   TCP port 8786 and TCP port 8787, which are used to access Dask
2.  Connect to the GPU instance.

    For more information, see [Connect to a Linux instance](../../../../reseller.en-US/Instances/Connect to instances/Overview.md#section_fjm_rgx_wdb).

3.  Enter the NGC API Key and press **Enter** to log on to the NGC container.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346840_en-US.png)

4.  Optional. Run the nvidia-smi command to view GPU information, such as GPU model and GPU driver version.

    We recommend that you check the GPU information to identify any potential issues. For example, if an earlier NGC driver version is used, it may not be supported by the target Docker image.

5.  Run the docker pull command obtained in [Procedure 1: Obtain the RAPIDS image download command](#section_6nn_fh6_3ro) to download the RAPIDS image.

    ``` {#codeblock_rcd_vmp_ael}
    docker pull nvcr.io/nvidia/rapidsai/rapidsai:0.6-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```

6.  Optional. Check the information of the downloaded image to ensure that the correct image is downloaded.

    ``` {#codeblock_yj1_6j4_m5a}
    docker images
    ```

7.  Run the NGC container to deploy the RAPIDS environment.

    ``` {#codeblock_dej_q4v_i2t}
    docker run --runtime=nvidia \
            --rm -it \
            -p 8888:8888 \
            -p 8787:8787 \
            -p 8786:8786 \
            nvcr.io/nvidia/rapidsai/rapidsai:0.6-cuda10.0-runtime-ubuntu16.04-gcc5-py3.6
    ```


## Procedure 3: Run RAPIDS Demo {#section_jlv_sqz_hzk .section}

1.  On the GPU instance, download the dataset and the Demo file.

    ``` {#codeblock_0rf_yf8_v2q}
    # Obtain the apt source address and download the script (used to download training data, notebook, and utils).
    $ source_address=$(curl http://100.100.100.200/latest/meta-data/source-address|head -n 1)
    $ source_address="${source_address}/opsx/ecs/linux/binary/machine_learning/"
    $ wget $source_address/rapids_notebooks_v0.6/utils/download_v0.6.sh
    # Run the downloaded script.
    $ sh ./download_v0.6.sh
    # Go to the download directory to view the downloaded file.
    $ apt update
    $ apt install tree
    $ tree /rapids/rapids_notebooks_v0.6/
    ```

    We recommend that you check the downloaded file contains five folders and 16 files.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346844_en-US.png)

2.  Start JupyterLab on the GPU instance by running the following commands:

    ``` {#codeblock_c8o_gs1_8lq}
    # Go to the working directory.
    $ cd /rapids/rapids_notebooks_v0.6/xgboost
    # Run the following command to start JupyterLab and set the logon password:
    $ jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token='logon password'
    # Exit.
    $ sh ../utils/stop-jupyter.sh
    ```

    You can also run the `$ sh ../utils/start-jupyter.sh` script to start JupyterLab. However you cannot set the logon password if you run the script. To exit, press Ctrl+C twice.

3.  Open your browser and enter `http://IP address of your GPU instance:8888` to access JupyterLab. If a password for JupyterLab is set, you need to enter the password as prompted.

    **Note:** We recommend that you use Google Chrome.

    If you set the logon password when you start JupyterLab, you will be prompted to enter your password.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346852_en-US.png)

4.  Run the NoteBook code.

    Log on to JupyterLab and view the NoteBook code. A mortgage repayment task is used in this example. For more information, see [Code running process](#section_88w_0mw_i43). Details of the example code include:

    -   A folder named mortgage\_2000\_1gb that contains decompressed training data. Specifically, this folder contains the acq folder, perf folder and names.csv file.
    -   A file named xgboost\_E2E.ipynb, which is an XGBoost Demo file. You can double-click this file to view its details, or click the **Execute** button to execute one cell at a time.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346845_en-US.png)

    -   A file named mortgage\_2000\_1gb.tgz, which contains the mortgage repayment training data of the year 2000 \(files in the perf folder are split into 1 GB sizes, namely, each file is no larger than 1 GB. This method helps utilize the GPU memory more efficiently\).

## Code running process {#section_88w_0mw_i43 .section}

In this example, XGBoost is used to demonstrate the end-to-end code running process from data pre-processing to training the XGBoost data model. The process involves the following three phases:

-   ETL \(Extract-Transform-Load\), which is completed on the GPU instance to extract and transform the data and then load the data to the data warehouse.
-   Data Conversion, which is completed on the GPU instance to convert the data processed in the ETL phase into DMatrix-format data so that XGBoost can be used to train the data model.
-   ML-Training, which is completed on the GPU instance by default so that the XGBoost training gradient boosting decision tree \(GBDT\) is used.

The NoteBook code is run as follows:

1.  Prepare the dataset.

    In this example, the Shell script downloads the mortgage repayment training data \(mortgage\_2000\_1gb.tgz\) and decompress the data to the mortgage\_2000\_1gb file.

    If you want to obtain more data for XGBoost model training, you can set the download\_url parameter to specify the required URL. For more information, see [Mortgage Data](https://docs.rapids.ai/datasets/mortgage-data).

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346846_en-US.png)

2.  Set one or more parameters as needed.

    |Parameter|Description|
    |---------|-----------|
    |start\_year|Specify the start year from which training data is selected. In the ETL phase, data generated between the start\_year and the end\_year is processed.|
    |end\_year|Specify the end year from which training data is selected. In the ETL phase, data generated between the start\_year and end\_year is processed.|
    |train\_with\_gpu|Set whether to use GPU for XGBoost model training. Default value: True.|
    |gpu\_count|Specify the number of workers to be started. Default value: 1. You can set the parameter to a value that is less than the number of GPUs in the GPU instance.|
    |part\_count|Specify the number of performance files used for data model training. Default value: 2 × gpu\_count. If the value is too large, an insufficient memory error occurs in Data Conversion phase and an error message is displayed on the backend of NoteBook.|

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027346847_en-US.png)

3.  Start Dask.

    The NoteBook code starts Dask Scheduler, and also starts workers according to the setting of the gpu\_count parameter for ETL and data model training.

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027446848_en-US.png)

4.  Start the ETL phase.

    In this phase, tables are associated, grouped, integrated, and split. The data format is DataFrame of the cuDF library \(similar to DataFrame of pandas\).

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027446849_en-US.png)

5.  Start the Data Conversion phase.

    In this phase, DataFrame-format data is converted into DMatrix-format data for XGBoost model training. Each worker processes one DMatrix object.

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027446850_en-US.png)

6.  Start the ML Training phase.

    In this phase, data model training is started by dask-xgboost, which supports collaborative communication among Dask workers. On the bottom layer, dask-xgboost is also called to execute data model training.

    The following figure shows an example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/216663/155928027446851_en-US.png)


## Related functions {#section_whh_v8f_nnc .section}

|Operation|Function name|
|---------|-------------|
|Download a file.|def download\_file\_from\_url\(url, filename\):|
|Decompress a file.|def decompress\_file\(filename, path\):|
|Obtain the number of GPUs in the current machine.|def get\_gpu\_nums\(\):|
|Manage the GPU memory.| -   def initialize\_rmm\_pool\(\):
-   def initialize\_rmm\_no\_pool\(\):
-   def run\_dask\_task\(func, \*\*kwargs\):

 |
|Submit a Dask task.| -   def process\_quarter\_gpu\(year=2000, quarter=1, perf\_file=""\):
-   def run\_gpu\_workflow\(quarter=1, year=2000, perf\_file="", \*\*kwargs\):

 |
|Use cuDF to load data from a CSV file.| -   def gpu\_load\_performance\_csv\(performance\_path, \*\*kwargs\):
-   def gpu\_load\_acquisition\_csv\(acquisition\_path, \*\*kwargs\):
-   def gpu\_load\_names\(\*\*kwargs\):

 |
|Process and extract characteristics of data for training machine learning models.| -   def null\_workaround\(df, \*\*kwargs\):
-   def create\_ever\_features\(gdf, \*\*kwargs\):
-   def join\_ever\_delinq\_features\(everdf\_tmp, delinq\_merge, \*\*kwargs\):
-   def create\_joined\_df\(gdf, everdf, \*\*kwargs\):
-   def create\_12\_mon\_features\(joined\_df, \*\*kwargs\):
-   def combine\_joined\_12\_mon\(joined\_df, testdf, \*\*kwargs\):
-   def final\_performance\_delinquency\(gdf, joined\_df, \*\*kwargs\):
-   def join\_perf\_acq\_gdfs\(perf, acq, \*\*kwargs\):
-   def last\_mile\_cleaning\(df, \*\*kwargs\):

 |

