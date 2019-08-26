# Modify configurations of vtep vSphere Distributed Switch {#task_d3r_tx1_hgb .task}

This topic describes the steps to modify the vtep VDS configurations.

1.  You have created a vtep VDS.
2.  You have added a host for the vtep VDS.
3.  Log on to the Windows instance on which the vCenter Server has been installed.

1.  Log on to the **vSphere Web Client**. 
2.  In the left-side navigation pane, click the distributed port group**vtep-DPortGroup**. 
3.   Click **Configure** from the right panel, and then click **Settings** \> **Properties**. On the Properties page, click **Edit**, as shown in the following figure.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84996/154705926035590_en-US.png)

 
4.   On the Edit Settings page, click **Security**. Click the **Promiscuous mode** drop-down box, and select Accept. Click the **MAC address changes** drop-down box, and select Accept, as shown in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/84996/154705926035591_en-US.png)

    The parameters are described as follows.

    |Parameter|Description|
    |:--------|:----------|
    |Promiscuous mode|     -   Accept: Placing a guest adapter in promiscuous mode causes it to detect all frames passed on the vSphere standard switch that are allowed under the VLAN policy for the port group that the adapter is connected to.
    -   Reject: Placing a guest adapter in promiscuous mode has no effect on which frames are received by the adapter.
 |
    |MAC address changes|     -   Accept: Changing the MAC address from the Guet OS has the intended effect : frames to the new MAC address are received.
    -   Reject: If you set to **Reject** and the guest operating system changes the MAC address of the adapter to anything other than what is in the .vmx configuratio file, all inbound frames are dropped. If the Guest OS changes the MAC address back to match the MAC address in the .vmx configuration file, inbound frames are passed again.
 |
    |Forged transmits|     -   Accept: No filtering I performed and all outbound frames are passed.
    -   Reject: Any outbound frame with a source MAC address that is different from the one currently set on the adapter are dropped.
 |

5.  Reboot the host that provides network management utilities. 

