# 安装SGX {#concept_rw4_1wz_wgb .task}

本文介绍SGX的原理，并给出了安装说明。

英特尔 SGX（Intel Software Guard Extension）是英特尔指令集架构的一个扩展。SGX为您提供了围圈（Enclave），即内存中一个加密的可信执行区域，由CPU保护您的数据和隐私不被恶意代码窃取。

SGX利用新增的处理器指令，在内存中分配一部分区域 EPC（Enclave Page Cache），通过CPU内的加密引擎MEE（Memory Encryption Engine）对其中的数据进行加密。EPC中加密的内容只有进入CPU后才会被解密成明文。因此，在SGX中，您可以不信任操作系统、VMM、甚至 BIOS，只需要信任CPU便能确保隐私数据不会泄漏。

实际应用中，您可以把隐私数据加密后以密文形式传递至云上的围圈中，并通过远程证明把对应的秘钥也传入围圈。然后在CPU的加密保护下利用数据进行运算，结果会以密文形式返回给您。这种模式下，您既可以利用云计算强大的计算力，又不用担心数据泄漏。

![安装SGX-SGX架构](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123390/156689981538658_zh-CN.png)

EDL（Enclave Definition Language）是SGX编程的核心，其中定义了所有围圈里对外读写、处理数据的函数。在编译阶段，SDK提供的Edger8r 工具会根据EDL中定义的函数生成围圈和普通内存的桥接函数，并做相应的安全检测。

函数分为信任函数（ecall）和不可信函数（ocall）：

-   ecall：定义在信任区域（trusted），在围圈外被调用，并在围圈内执行。
-   ocall：定义在不可信区域（untrusted），在围圈内被调用，并在围圈外执行。

``` {#codeblock_r93_a9s_pus}
// demo.edl
enclave {
        // Add your definition of "secret_t" here
        trusted {
                 public void get_secret([out] secret_t* secret);
        };
        untrusted {
        // This OCALL is for illustration purposes only.
        // It should not be used in a real enclave,
        // unless it is during the development phase
        // for debugging purposes.
        void dump_secret([in] const secret_t* secret);
        };
};
```

## 以安装文件方式安装SGX {#section_nsr_pws_qgb .section}

需要先安装对应Linux内核版本的头文件，安装SGX时包括驱动、PSW、SDK等组件。

**说明：** 样例中的 Makefile 默认安装目录是/opt/intel/。

1.  下载适用SGX版本的安装文件。下载链接为[SGX](https://01.org/intel-software-guard-extensions/downloads)。
2.  安装SGX。具体安装步骤，请参见[安装指南](https://download.01.org/intel-sgx/linux-2.0/docs/Intel_SGX_Installation_Guide_Linux_2.0_Open_Source.pdf)。

## 以源代码方式安装 SGX {#section_cyz_rws_qgb .section}

需要先安装对应 Linux 内核版本的头文件，安装SGX时包括驱动、PSW、SDK 等组件。

**说明：** 样例中的 Makefile 默认安装目录是/opt/intel/。

1.  从[官方 Github](https://github.com/intel/linux-sgx)下载源代码。
2.  按README.md所述流程编译源代码。

