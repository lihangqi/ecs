# Initialize the Control Cluster to Create a Control Cluster Master {#task_bv3_5y1_hgb .task}

After installing the first NSX Controller, initializing the control cluster is required to enable that the controller is able to communicate with the hypervisor hosts.

-   Install at least one NSX Controller.
-   Join the NSX Controller with the management plane.
-   Verify that you have admin privileges to log in to the NSX Controller appliance.
-   Assign a shared secret password. A shared secret password is a user-defined shared secret password .

1.  Right-click the NSX Controller virtual appliance and click **Power** \> **Power on** in the vCenter Server. 
2.  Right-click the NSX Controller virtual appliance and click **Open Console**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708740535865_en-US.png)

 
3.  Enter the CLI admin username and pasword to log in to the NSX Controller. 
4.  Run the `set control-cluster security-model shared-secret secret <secret>` command and type a shared secret when prompted.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708740535869_en-US.png)

 
5.  Run the `initialize control-cluster` command. This command makes this controller the control cluster master. 

    **Note:** In the cluster, you only need to initialize one controller.

6.  Run the `get control-cluster status verbose` command. Verify that is master and in majority are true, the status is active, and the Zookeeper Server IP is reachable, ok.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/85020/154708740635870_en-US.png)

 

