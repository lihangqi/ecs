# Modify the VMkernal adapter MAC address {#task_sw4_4y1_hgb .task}

This topic describes how to modify the VMkernal adapter MAC address for each ESXi host.

1.  View the MAC addresses corresponded to the VMkernal adapters of the two hosts. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84997/154705647135627_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84997/154705647135629_en-US.png)

2.  View the MAC addresses corresponded to the physical adapters of the two hosts. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84997/154705647135628_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84997/154705647135630_en-US.png)

3.  Open SSH sessions to both ESXi hosts, and run the vi /etc/vmware/esx.conf command. Find the corresponding MAC address of the VMkernal adapter, and modify it to the MAC address of the physical adapter. 
4.  Reboot both ESXi hosts to make the modification take effect. 

