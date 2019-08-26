# Configure the NSX Manager {#task_f1r_2vs_ggb .task}

After the OVF deployment is finished, you need to configure the NSX Manager.

1.  In the left-side navigation pane, click the target NSX Manager. On the **Configure** tab, choose **VM Hardware** \> **Edit**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708751035890_en-US.png)

2.  Click the **Network adapter 1** and delete the default network adapter \(**VM Network**\) under the **Virtual Hardware** configuration. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708751035891_en-US.png)

3.  At the bottom of the window, click **Select**, which is next to the **New device** option, choose **PCI device**, and click **Add**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708751035892_en-US.png)

4.  From the **New PCI device** entry, click the drop-down menu and choose 0000:61:00.0 | Red Hat, Inc. Transitional/Legacy Virtio PCI Network Card. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84983/154708751035893_en-US.png)


