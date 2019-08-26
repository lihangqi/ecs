# Change the private IP of an ECS instance {#task_bng_thn_xdb .task}

After creating an ECS instance in a VPC network, you can change the private IP address and can change the VSwitch of the ECS instance.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs). 
2.  In the left-side navigation pane, click **Instances**. 
3.   Select the target region. 
4.  In the **Actions** column, click **More** \> **Instance Status** \> **Stop**. 
5.  When the instance is stopped, click the instance ID to go to its Instance Details page. 
6.  In the **Configuration Information** panel, click **More** \> **Modify Private IP Address**. 
7.  In Modify Private IP Address dialog, select a VSwitch, and then click **Modify**. 

    Make sure the current VSwitch and the selected VSwitch are in the same zone.

    **Note:** Enter a new IP address if you do not want to change the VSwitch of the ECS instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9658/15432131645483_en-US.png)

8.  Go back to the instance page and, in the **Actions** column, click **More** \> **Instance Status** \> **Restart** to make the new private IP address take effect. 

