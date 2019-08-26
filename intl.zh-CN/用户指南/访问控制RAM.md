# 访问控制RAM {#concept_stg_4pd_zdb .concept}

如果您购买了多台云服务器 ECS 实例，您的组织里有多个用户需要使用这些实例。如果这些用户共享使用您的云账号密钥，那么存在以下问题：

-   您的密钥由多人共享，泄密风险高；
-   您无法限制用户的访问权限，容易出现误操作导致安全风险。

访问控制 RAM \(Resource Access Management\) 是阿里云提供的资源访问控制服务。通过 RAM，您可以集中管理您的用户（比如员工、系统或应用程序），以及控制用户可以访问您名下哪些资源的权限。

访问控制 RAM 将帮助您管理用户对资源的访问权限控制。例如，为了加强网络安全控制，您可以给某个群组附加一个授权策略，该策略规定：如果用户的原始 IP 地址不是来自企业网络，则拒绝此类用户请求访问您名下的 ECS 资源。

您可以给不同群组设置不同权限，例如：

-   SysAdmins：该群组需要创建和管理 ECS 镜像、实例、快照、安全组等权限。您给 SysAdmins 组附加了一个授权策略，该策略授予组成员执行所有 ECS 操作的权限。
-   Developers：该群组只需要使用实例的权限。您可以给 Developers 组附加一个授权策略，该策略授予组成员调用 DescribeInstances、StartInstance、StopInstance、CreateInstance 和 DeleteInstance 的权限。
-   如果某开发人员的工作职责发生转变，成为一名系统管理人员，您可以方便的将其从 Developpers 群组移到 SysAdmins 群组。

更多关于访问控制 RAM的介绍，请参考 [RAM 的产品文档](../../../../intl.zh-CN/产品简介/什么是RAM？.md)。

