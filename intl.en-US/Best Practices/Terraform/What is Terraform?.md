# What is Terraform? {#concept_twc_3dz_dfb .concept}

Terraform is an open source tool for securely and efficiently provisioning and managing cloud infrastructure.

[HashiCorp Terraform](https://www.terraform.io/) is an automated IT infrastructure orchestration tool that can use codes to manage and maintain IT resources. The Command Line Interface \(CLI\) of Terraform provides a simple mechanism, which is used for deploying and versioning configuration files on Alibaba Cloud or any other supported cloud.

Terraform writes the infrastructure, for example, virtual machines, storage accounts, and network interfaces in the configuration file that describes the cloud resource topology. The Command Line Interface \(CLI\) of Terraform provides a simple mechanism, which is used for deploying and versioning configuration files on Alibaba Cloud or any other supported cloud.

Terraform is a highly scalable tool that supports new infrastructure through providers. You can use Terraform to create, modify, or delete multiple resources, such as ECS, VPC, RDS, and SLB.

## Benefits {#section_w55_1fz_dfb .section}

-   **Multiple-cloud infrastructure deployment**

    Terraform applies to multi-cloud scenarios, where similar infrastructure is deployed on Alibaba Cloud, other cloud providers, or local data centers. Developers can use the same tool and configuration file to simultaneously manage the resources of different cloud providers.

-   **Automated infrastructure management**

    Terraform can create configuration file templates to define, provision, and configure ECS resources in a repeatable and predictable manner, reducing deployment and management errors resulting from human intervention. In addition, Terraform can deploy the same template multiple times to create the same development, test, and production environment.

-   **Infrastructure as code**

    With Terraform, you can use codes to manage and maintain resources. It allows you to store the infrastructure status, so that you can track the changes in different components of the system \(infrastructure as code\) and share these configurations with others.

-   **Reduced development costs**

    You can reduce costs by creating on-demand development and deployment environments, In addition, you can evaluate such environments before making system changes.


## Application scenarios {#section_j4f_wmz_dfb .section}

Terraform is a well-proven and open-source automated operation and maintenance tool for managing cloud infrastructure, creating images, and supporting multi-cloud business scenarios.

For the application scenarios of Terraform, see Terraform details.

## Use Terraform {#section_igv_5kz_dfb .section}

Terraform allows you to use a [simple template language](https://www.terraform.io/docs/configuration/syntax.html) to easily define, preview, and deploy cloud infrastructure on Alibaba Cloud. The steps for Terraform to provision resources in ECS are described as follows:

1.  Install Terraform.
2.  Configure Terraform.
3.  Use Terraform to create one or more ECS instances.

## More information {#section_exx_ldh_2fb .section}

-   [Terraform Alibaba provider](https://www.terraform.io/docs/providers/alicloud/index.html)
-   [Terrafrom Alibaba github](https://github.com/alibaba/terraform-provider)
-   [Terraform Registry Alibaba Modules](https://registry.terraform.io/browse?provider=alicloud)

