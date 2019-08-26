# Export security group rules {#task_tpq_3jy_5fb .task}

Security group rules can be exported to a JSON file for local backup.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.11.bbdc2e95uqPijv#/home). 
2.  Click Security Groups in the left-side navigation pane. 
3.  Select a region. 
4.  On the Security Groups list page, find the target security group, and then click **Add Rules** in the **Actions** column. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64134/154865697532187_en-US.png)

5.  Click **Export Rules** to download and save the rules to a local JSON file. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64134/154865697532186_en-US.png)

    **Note:** The JSON file name takes the following format:

    ecs\_$\{region\_id\}\_$\{groupID\}.json

    If regionID is cn-qingdao, and groupID is sg-123, then the exported JSON file name is ecs\_cn-qingdao\_sg-123.json.


