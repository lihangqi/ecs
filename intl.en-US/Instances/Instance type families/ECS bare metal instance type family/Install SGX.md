# Install SGX {#concept_rw4_1wz_wgb .concept}

This topic describes what Intel Software Guard Extension \(Intel SGX\) is and how to install it.

## What is SGX? {#section_zmg_jws_qgb .section}

SGX is an Intel architecture extension designed to increase the security of application code and data. You can partition your application into processor-hardened enclaves or protected areas of execution in memory that increase security even on compromised platforms.

SGX sets aside one or more ranges of physical memory as the Enclave Page Cache \(EPC\) and encrypts the data stored in the EPC using the Memory Encryption Engine \(MEE\). The data stored in the EPC is only decrypted inside the CPU. SGX offers CPU-based security controls. Data remains protected even when the OS, VMM, or BIOS are compromised.

## Application {#section_x5x_jws_qgb .section}

You can encrypt sensitive data, pass the encrypted data to the enclave in the cloud, and provide the corresponding key to the enclave through remote attestation. Then, you can compute over the fully encrypted data protected by the CPU, and the result is returned to you in an encrypted version. In this way, you can make use of the powerful cloud computing infrastructures with reduced risk of data disclosure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130463/156023045743200_en-US.png)

## Enclave Definition Language \(EDL\) {#section_gqd_lws_qgb .section}

EDL is the fundamental part of SGX. It defines all enclave interface functions. During the build process, the Edger8r tool generates trusted and untrusted proxy/bridge functions and performs security checks.

Enclave interface functions can be divided into Enclave Calls \(ECALLs\) and Outside Calls \(OCALLs\).

-   ECALL: A call from the application into an interface function within the enclave, which is defined as a trusted environment.
-   OCALL: A call made from within the enclave to the application, which is defined as an untrusted environment.

```
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

## Install SGX using the installer file {#section_nsr_pws_qgb .section}

You can install SGX using the installer file, which includes the SGX driver, SGX Platform Software \(PSW\), and SDK. You must also install corresponding Linux kernel header files. The procedure is as follows:

**Note:** The default directory for the Makefile in the example is /opt/intel/.

1.  [Download](https://01.org/intel-software-guard-extensions/downloads) the SGX installer file.
2.  Follow the steps in the [Installation guide](https://download.01.org/intel-sgx/linux-2.0/docs/Intel_SGX_Installation_Guide_Linux_2.0_Open_Source.pdf).

## Install SGX using the source code {#section_cyz_rws_qgb .section}

You can install SGX using the source code, which includes the SGX driver, SGX Platform Software \(PSW\), and SDK. You must also install corresponding Linux kernel header files. The procedure is as follows:

**Note:** The default directory for the Makefile in the example is /opt/intel/.

1.  Download the source code from [Github](https://github.com/intel/linux-sgx).
2.  Compile the source code according to the README.md file.

