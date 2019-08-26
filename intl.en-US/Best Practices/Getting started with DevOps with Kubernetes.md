# Getting started with DevOps with Kubernetes {#concept_jfq_c2n_qgb .concept}

## Introduction {#section_upr_d2n_qgb .section}

The goal of this tutorial is to explain how to create a [CI](https://en.wikipedia.org/wiki/Continuous_integration)/[CD](https://en.wikipedia.org/wiki/Continuous_delivery) pipeline to deploy an application in [Kubernetes](https://kubernetes.io/) running on top of Alibaba Cloud.

The procedure can be summarized in two mains steps:

1.  Installing the tooling environment \(Gitlab and Kubernetes\).
2.  Creating a small Java web application and configuring a CI/CD pipeline around it.

## Prerequisite {#section_wpr_d2n_qgb .section}

The very first step is to create an Alibaba Cloud account and obtain an AccessKey ID and Secret.

Cloud resources are created with [Terraform](https://www.terraform.io/) scripts. If you do not know this tool, [follow this tutorial](https://www.terraform.io/intro/getting-started/install.html) and familiarize yourself with the [alicloud provider](https://www.terraform.io/docs/providers/alicloud/index.html).

Make sure you are familiarized with Kubernetes. If you need, you can follow this [awesome tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/) to learn the basics. You will also need to [setup the command line tool kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

You should also have [Git](https://git-scm.com/) installed on your computer.

## Preparation {#section_dbm_bly_bhb .section}

Please download the [related resources](https://github.com/alibabacloud-howto/devops/tree/master/tutorials/getting_started_with_devops_with_kubernetes) on your computer by cloning this Git repository. Open a terminal and enter the following commands:

```
# Navigate to a folder where you want to clone this tutorial
cd ~/projects

# Clone this repository
git clone git@github.com:alibabacloud-howto/devops.git

# Navigate to the folder of this tutorial
cd devops/tutorials/getting_started_with_devops_with_kubernetes/
```

## Gitlab environment {#section_zpr_d2n_qgb .section}

This tutorial uses [Gitlab](https://about.gitlab.com/) to manage Git repositories and to run CI/CD pipelines. The community edition is free, simple to use and have all the features that we need for this demo.

Open a terminal and enter the following commands with your own AccessKey and region information:

```
export ALICLOUD_ACCESS_KEY="your-accesskey-id"
export ALICLOUD_SECRET_KEY="your-accesskey-secret"
export ALICLOUD_REGION="your-region-id"

cd environment/gitlab
terraform init
terraform apply -var 'gitlab_instance_password=YourSecretR00tPassword'
```

**Note:** This script is a bit too simple to be used in production, for example, an SSL certificate should be configured to allow HTTPS. Here is a [more complete tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-gitlab-on-ubuntu-16-04) about Gitlab installation.

The output of the script should contain the IP addresses of the newly installed Gitlab instance and a [Gitlab runner](https://docs.gitlab.com/ce/ci/runners/):

```
Outputs:

gitlab_runner_public_ip = w.x.y.z
gitlab_public_ip = a.b.c.d
```

Open the page `http://a.b.c.d` \(from `gitlab_public_ip`\) in your web browser and:

1.  Set a new password.
2.  Sign in as root \(with your new password\).

You should be able to see a welcome screen. You can now generate and upload an SSH key:

1.  Click your user’s avatar on the top-right of the page and select **Settings**.
2.  In the left-side navigation pane, select **SSH Keys**.
3.  If necessary, generate your SSH key as instructed.
4.  Copy your public key in the textarea \(it should be in the file **~/.ssh/id\_rsa.pub**\).
5.  Click **Add key**.

The next step is to register the Gitlab runner \(the ECS instance that runs CI/CD scripts\):

1.  In the top menu, select **Admin area** \(the wrench icon\).
2.  In the left-side navigation pane, select **Overview** \> **Runners**.
3.  The new page must provide a URL and a token under the section **Setup a shared Runner manually**. Keep this page opened, open a terminal, and run the following commands:

    ```
    ssh root@w.x.y.z # The IP address is from `gitlab_runner_public_ip`. The password is the one you set with `gitlab_instance_password`.
    gitlab-runner register
    ```

    Enter the URL and the token from the web browser tab, set **docker-runner** as the description, choose **docker** as executor and set **alpine:latest** as the default Docker image.

    **Note:** Do not set any tag, or your GitLab runner will not execute your jobs.

4.  Refresh the web browser tab and check the runner is displayed.

Go back to the home page by clicking on the Gitlab icon on the top-left side of the screen and keep this web browser tab opened, we will return to it later.

## Kubernetes environment {#section_gqr_d2n_qgb .section}

To keep it simple, this tutorial creates a single-AZ cluster. However, a multi-AZ one is preferred for production. Read the official documentation for more information.

Open a terminal and enter the following commands with your own AccessKey and region information:

```
export ALICLOUD_ACCESS_KEY="your-accesskey-id"
export ALICLOUD_SECRET_KEY="your-accesskey-secret"
export ALICLOUD_REGION="your-region-id"

cd environment/kubernetes
terraform init
terraform apply -var 'k8s_password=YourSecretR00tPassword'
```

**Note:** It takes about 20 minutes to create a Kubernetes cluster.

The output of the script should contain the master node public IP address:

```
Outputs:

k8s_master_public_ip = e.f.g.h
```

Execute the following commands to configure **kubectl** \(the password is the one you set with the variable `k8s_password`\):

```
mkdir $HOME/.kube
scp root@e.f.g.h:/etc/kubernetes/kube.conf $HOME/.kube/config # The IP address is the one from `k8s_master_public_ip`

# Check that it works
kubectl cluster-info
```

If the configuration went well, the result of the last command should be something like:

```
Kubernetes master is running at https://161.117.97.242:6443
Heapster is running at https://161.117.97.242:6443/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://161.117.97.242:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
monitoring-influxdb is running at https://161.117.97.242:6443/api/v1/namespaces/kube-system/services/monitoring-influxdb/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## Container registry {#section_kqr_d2n_qgb .section}

Unfortunately it is not yet possible to create a container registry on Alibaba Cloud through Terraform. Instead, this step must be done manually through the web console:

1.  Log on to the [Container Registry console](https://partners-intl.console.aliyun.com/#/cr).
2.  In the left-side navigation pane, select **Products** \> **Container Registry**.
3.  Select your region on top of the page.
4.  Click **Namespace** from the left-side navigation pane.
5.  Click **Create Namespace**, set a name such as **cicd-k8s-tutorial** and click **Confirm**.
6.  Click **Repositories** from the left-side navigation pane.
7.  If you do not remember it, you can click **Reset Docker Login Password**.

Keep this page opened in the web browser, we will need to create a repository in the next step.

## CI/CD Pipeline {#section_mqr_d2n_qgb .section}

This tutorial uses a very simple [Spring Boot](https://spring.io/guides/gs/spring-boot/) app as an example. You can find the source code in the folder `app/simple-rest-service`.

**Docker image repository**

The first step is to create a repository where Docker images will be saved. Open you web browser tab from the [Container registry section](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_devops_with_kubernetes/README.html#container-registry) and execute the following instructions:

1.  Click **Create Repository**, select your namespace, set the repository name to **simple-rest-service**, set a summary, set the type as **Public**, click **Next**, select **Local Repository** as Code Source, and click **Create Repository**.
2.  You should now see a list of repositories. Click **Manage** for your new repository.
3.  On the new page, copy the **Internet** repository address and keep it on the side for the moment.

**Gitlab project**

Open the web browser tab you created [in the Gitlab environment section](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_devops_with_kubernetes/README.html#gitlab-environment) and create a new project:

1.  From the home page, click **Create a project**.
2.  Set the name **simple-rest-service** and click **Create project**.
3.  Once the project is created, in the left-side navigation pane, select **Settings** \> **CI/CD**.
4.  Expand the **Variables** panel, and create the following variables:
    -   DOCKER\_REGISTRY\_IMAGE\_URL = **Internet** repository address you got from the [Docker image repository section](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_devops_with_kubernetes/README.html#docker-image-repository)
    -   DOCKER\_REGISTRY\_USERNAME = Alibaba Cloud account username
    -   DOCKER\_REGISTRY\_PASSWORD = Docker Login Password you might have reset in the [Container registry section](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_devops_with_kubernetes/README.html#container-registry)
    -   K8S\_MASTER\_PUBLIC\_IP = The Kubernetes cluster public IP \(from `k8s_master_public_ip`\)
    -   K8S\_PASSWORD = The Kubernetes password \(from `k8s_password`\)

The project repository is now ready to host files:

1.  Open a terminal on your local machine and type:

    ```
    mkdir -p $HOME/projects
    cd $HOME/projects
    git clone git@a.b.c.d:root/simple-rest-service.git # The IP address comes from `gitlab_public_ip`
    cd simple-rest-service
    ```

2.  Copy the following files from **app/simple-rest-service** into the new folder **$HOME/projects/simple-rest-service**:
    -   src - Sample application source code
    -   pom.xml - [Maven](https://maven.apache.org/) project descriptor \(declares dependencies and packaging information for the application\)
    -   deployment.yml - Kubernetes deployment descriptor \(describes the deployment and a load balancer service\)
    -   .gitlab-ci.yml - CI/CD descriptor \(used by Gitlab to create a pipeline\)
3.  In your terminal, type:

    ```
    git add .gitlab-ci.yml deployment.yml pom.xml src/
    git commit -m "Initial commit"
    git push origin master
    ```

    **Note:** If you have an error when you try to push your code, it may be due to the fact that the master branch is automatically protected. In this case, go to the Gitlab web browser tab, select **Settings** \> **Repository** \> **protected Branches**, type `master` in the Branch attribute, and select **Create Wildcard Master**.


Gitlab automatically recognizes the file **.gitlab-ci.yml** and create a pipeline with 3 steps:

1.  Compile and execute unit tests.
2.  Create the Docker image with [JIB](https://github.com/GoogleContainerTools/jib) and upload it to the [Docker image repository](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_devops_with_kubernetes/README.html#docker-image-repository).
3.  Deploy the application in Kubernetes.

You can see the pipeline in Gitlab by selecting **CI/CD** \> **Pipelines** from the left-side navigation pane.

After you pipeline has been executed completely, you can check you Kubernetes cluster with the following commands:

-   Check the deployments:

    ```
    kubectl get deployments
    ```

    The result should be something like:

    ```
    NAME                  DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
    simple-rest-service   2         2         2            2           21m
    ```

-   Check the pods:

    ```
    kubectl get pods
    ```

    The result should be something like:

    ```
    NAME                                   READY   STATUS    RESTARTS   AGE
    simple-rest-service-5b9c496d5d-5n6vl   1/1     Running   0          18m
    simple-rest-service-5b9c496d5d-h758n   1/1     Running   0          18m
    ```

-   Check the services:

    ```
    kubectl get services
    ```

    The result should be something like:

    ```
    NAME                      TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
    simple-rest-service-svc   LoadBalancer   10.1.214.231   161.117.73.86   80:30571/TCP   23m
    ```

-   Check the logs of one pod:

    ```
    kubectl logs simple-rest-service-5b9c496d5d-5n6vl
    ```

    The result should start with:

    ```
    .   ____          _            __ _ _
       /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
      ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
       \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
        '  |____| .__|_| |_|_| |_\__, | / / / /
       =========|_|==============|___/=/_/_/_/
       :: Spring Boot ::        (v2.0.5.RELEASE)
    ```


Test the application by yourself:

1.  Open a new tab in your web browser and visit http://161.117.73.86 \(the service EXTERNAL-IP\). You should see **Hello world!**
2.  Add `?name=Seven` to the URL \(so it should be something like **http://161.117.73.86?name=Seven**\). You should see the **Hello Seven!**

