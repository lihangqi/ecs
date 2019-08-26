# Best practices of ECS data security {#concept_51404_zh .concept}

This document introduces how to implement data security for ECS instances from the O&M perspective.

## Intended audience {#section_e1n_gv2_2fb .section}

This document applies to individuals and enterprises that are new to Alibaba Cloud.

## Contents {#section_kwg_dv2_2fb .section}

-   Back up data regularly
-   Design security domains properly
-   Set security group rules
-   Set logon passwords
-   Server port security
-   Application vulnerability protection
-   Security information collection

## Back up data regularly {#section_nwg_dv2_2fb .section}

As the foundation of disaster tolerance, data backup is intended to reduce the risk of data loss due to system failures, operation errors, and security problems. ECS instances come with the snapshot backup function. Correctly using the snapshot function can satisfy the data backup requirements for most users. It is recommended to customize your own backup policy according to actual business needs. You can select [Create Snapshot](../../../../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) or [Create Automatic Snapshot Policy](../../../../intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md#), and [apply the policy to specific disks](../../../../intl.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#). It is recommended to take automatic snapshots on a daily basis, and store them for at least seven days. Good backup habits contribute to rapid data recovery and minimizing losses in the case of failure.

## Design security domains properly {#section_pwg_dv2_2fb .section}

Developed upon the Software Defined Network \(SDN\) technology, VPCs allow you to build private networks that separate servers of different security levels in your enterprise, preventing servers from impacting each other over an interconnected network.

It is recommended that you [create VPC](https://www.alibabacloud.com/help/zh/doc-detail/27710.htm), and set the IP address range, network segments, route tables, and gateways. You can store important data in an intranet that is totally isolated from the Internet. You can use Elastic IP \(EIP\) addresses or the Jumper Server to manage data in daily O&M.

## Set security group rules {#section_qwg_dv2_2fb .section}

As an important means for security isolation, security groups are used to set network access control for one or more ECS instances. With security groups, you can set firewall policies at the instance level, filtering active and passive access of an instance at the network layer. Specifically, you can restrict inbound and outbound access on a port, and authorize access to IP addresses, reducing attacks and enhancing instance security.

For example, the remote port is 22 by default in Linux, which should not be open to the Internet directly. You can set up a security group to control the Internet access to an ECS instance, such as authorizing fixed IP addresses to access the instance. To learn more about security groups, see [Application cases](../../../../intl.en-US/Security/Security groups/Scenarios.md#). If you have higher requirements, you can also use third-party VPN products to encrypt the logon data. For more software, visit [Alibaba Cloud Market](https://market.aliyun.com/software).

## Set logon passwords {#section_swg_dv2_2fb .section}

Weak passwords have been a major cause of data leakage, as they are one of the most common vulnerabilities and can be exploited very easily. It is recommended that the server password should contain at least eight characters, and should be complicated enough by including uppercase and lowercase letters, numbers and special characters. In addition, you should change the password regularly.

## Server port security {#section_twg_dv2_2fb .section}

As long as servers provide Internet services, the corresponding ports will be exposed to the Internet. From the perspective of security management, more open ports mean more system risks. It is recommended to open as few ports as necessary to the Internet. Common ports should be changed to custom ports \(port 30000 or greater\), and access control should be implemented on the service ports.

For example, it is recommended to restrict database services to the intranet and prevent access from the Internet. If it is necessary to access the database directly from the Internet, you need to change the connection port from 3306 to a greater port, and authorize the relevant IP addresses according to the business needs.

## Application vulnerability protection {#section_bts_32f_2fb .section}

Application vulnerabilities are security defects that can be exploited by hackers to illegally access data from Web applications, cache, database and storage. Common application vulnerabilities include SQL injection, XSS attacks, Web shells, backdoor, command injection, illegal HTTP requests, common Web server vulnerability attacks, unauthorized access to core files, path traversal, and more. These vulnerabilities are different from system vulnerabilities, and are difficult to fix. If application security cannot be guaranteed during the initial design, servers may be attacked due to such vulnerabilities. Therefore, it is recommended to install a [Web Application Firewall \(WAF\)](../../../../intl.en-US/Quick Start/Quick start.md#) to prevent various attacks, thus ensuring website security and availability.

## Security information collection {#section_jyy_pdf_2fb .section}

In today's Internet security field, both security engineers and hackers are racing against the clock. As a security service based on big data, [Alibaba Cloud Security Situational Awareness](../../../../intl.en-US/Product Introduction/What is Security Center?.md#) can fully, rapidly and accurately capture and analyze factors that may lead to security situation changes in large cloud computing environments. After that, Situational Awareness associates the current threats with the past ones to perform big data analysis, so as to predict potential security events in the future and provide a systematic solution.

Therefore, in addition to daily O&M, technicians should obtain as much information as possible to improve warning capability. In this way, quick recovery can be made possible in the case of security problems and ECS data security can be truly guaranteed.

