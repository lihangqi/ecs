# 什么是Terraform {#concept_twc_3dz_dfb .concept}

Terraform是一种开源工具，用于安全高效地预配和管理云基础结构。

[HashiCorp Terraform](https://www.terraform.io/) 是一个IT基础架构自动化编排工具，可以用代码来管理维护 IT 资源。Terraform的命令行接口 \(CLI\) 提供一种简单机制，用于将配置文件部署到阿里云或其他任意支持的云上，并对其进行版本控制。

它编写了描述云资源拓扑的配置文件中的基础结构，例如虚拟机、存储帐户和网络接口。Terraform 的命令行接口（CLI）提供一种简单机制，用于将配置文件部署到阿里云或任何其他支持的云并对其进行版本控制。

Terraform是一个高度可扩展的工具，通过 Provider 来支持新的基础架构。您可以使用Terraform来创建、修改、删除ECS、VPC、RDS、SLB等多种资源。

## 优势 {#section_w55_1fz_dfb .section}

-   **将基础结构部署到多个云**

    Terraform适用于多云方案，将相类似的基础结构部署到阿里云、其他云提供商或者本地数据中心。开发人员能够使用相同的工具和相似的配置文件同时管理不同云提供商的资源。

-   **自动化管理基础结构**

    Terraform能够创建配置文件的模板，以可重复、可预测的方式定义、预配和配置ECS资源，减少因人为因素导致的部署和管理错误。能够多次部署同一模板，创建相同的开发、测试和生产环境。

-   **基础架构即代码（Infrastructure as Code）**

    可以用代码来管理维护资源。允许保存基础设施状态，从而使您能够跟踪对系统（基础设施即代码）中不同组件所做的更改，并与其他人共享这些配置 。

-   **降低开发成本**

    您通过按需创建开发和部署环境来降低成本。并且，您可以在系统更改之前进行评估。


## 应用场景 {#section_j4f_wmz_dfb .section}

Terraform的应用场景请参见 [Terraform详情页](https://www.alibabacloud.com/solutions/devops/terraform)。

## 使用Terraform {#section_igv_5kz_dfb .section}

Terraform能够让您在阿里云上轻松使用 [简单模板语言](https://www.terraform.io/docs/configuration/syntax.html) 来定义、预览和部署云基础结构。以下为Terraform在ECS中预配资源的必要步骤：

1.  安装Terraform。
2.  配置Terraform。
3.  使用Terraform创建一台或多台ECS实例。

## 更多资料 {#section_exx_ldh_2fb .section}

-   [Terraform Alibaba provider文档](https://www.terraform.io/docs/providers/alicloud/index.html)
-   [Terrafrom Alibaba github](https://github.com/alibaba/terraform-provider)
-   [Terraform Registry Alibaba Modules](https://registry.terraform.io/browse?provider=alicloud)

