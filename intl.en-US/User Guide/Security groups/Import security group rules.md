# Import security group rules {#task_jt3_spy_5fb .task}

Security group rules can be imported to a security group. You can export the rules of a security group to a file, and then import that file into other security groups or the original security group. In this way, you can quickly create or restore security group rules.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home). 
2.  Click Security Groups in the left-side navigation pane. 
3.  Select a region. 

    **Note:** You can import security group rules from different regions.

4.  On the Security Groups list page, find the target security group, and then click **Add Rules** in the **Actions** column. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64192/154865695432200_en-US.png)

5.  Click Import Rules. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64192/154865695432204_en-US.png)

6.  Select the target JSON file. You can preview the rules in the file. 

    The Preview Rules part displays the following information:

    -   The number of rules to be imported.
    -   Import check results. If any rules fail the import check, you can move the cursor over the warning icon for details.
    -   Details of the rules to be imported.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64192/154865695432208_en-US.png)

    **Note:** Up to 100 security group rules can be imported, so the remaining rules will not be imported. The imported new rules do not overwrite the existing rules.

7.  Click **Start** to import the rules. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64192/154865695432214_en-US.png)

8.  View the import results, and then click **Finish and close**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64192/154865695432218_en-US.png)


