# Overview {#concept_tmr_pgx_wdb .concept}

Based on the network type and operating system of your ECS instance, and the operating system of your local machine, use one of the following methods to connect to an ECS instance.

## Connect to a Linux instance {#section_fjm_rgx_wdb .section}

The following table details different methods by which to remotely connect to a Linux instance.

|Is Internet access required?|Operating system of the local machine |Connection method|
|:---------------------------|:-------------------------------------|:----------------|
|Yes/No|Windows or Unix-like OS|[Connect to an instance by using the Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#).|
|Yes|Windows|Use a remote connection tool to create remote connection:-   Use an SSH key pair as the credential. For details, see [connect to a Linux instance by using an SSH key pair](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using an SSH key pair.md#).
-   Use a password as the credential. For details, see [connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#windows).

|
|Yes|Linux, Mac OS, or other Unix-like OS|Use commands to create remote connection:-   Use an SSH key pair as the credential. For details, see [connect to a Linux instance by using an SSH key pair](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using an SSH key pair.md#linux).
-   Use a password as the credential. For details, see [connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#linux).

|
|Yes|iOS or Android|User apps, such as SSH Control Lite or JuiceSSH, to create remote connection. For details, see [connect to an instance on a mobile device](reseller.en-US/User Guide/Connect to instances/Connect to an instance on a mobile device.md#linux).|

## Connect to a Windows instance {#section_mjm_rgx_wdb .section}

The following table details different methods by which to remotely connect to a Windows instance.

|Is Internet access required?|Operating system of the local machine|Connection method|
|:---------------------------|:------------------------------------|:----------------|
|Yes/No|Windows or Unix-like OS|[Connect to an instance by using the Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#).|
|Yes|Windows|Use mstsc to create remote connection. For details, see [connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#windows).|
|Yes|Linux|Use a remote connection tool, such as rdesktop, to create remote connection. For details, see [connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#linux).|
|Yes|Mac OS|Use Microsoft Remote Desktop Connection for Mac to create remote connection. For details, see [connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#macOS).|
|Yes|iOS or Android|Use Microsoft Remote Desktop to create a remote connection. For details, see [connect to an instance on a mobile device](reseller.en-US/User Guide/Connect to instances/Connect to an instance on a mobile device.md#windows).|

