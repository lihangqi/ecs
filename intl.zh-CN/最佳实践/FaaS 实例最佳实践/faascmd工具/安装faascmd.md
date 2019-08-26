# 安装faascmd {#concept_blq_4qz_sfb .concept}

本文为您介绍如何下载安装faascmd工具。

## 准备工作 {#section_rjw_wzz_sfb .section}

-   您需要在运行fasscmd的实例上完成以下准备工作。
    1.  检查Python版本，需为2.7.x。

```
python -V
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61532/154398718930953_zh-CN.png)

    2.  运行以下命令安装python模块。

```
pip -q install oss2
pip -q install aliyun-python-sdk-core
pip -q install aliyun-python-sdk-faas
pip -q install aliyun-python-sdk-ram
```

    3.  运行以下命令检查aliyun-python-sdk-core的版本号，需为2.11.0或以上版本。

```
cat /usr/lib/python2.7/site-packages/aliyunsdkcore/__init__.py
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61532/154398718930957_zh-CN.png)

**说明：** 如果版本号低于2.11.0，运行 `pip install --upgrade aliyun-python-sdk-core` 命令升级至最新版本。

-   [获取RAM用户的AccessKey ID和AccessKey Secret](../../../../intl.zh-CN/通用参考/创建AccessKey.md#)

## 操作步骤 {#section_b4w_yb1_tfb .section}

1.  登录实例后，您可以在当前目录或任意目录下运行`wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/faascmd`命令下载faascmd。

**说明：** 在 [配置faascmd](intl.zh-CN/最佳实践/FaaS 实例最佳实践/faascmd工具/配置faascmd.md#) 时，您需要把faascmd所在目录的绝对路径添加到PATH变量中。

2.  运行以下命令为faascmd添加可执行权限。

```
chmod +x faascmd
```


