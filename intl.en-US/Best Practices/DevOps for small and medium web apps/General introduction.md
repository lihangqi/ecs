# General introduction {#concept_dyy_j32_qgb .concept}

The intended audience of this document are independent development teams that need to develop and maintain a small/medium web application on Alibaba Cloud. The goal is to keep things simpl. Necessary technologies and best practices are introduced step by step.

## Introduction {#section_js5_z32_qgb .section}

More complex tooling is mentioned near the middle of this tutorial, for example [infrastructure as code tools](https://en.wikipedia.org/wiki/Infrastructure_as_Code) are explained in [Continuous delivery](intl.en-US/Best Practices/DevOps for small and medium web apps/Continuous delivery.md#).

The sample web application that comes with this tutorial is composed of two parts:

-   A backend written in Java with [Spring Boot](https://spring.io/projects/spring-boot).
-   A frontend written in Javascript with [React](https://reactjs.org/).

This document addresses the following points:

-   How to automate compilation, testing, code analysis and packaging with a [CI pipeline](https://en.wikipedia.org/wiki/Continuous_integration).
-   How to extend this pipeline to [deploy the application automatically](https://en.wikipedia.org/wiki/Continuous_delivery).
-   How to setup a highly-available architecture on Alibaba Cloud.
-   How to backup periodically \(and restore!\) the database and the [version control system](https://en.wikipedia.org/wiki/Version_control).
-   How to upgrade the application and the database.
-   How to centralize logs and monitor your cluster.

## Prerequisites {#section_ipf_jj2_qgb .section}

To follow this tutorial:

-   Familiarize yourself with [Git](https://git-scm.com/) and install it on your computer.
-   Make sure you have an Alibaba Cloud account.
-   Download the [related resources](https://github.com/alibabacloud-howto/devops/tree/master/tutorials/devops_for_small_to_medium_web_applications) before moving to the next part.

