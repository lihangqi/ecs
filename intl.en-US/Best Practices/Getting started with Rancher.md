# Getting started with Rancher {#concept_yht_32n_qgb .concept}

## Introduction {#section_r4y_j2n_qgb .section}

[Rancher](https://rancher.com/) is a multi-cluster [Kubernetes](https://kubernetes.io/) management platform. The goal of this tutorial is to explain how to set up Rancher on a [single node](https://rancher.com/docs/rancher/v2.x/en/installation/) and how to integrate it with Alibaba Cloud Container Service.

## Prerequisites {#section_s4y_j2n_qgb .section}

To follow this topic, you need to create an Alibaba Cloud account and [obtain an AccessKey ID and Secret](https://partners-intl.aliyun.com/help/faq-detail/63482.htm).

Cloud resources are created with [Terraform](https://www.terraform.io/) scripts. If you do not know this tool, [follow this topic](https://www.terraform.io/intro/getting-started/install.html) and familiarize yourself with the [Alicloud Provider](https://www.terraform.io/docs/providers/alicloud/index.html).

You are familiarized with Kubernetes. You can follow this [tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/) to learn the basics. You need to [set up the command line tool kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

The [related resources](https://github.com/alibabacloud-howto/devops/tree/master/tutorials/getting_started_with_rancher) are downloaded.

## Rancher installation {#section_v4y_j2n_qgb .section}

There are two ways to [set up](https://rancher.com/docs/rancher/v2.x/en/installation/) Rancher:

-   Single-node configuration.
-   High-Availability configuration.

We will choose the first way as it makes things simpler.

Open a terminal on your computer and execute the following instructions:

``` {#codeblock_0rh_tba_o91}
# Go to the folder where you have downloaded this tutorial
cd path/to/this/tutorial

# Go to the Rancher environment folder
cd environment/rancher

# Download the latest stable version of the Alibaba Cloud provider
terraform init

# Configure the Alibaba Cloud provider
export ALICLOUD_ACCESS_KEY="your-accesskey-id"
export ALICLOUD_SECRET_KEY="your-accesskey-secret"
export ALICLOUD_REGION="your-region-id"

# Configure variables for the Terraform scripts
export TF_VAR_ecs_root_password="YourR00tP@ssword"

# Create the resources in the cloud
terraform apply
```

The last command should ask you to confirm by entering `yes` and should print logs that end like this:

``` {#codeblock_nb8_4wk_i6r}
Apply complete! Resources: 9 added, 0 changed, 0 destroyed.

Outputs:

rancher_eip_ip_address = 161.117.4.26
```

Open a web browser tab and enter the URL corresponding to https://rancher\_eip\_ip\_address \(for example, https://161.117.4.26/\). Your web browser will complain that the connection is unsecured \(which is normal because we did not configure any SSL/TLS certificate\). Make an exception and continue browsing.

**Note:** If using an invalid certificate bothers you, follow [this documentation](https://rancher.com/docs/rancher/v2.x/en/installation/single-node/#2-choose-an-ssl-option-and-install-rancher) to set up HTTPS.

The following welcome page is displayed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173839917_en-US.png)

Set an administrator password and click **Continue**. Keep the default value of the server URL and click **Save URL**.

The Clusters page is displayed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173839918_en-US.png)

## Kubernetes cluster {#section_bpy_j2n_qgb .section}

Unfortunately the integration with Alibaba Cloud Container Service is not yet supported by the current version of Rancher \(v2.1.3\). However, we can create a Kubernetes cluster with Terraform and import it manually to Rancher.

 **Cluster sizing** 

Before creating our cluster we need to size it correctly. Currently in Alibaba Cloud, a Kubernetes cluster must have exactly 3 master nodes, but the node instance types \(number of CPUs and amount of RAM\) and the number of worker nodes are flexible.

**Note:** [This document](https://elastisys.com/wp-content/uploads/2018/01/kubernetes-ha-setup.pdf?x83281) is a good introduction about the master and worker node concepts in Kubernetes.

[This document in Chinese](https://yq.aliyun.com/articles/599169) gives advices about which instance type to choose for master nodes; it also provides general tips about cluster administration. Concerning our sizing problem, this article proposes the following configurations:

-   1-5 worker nodes, master specification: 4 vCPUs and 8 GB of RAM
-   6-20 worker nodes, master specification: 4 vCPUs and 16 GB of RAM
-   21-100 worker nodes, master specification: 8 vCPUs and 32 GB of RAM
-   100-200 worker nodes, master specification: 16 vCPUs and 64 GB of RAM

According to the same article, the disk size for each master node does not need to be large, as it mainly contains the OS \(about 3 GB\), docker images, system and application logs, temporary data, and so on.

[This second document in Chinese](https://yq.aliyun.com/articles/602932) explains how to choose the number and the type of workers nodes. It also provides information about network driver, disk size selection and other management tasks.

The first important advice this topic provides is to prefer few large workers instead of many small ones:

-   A small number of large workers increases the chance of having interdependent containers running on the same machine, which greatly reduces network transmission.
-   Large resources \(such as network bandwidth or physical RAM\) concentrated on few nodes allow better resource utilization. For example if two applications need 1 GB of RAM, it is better to collocate them on one worker with 3 GB of physical RAM instead of distributing them on two workers with 1.5 GB of physical RAM each; in the first case the large worker is able to accept a third application that would also need 1 GB of RAM, whereas the two small workers cannot.
-   Pulling Docker images is more efficient on a smaller number of workers, because images are downloaded, stored on the local disk, and then re-used between containers.

However a too small number of workers is not a good idea, because a system should continue to function even if a worker node is down. The exact number of workers depends on the total number of required vCPUs and on the acceptable fault tolerance.

Let’s consider the following example where a system needs a total of 160 vCPUs:

-   If the fault tolerance is 10%, we cannot lose more than 16 vCPUs, so a valid configuration is 10 workers with 16 vCPUs.
-   If the fault tolerance is 20%, we cannot lose more than 32 vCPUs, so a valid configuration is 5 workers with 32 vCPUs.

About the amount of RAM for each worker, the document gives the following rule of thumb in case of applications that are relatively greedy in memory, such as Java applications: a good ratio is 8 GB of RAM per vCPU, so if we choose an instance type with 4 vCPUs, then we need to take about 32 GB of RAM.

 **Cluster creation** 

We will create a Kubernetes cluster in multiple availability zones. This decision increases the availability of the system, but it adds the following constraints:

-   Alibaba Cloud Container Service is designed to support either 1 or 3 availability zones.
-   To be compatible with most of the regions, we can only use 2 availability zones, so we will need to configure our Kubernetes cluster to use twice the same availability zone.
-   The minimum number of worker nodes is 3.

Open a terminal on your computer and execute the following instructions:

``` {#codeblock_p5c_1l9_hum}
# Go to the folder where you have downloaded this tutorial
cd path/to/this/tutorial

# Go to the Rancher environment folder
cd environment/kubernetes-cluster

# Download the latest stable version of the Alibaba Cloud provider
terraform init

# Configure the Alibaba Cloud provider
export ALICLOUD_ACCESS_KEY="your-accesskey-id"
export ALICLOUD_SECRET_KEY="your-accesskey-secret"
export ALICLOUD_REGION="your-region-id"

# Configure variables for the Terraform scripts
export TF_VAR_ecs_root_password="YourR00tP@ssword"
export TF_VAR_master_instance_cpu_count=4
export TF_VAR_master_instance_ram_amount=8 # in GB
export TF_VAR_master_instance_disk_size=40 # in GB
export TF_VAR_worker_instance_count=3 # Must be >= 3
export TF_VAR_worker_instance_cpu_count=4
export TF_VAR_worker_instance_ram_amount=32 # in GB
export TF_VAR_worker_instance_disk_size=80 # in GB

# Create the resources in the cloud
terraform apply
```

The last command should ask you to confirm by entering `yes` and should end with similar logs:

``` {#codeblock_28u_me5_094}
Apply complete! Resources: 16 added, 0 changed, 0 destroyed.

Outputs:

rancher_k8s_cluster_ip_address = 161.117.96.245
```

**Note:** Do not worry if the operation takes some time. Creating a cluster typically takes about 15 minutes.

Let’s configure [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) locally so that it can communicate with the new cluster. Execute the following commands in your terminal:

``` {#codeblock_yml_6mv_2q5}
mkdir $HOME/.kube
scp root@161.117.96.245:/etc/kubernetes/kube.conf $HOME/.kube/config
# Note 0: the IP address is the one from `rancher_k8s_cluster_ip_address`.
# Note 1: the password is the one that was set in `TF_VAR_ecs_root_password`.

# Check that it worked
kubectl cluster-info
```

If the configuration went well, the result of the last command should be something like:

``` {#codeblock_0jd_1ac_l8t}
Kubernetes master is running at https://161.117.96.245:6443
Heapster is running at https://161.117.96.245:6443/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://161.117.96.245:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
monitoring-influxdb is running at https://161.117.96.245:6443/api/v1/namespaces/kube-system/services/monitoring-influxdb/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## Importing the Kubernetes Cluster into Rancher {#section_kpy_j2n_qgb .section}

Now that we have our Kubernetes Cluster, let’s import it into Rancher so that we can manage it from there.

Open your web browser tab with Rancher \(the page you got when you finished the [Rancher installation section](https://alibabacloud-howto.github.io/devops/tutorials/getting_started_with_rancher/README.html#rancher-installation)\) and follow these instructions:

1.  The current page must be the **Clusters** one. Click **Add Cluster**.
2.  Select **Import existing cluster**.
3.  Set the **Cluster Name** field to **alibabacloud-cluster**.
4.  Click **Create**.

You should get a page like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173839920_en-US.png)

Let’s execute the last command. Copy it and paste it in your terminal:

``` {#codeblock_qxf_8yg_slz}
# Command from Rancher in order to import the cluster
curl --insecure -sfL https://161.117.4.26/v3/import/nlz588gctmkkkpc8jsntrht8ff65gbp4d629smqzbcjpvxzltfdmph.yaml | kubectl apply -f -
```

This command should output the following logs:

``` {#codeblock_vz1_9rz_2p5}
namespace/cattle-system created
serviceaccount/cattle created
clusterrolebinding.rbac.authorization.k8s.io/cattle-admin-binding created
secret/cattle-credentials-1d26caa created
clusterrole.rbac.authorization.k8s.io/cattle-admin created
deployment.extensions/cattle-cluster-agent created
daemonset.extensions/cattle-node-agent created
```

Go back to the web browser tab and click **Done**. You should now see your cluster:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173939921_en-US.png)

On this page, click the cluster name \(alibabacloud-cluster\). You should obtain a dashboard similar to this one:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173939922_en-US.png)

## Testing {#section_qpy_j2n_qgb .section}

Let’s play a bit with Rancher by deploying a small application. Open your web browser tab with the cluster dashboard and execute the following actions:

1.  In the top menu, select **Projects/Namespaces**.
2.  This page displays two projects **Default** and **System**. Click **Default**.
3.  The new page displays the workloads, but it is empty for the moment. Click **Deploy**.
4.  In this form, set the fields like this:
    -   Name = hello-workload
    -   Docker Image = rancher/hello-world
5.  Scroll down and click **Show advanced options**.
6.  Expand **Labels & Annotations** and click **Add Label**.
7.  Set the key app and the value hello-app.
8.  Click **Launch**.

After few seconds you should see your workload named **hello-workload** with the **Active** status:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173939923_en-US.png)

Let’s [create a load balancer](https://rancher.com/docs/rancher/v2.x/en/k8s-in-rancher/load-balancers-and-ingress/) to expose this application to internet:

1.  Click **Import YAML**.
2.  Copy the following content in the dark text area:

    ``` {#codeblock_o9n_w1j_0jw}
    apiVersion: v1
    kind: Service
    metadata:
      name: hello-app-load-balancer
      labels:
        app: hello-app
    spec:
      type: LoadBalancer
      ports:
      - port: 80
        protocol: TCP
        targetPort: 80
      selector:
        app: hello-app
    ```

3.  Click **Import**.
4.  Click **Load Balancing**.

You can see your load balancer:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173939924_en-US.png)

To get the IP address of this load balancer, click the menu on the right of **hello-app-load-balancer** \(with 3 vertical dots\) and select **View/Edit YAML**. You can see a large YAML file. Scroll down until you see the `status`:

``` {#codeblock_gzs_b17_cxc}
status:
  loadBalancer:
    ingress:
    - ip: 161.117.96.212
```

Copy this IP address and paste it into the URL bar of a new web browser tab. You can access to your application:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123251/156013173939925_en-US.png)

Congratulation if you managed to get this far! If you want to continue to learn about Kubernetes and Rancher, see the [official documentation](https://rancher.com/docs/rancher/v2.x/en/k8s-in-rancher/).

