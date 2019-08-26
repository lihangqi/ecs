# GitLab installation and configuration {#concept_ems_xj2_qgb .concept}

## Introduction {#section_uqw_qk2_qgb .section}

[GitLab CE edition](https://about.gitlab.com/) is a free open-source tool that will help us to host Git repositories and run our CI/CD pipeline.

To keep it simple, we will install GitLab on an ECS instance with a direct access to internet. Although the servers will be protected via [encryption](https://en.wikipedia.org/wiki/Transport_Layer_Security) and restrictive [security group rules](../../../../reseller.en-US/Security/Security groups/Add security group rules.md#), you might also want to isolate your virtual machines from internet by using a [VPN Gateway](../../../../reseller.en-US/Product Overview/What is VPN Gateway?.md#).

The following diagram illustrates the architecture we will put in place for GitLab:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122916/155928288038457_en-US.png)

## Cloud resources creation {#section_fcr_jm2_qgb .section}

The first step is to buy a domain name. This is necessary if you want to enable security on your servers:

1.  Log on to the [Domain console](https://partners-intl.console.aliyun.com/#/dc).
2.  Click **Purchase**.
3.  Choose a domain, such as **my-sample-domain.xyz** and follow the instructions to buy it.
4.  Return to the console and refresh the page in order to see your new domain.

**Note:** Due to a limitation in Direct Mail, choose a domain name with less than 28 characters.

The second step is to create ECS instances and related resources:

1.  Log on to the [VPC console](https://partners-intl.console.aliyun.com/#/vpc).
2.  Select the region where you want to create the VPC on top of the page, for example, Singapore.
3.  Click **Create VPC**.
4.  Fill in the new form with the following information:
    -   VPC name = devops-simple-app-vpc
    -   VPC destination CIDR Block = “192.168.0.0/16”
    -   VSwitch name = devops-simple-app-vswitch
    -   VSwitch zone = first zone of the list
    -   VSwitch destination CIDR Block = “192.168.0.0/24”
5.  Click **OK**the create the VPC and the VSwitch.
6.  In the VPC list, click the VPC you have just created.
7.  Scroll down and click **0** at the right of **Security Group**.
8.  In the new page, click **Create Security Group**.
9.  Fill in the new form with the following information:
    -   Template = Web Server Linux
    -   Security Group Name = devops-simple-app-security-group
    -   Network Type = VPC
    -   VPC = select the VPC you just created \(with the name devops-simple-app-vpc\)
10. Click **OK** to create the security group and the rules from the template. Note that the rules open the ports for [SSH](https://en.wikipedia.org/wiki/Secure_Shell), [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol), [HTTPS](https://en.wikipedia.org/wiki/HTTPS) and [ICMP](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol) to any computer on Internet.
11. Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
12. Click **Create Instance**.
13. If needed, select **Advanced Purchase** \(also named **Custom**\).
14. Fill in the wizard with the following information:
    -   Billing Method = Pay-As-You-Go
    -   Region = the same as your VPC and the same availability zone as the VSwitch
    -   Instance Type = filter by vCPU = 2, Memory = 4 GiB, Current Generation tab, and select a remaining type such as **ecs.n4.large**
    -   Image = Ubuntu 18.04 64bit
    -   System Disk = Ultra Disk 40 GiB
    -   Network = VPC, select the VPC and VSwitch you have just created
    -   Do NOT assign a public IP \(we will create an EIP instead, which is more flexible\)
    -   Security Group = select the group you have just created
    -   Log on Credentials = select **Password** and choose one
    -   Instance Name = devops-simple-app-gitlab
    -   Host = devops-simple-app-gitlab
    -   Read and accept the terms of service
15. Finish the instance creation by clicking **Create Instance**.
16. Go back to the console, click **Instances** from the left-side navigation pane, and select a region. Now you can see your new instance.
17. Click **EIP** from the left-side navigation pane.
18. On the new page, click **Create EIP**.
19. Fill in the wizard with the following information:
    -   Region = the region where you have created your ECS
    -   Max Bandwidth = 1 Mbps
    -   Quantity = 1
20. Click **Buy Now**, check the agreement of service, and click **Activate**.
21. Go back to the console and check your new EIP.
22. Next to you new EIP, click **Bind**.
23. In the new form, select:
    -   Instance Type = ECS Instance
    -   ECS Instance = devops-simple-app-gitlab/i-generatedstring
    -   Click **OK** to bind the EIP to your ECS instance.
24. Copy the IP address of your EIP \(for example, 47.88.155.70\).

The ECS instance is ready for GitLab. Now register a sub-domain for this machine:

1.  Log on to the [Domain console](https://partners-intl.console.aliyun.com/#/dc).
2.  On the row corresponding to your domain \(for example, my-sample-domain.xyz\), click **Resolve**.
3.  Click **Add Record**.
4.  Fill in the new form with the following information:
    -   Type = A- IPV4 address
    -   Host = gitlab
    -   ISP Line = Outside mainland China
    -   Value = The EIP IP Address \(for example, 47.88.155.70\)
    -   TTL = 10 minute\(s\)
5.  Click **OK** to add the record.

## GitLab installation {#section_qnl_1qm_qgb .section}

We can now finally install GitLab! Open a terminal on your computer and type:

``` {#codeblock_9o6_4ur_00l}
# Connect to the ECS instance
ssh root@gitlab.my-sample-domain.xyz # Use the password you set when you have created the ECS instance

# Update the machine
apt-get update
apt-get upgrade

# Add the GitLab repository for apt-get
cd /tmp
curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
bash /tmp/script.deb.sh

# Install GitLab
apt-get install gitlab-ce

# Open GitLab configuration
nano /etc/gitlab/gitlab.rb
```

**Note:** If you use MAC OSX, you must first disable the setting **Set locale environment variables on startup** in **Preferences** \> **Profiles** \> **Advanced**.

In the GitLab configuration file, replace the value of `external_url` by `http://gitlab.my-sample-domain.xyz` \(the domain you have just purchased and configured\), and then save and quit by pressing Ctrl + X.

Now start GitLab and try it. In your terminal, run the following command:

``` {#codeblock_78a_65f_lr3}
gitlab-ctl reconfigure
```

Open your web browser on `http://gitlab.my-sample-domain.xyz`. You can see the following screen:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122916/155928288038568_en-US.png)

Congratulation if you get a similar screen! In case it does not work, first make sure you did not miss a step, and then [raise an issue](https://github.com/alibabacloud-howto/devops/issues) if the problem persists.

Do not enter your new password yet because you are using an unencrypted connection. Now fix this problem.

## HTTPS configuration {#section_fg4_q5m_qgb .section}

Open your terminal and enter the following commands:

``` {#codeblock_9go_4rl_32r}
# Connect to the ECS instance
ssh root@gitlab.my-sample-domain.xyz # Use the password you set when you have created the ECS instance

# Install dependencies
apt-get install ca-certificates openssh-server
apt-get install postfix # During the installation, select "Internet Site" and set your domain (for example, gitlab.my-sample-domain.xyz)

# Open GitLab configuration
nano /etc/gitlab/gitlab.rb
```

The last command allows you to edit GitLab configuration:

1.  Modify the value of `external_url` by adding an `s` to `http://` into `https://` \(for eample, https://gitlab.my-sample-domain.xyz\).
2.  Scroll to **Let’s Encrypt integration** and insert the following lines:

    ``` {#codeblock_8sy_ke9_bro}
    letsencrypt['enable'] = true
    letsencrypt['contact_emails'] = ["john.doe@your-company.com"] # Your email address
    letsencrypt['auto_renew'] = true
    letsencrypt['auto_renew_hour'] = 11
    letsencrypt['auto_renew_minute'] = 42
    letsencrypt['auto_renew_day_of_month'] = "*/14"
    ```

    Quit and save the file by pressing Ctrl + X, and then apply the configuration change and restart GitLab with:

    ``` {#codeblock_myq_7nv_h1i}
    gitlab-ctl reconfigure
    ```

    Check it worked by opening your web browser to https://gitlab.my-sample-domain.xyz \(with the `s` in https\).


You can now enter your new password and sign in with the username `root` and your new password. You can now access to the GitLab dashboard.

Before going further we still need to configure two things:

-   An email server so that GitLab can send emails.
-   Automatic backup in order to avoid loosing data.

## Mail server configuration {#section_l5k_lxm_qgb .section}

**Note:** Direct Mail is not available in all regions, but you can configure it in a different one from where you have created your ECS. At the time of writing, Direct Mail is available in China \(Hangzhou\), Singapore and Australia \(Sydney\). Contact us if you need it in another region.

Go back to the Alibaba Cloud web console and execute the following instructions:

1.  Log on to the [Direct Mail console](https://partners-intl.console.aliyun.com/#/dm).
2.  Select the region on top of the page.
3.  Click **Email Domains** from the left-side navigation pane.
4.  Click **New Domain**.
5.  In the new form, set the `domain as mail.my-sample-domain.xyz` \(the domain you chose earlier with the prefix `mail`\).
6.  The page must be refreshed with your new email domain. Click **Configure** link on its right side.
7.  The new page explains you how to configure your domain. Keep this web browser tab opened, open a new one and go to the [Domain console](https://partners-intl.console.aliyun.com/#/dc).
8.  Click **Resolve** link next to your domain.
9.  Click **Add Record**.
10. Fill the new form with the following information:
    -   Type = TXT- Text
    -   Host = the **Host record** column under **1,Ownership verification** in the Direct Mail tab \(for example, aliyundm.mail\)
    -   ISP Line = Outside mainland China
    -   Value = the **Record value** column under **1,Ownership verification** in the Direct Mail tab \(for example, 3cdb41a3351449c2af6f\)
    -   TTL = 10 minute\(s\)
11. Click **OK** and click **Add Record** again.
12. Fill the new form with the following information:
    -   Type = TXT- Text
    -   Host = the **Host record** column under **2,SPF verification** in the Direct Mail tab \(for example, mail\)
    -   ISP Line = Outside mainland China
    -   Value = the **Record value** column under **2,SPF verification** in the Direct Mail tab \(for example, v=spf1 include:spfdm-ap-southeast-1.aliyun.com -all\)
    -   TTL = 10 minute\(s\)
13. Click **OK** and click **Add Record** again.
14. Fill the new form with the following information:
    -   Type = MX- Mail exchange
    -   Host = the **Host record** column under **3,MX Record Verification** in the Direct Mail tab \(for example, mail\)
    -   ISP Line = Outside mainland China
    -   Value = the **Record value** column under **3,MX Record Verification** in the Direct Mail tab \(for example, mxdm-ap-southeast-1.aliyun.com\)
    -   MX Priority = 10
    -   TTL = 10 minute\(s\)
    -   Synchronize the Default Line = checked
15. Click **OK** and click **Add Record** again.
16. Fill the new form with the following information:
    -   Type = CNAME- Canonical name
    -   Host = the **Host record** column under **4,CNAME Record Verification** in the Direct Mail tab \(for example, dmtrace.mail\)
    -   ISP Line = Outside mainland China
    -   Value = the **Record value** column under **4,CNAME Record Verification** in the Direct Mail tab \(for example, tracedm-ap-southeast-1.aliyuncs.com\)
    -   TTL = 10 minute\(s\)
17. Click **OK**.

You should probably have a domain configuration that looks like that:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122916/155928288038861_en-US.png)

Continue the email server configuration:

1.  Go back to the Direct Mail console \(the web browser tab you kept opened\).
2.  Click **Cancel** to go back to the email domain list.
3.  Click **Verify** next to your new domain, and confirm when the prompt appears.
4.  Refresh the page after 20 sec. If the status of your domain is still **To Be Verified**, click **Configure** and check which step is still in the **To Be Verified** status, fix your domain configuration and re-do the previous step \(**Verify**\). Sometime the verification step is a bit slow and you need to retry several times. When the email domain status is **Verification successful**, you can continue to the next step.
5.  Click **Sender Addresses** from the left-side navigation pane.
6.  Click **Create Sender Address**.
7.  Fill the new form with the following information:
    -   Email Domains = mail.my-sample-domain.xyz \(the email domain you just configured\)
    -   Account = gitlab
    -   Reply-To Address = your email address \(for example, john.doe@your-company.com\)
    -   Mail Type = Triggered Emails
8.  Click **OK** to close the form.
9.  Your new sender address should be added to the list. click **Set SMTP password** next to it.
10. Set the SMTP password and click **OK**.
11. Click **Verify the reply-to address** next to your new sender address, and confirm when the prompt appears.
12. Check your mailbox corresponding to the address you set in the **Reply-To Address** field, you should have received an email from **directmail**.
13. Click on the link in this email in order to see a confirmation message.
14. Go back to the sender addresses page and save the SMTP address and port at the end of the description, it should be something like **SMTP service address: smtpdm-ap-southeast-1.aliyun.com . SMTP service ports: 25, 80 or 465\(SSL encryption\)**.

Now that the email server is ready, let’s configure GitLab to use it. Open a terminal on your computer and enter the following commands:

``` {#codeblock_m4s_etx_hjn}
# Connect to the ECS instance
ssh root@gitlab.my-sample-domain.xyz # Use the password you set when you have created the ECS instance

# Open GitLab configuration
nano /etc/gitlab/gitlab.rb
```

Scroll down to **\#\#\# Email Settings** and insert the following lines:

``` {#codeblock_v2v_7v0_l5u}
gitlab_rails['gitlab_email_enabled'] = true
gitlab_rails['gitlab_email_from'] = 'gitlab@mail.my-sample-domain.xyz' # The sender address you have just created
gitlab_rails['gitlab_email_display_name'] = 'GitLab'
gitlab_rails['gitlab_email_reply_to'] = 'gitlab@mail.my-sample-domain.xyz'
```

Scroll down to **\#\#\# GitLab email server settings** and insert the following lines:

``` {#codeblock_ces_jto_427}
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtpdm-ap-southeast-1.aliyun.com"   # SMTP address written in the Direct Mail console
gitlab_rails['smtp_port'] = 465                                     # SMTP port written in the Direct Mail console
gitlab_rails['smtp_user_name'] = "gitlab@mail.my-sample-domain.xyz" # Sender address
gitlab_rails['smtp_password'] = "HangzhouMail2018"                  # SMTP password for the sender address
gitlab_rails['smtp_domain'] = "mail.my-sample-domain.xyz"           # Your email domain
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = false
gitlab_rails['smtp_tls'] = true
```

Apply the configuration change and restart GitLab:

``` {#codeblock_g4h_v19_fa1}
gitlab-ctl reconfigure
```

You can test the configuration like this:

1.  Go to GitLab and sign in as root: https://gitlab.my-sample-domain.xyz/
2.  Click **Admin area** in the top menu \(the wrench icon\).
3.  Click **Users** from the left-side navigation pane.
4.  Click **Administrator** user.
5.  Click **Edit**.
6.  Change the **Email** field to your personal email address.
7.  Click **Save changes**.
8.  Sign out by clicking on your profile picture on the top-right of the page and by selecting **Sign out**.
9.  Click the **Forgot your password?** link.
10. Set your personal email address and click **Reset password**.
11. Check in your personal mailbox and verify you have received an email \(it may be in the spam folder\).

## Automatic backup configuration {#section_ddz_fzm_qgb .section}

Backups are important because they prevent data loss in case of accident and allow you to migrate to another ECS instance if you need.

In order to run backups automatically, please open a terminal and run the following commands:

**Note:** The [GitLab documentation](https://docs.gitlab.com/ee/raketasks/backup_restore.html#tar) requires tar version to be equals to or later than 1.30.

Let’s now create an OSS bucket where we will store our backups:

1.  Log on to the [OSS console](https://partners-intl.console.aliyun.com/#/oss).
2.  Click **Create Bucket**.
3.  Fill the new form with the following information:
    -   Bucket Name = gitlab-my-sample-domain-xyz \(you can set the name you want, but it must be unique\)
    -   Region = the same as your ECS instance \(for example, Asia Pacific SE 1 \(Singapore\)\)
    -   Storage Class = Standard
    -   Access Control List \(ACL\) = Private
4.  Click **OK**.
5.  The page must show the bucket you have just created. Save the last **Endpoint** for VPC Network Access \(something like `oss-ap-southeast-1-internal.aliyuncs.com`\). It contains your bucket name and the region ID, for example, ap-southeast-1.

You will also need an access key id and secret:

1.  Log on to the [user management center](https://partners-intl.console.aliyun.com/#/usercenter) by clicking on your user on the top-right of the page and by selecting AccessKey.
2.  Click **Create Access Key**.
3.  Note the AccessKeyID and the AccessKeySecret and click **Save AccessKey Information**.

In your terminal, mount your OSS bucket as a folder:

``` {#codeblock_kkt_nnt_hp7}
# Save your bucket name, access key id and access key secret in the file /etc/passwd-ossfs
# The format is my-bucket:my-access-key-id:my-access-key-secret
echo gitlab-my-sample-domain-xyz:LTAI********ujwZ:rc15yggaCX08A********X49wNUGpk > /etc/passwd-ossfs
chmod 640 /etc/passwd-ossfs

# Create a folder where we will mount the OSS bucket
mkdir /mnt/gitlab-bucket

# Mount the OSS bucket
# The -ourl come from the last "Endpoint" for VPC Network Access
ossfs gitlab-my-sample-domain-xyz /mnt/gitlab-bucket -ourl=http://oss-ap-southeast-1-internal.aliyuncs.com

# Check it works
echo "It works" > /mnt/gitlab-bucket/test.txt

# Unmount the OSS bucket
umount /mnt/gitlab-bucket
```

Check that the test file is present in your bucket:

1.  Log on to the [OSS console](https://partners-intl.console.aliyun.com/#/oss).
2.  Click your bucket name from the left-side navigation pane.
3.  Click **Files** from the top menu.
4.  The file test.txt should be present and should contain **It works**.
5.  Delete this file.

Configure the OSS bucket so that it is automatically mounted when the ECS machine starts. Create the following file:

Adapt and copy the following content:

Make sure you set the right bucket name and endpoint. Quit and save by pressing CTRL + X. Configure Systemd to run this script at startup:

Log on to the [OSS console](https://partners-intl.console.aliyun.com/#/oss), and check that the test2.txt file is present in your bucket and delete it.

Let’s now configure GitLab to put its backup files in the mounted folder. Open the terminal and run:

``` {#codeblock_mhj_76u_ddw}
# Open GitLab configuration
nano /etc/gitlab/gitlab.rb
```

Scroll to **\#\#\# Backup Settings** and insert the following line:

``` {#codeblock_mca_nlh_gkq}
gitlab_rails['backup_path'] = "/mnt/gitlab-bucket/backup/"
```

Quit and save by pressing CTRL + X, and then check if it works:

``` {#codeblock_p1n_jyt_a70}
# Apply GitLab configuration
gitlab-ctl reconfigure

# Manually launch a first backup
gitlab-rake gitlab:backup:create
```

The last command should have created a backup. Log on to the OSS console and check you have a file with a path like backup/1540288854\_2018\_10\_23\_11.3.6\_gitlab\_backup.tar.

Let’s now configure automatic backup to be executed automatically every night. For that we will create two types of [cron jobs](https://en.wikipedia.org/wiki/Cron): one to execute the backup command above, one to save the GitLab configuration files.

Open your terminal and execute:

``` {#codeblock_ng2_j99_gk1}
# Edit the CRON configuration file. Select nano as the editor.
crontab -e
```

Enter the following lines into this file:

``` {#codeblock_zkr_y67_qxu}
0 2 * * * /opt/gitlab/bin/gitlab-rake gitlab:backup:create CRON=1
0 2 * * * /bin/cp /etc/gitlab/gitlab.rb "/mnt/gitlab-bucket/backup/$(/bin/date '+\%s_\%Y_\%m_\%d')_gitlab.rb"
0 2 * * * /bin/cp /etc/gitlab/gitlab-secrets.json "/mnt/gitlab-bucket/backup/$(/bin/date '+\%s_\%Y_\%m_\%d')_gitlab-secrets.json"
```

Save and quit by pressing CTRL + X.

You now have configured automatic backup every night at 2AM. If you want to test this configuration you can replace **0 2 \* \* \*** by the current time + 2 min. for example if the current time is 14:24, then set **26 14 \* \* \***. after that you need to wait about 2 min and check whether new files have been created in your OSS bucket.

The restoration process is well described in the [official documentation](https://docs.gitlab.com/ee/raketasks/backup_restore.html#restore-for-omnibus-installations) \(section **Restore for Omnibus installations**\). Note that it is considered as a [best practice](https://www.theregister.co.uk/2017/02/01/gitlab_data_loss/) to test your backups from time to time.

## GitLab runner installation and configuration {#section_zcq_hzm_qgb .section}

It is [a best practice](https://docs.gitlab.com/ce/install/requirements.html#gitlab-runner) to run CI/CD jobs \(code compilation, unit tests execution, application packing, and so on\) on a different machine from the one that run GitLab.

Thus, we need to setup one [runner](https://docs.gitlab.com/ce/ci/runners/) on a new ECS instance. Please execute the following instructions:

1.  Log on to the [VPC console](https://partners-intl.console.aliyun.com/#/vpc).
2.  Select the region of the GitLab ECS instance \(on top of the screen\).
3.  Click the VPC **devops-simple-app-vpc**.
4.  Click **1** next to **Security Group**.
5.  Click **Create Security Group**.
6.  Fill the new form with the following information:
    -   Template = Customize
    -   Security Group Name = devops-simple-app-security-group-runner
    -   Network Type = VPC
    -   VPC = select the VPC **devops-simple-app-vpc**
7.  Click **OK** to create the group. We will not add any rule in order to be as restrictive as possible \(to improve security\).
8.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
9.  Click **Create Instance**.
10. If needed, select **Advanced Purchase** \(also named **Custom**\).
11. Fill the wizard with the following information:
    -   Billing Method = Pay-As-You-Go
    -   Region = the same as the ECS instance where you have installed GitLab
    -   Instance Type = filter by vCPU = 2, Memory = 4 GiB, Current Generation tab, and select a remaining type such as **ecs.n4.large**
    -   Image = Ubuntu 18.04 64bit
    -   System Disk = Ultra Disk 40 GiB
    -   Network = VPC, select the VPC and VSwitch of the GitLab ECS instance
    -   Assign a public IP \(no need of an EIP this time\)
    -   Security Group = select **devops-simple-app-security-group-runner**
    -   Log on Credentials = select **Password** and choose one
    -   Instance Name = devops-simple-app-gitlab-runner
    -   Host = devops-simple-app-gitlab-runner
    -   Read and accept the terms of service
12. Finish the instance creation by clicking **Create Instance**.
13. Go back to the ECS console, select **Instances** from the left-side navigation pane and choose your region on top the screen. you should be able to see your new instance **devops-simple-app-gitlab-runner**.
14. Click **Connect** on the right of your ECS instance, copy the VNC Password \(something like **667078**\) and enter it immediately after.
15. You should see a terminal in your web browser inviting you to login. Authenticate as root with the password you have just created.

Execute the following commands in this web-terminal:

``` {#codeblock_46e_rs2_xhf}
# Update the machine
apt-get update
apt-get upgrade

# Add a new repository for apt-get for GitLab Runner
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh | sudo bash

# Add a new repository for apt-get for Docker
apt-get install software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Update the machine
apt-get update

# Install GitLab runner
apt-get install gitlab-runner

# Install dependencies for Docker
apt-get install apt-transport-https ca-certificates curl software-properties-common

# Install Docker
apt-get install docker-ce
```

As you can see we setup two applications: [GitLab Runner](https://docs.gitlab.com/ce/ci/runners/) and [Docker](https://www.docker.com/). We will keep things very simple with Docker: it is a [very](https://docs.docker.com/engine/swarm/key-concepts/)[powerful](https://kubernetes.io/) tool, but for the moment we will just use it as a super installer, for example we will not setup any tool, compiler or SDK on this machine. instead we will be lazy and let Docker to download the right [images](https://docs.docker.com/get-started/) for us. Things will become more clear later in this tutorial when we will configure our CI/CD pipeline.

Now we need to connect the runner with GitLab:

1.  Open GitLab in another web browser tab \(the URL must be like https://gitlab.my-sample-domain.xyz/\).
2.  Sign in if necessary.
3.  Click **Admin area** from the top \(the wrench icon\).
4.  Click **Runners** from the left.

The bottom of the page contains an URL and a token:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122916/155928288138984_en-US.png)

Go back to the web-terminal connected to the runner machine, and type:

``` {#codeblock_9l9_uam_pyj}
gitlab-runner register
```

This tool needs several information to register the runner. Enter the following responses:

1.  Enter the gitlab-ci coordinator URL \(for example, https://gitlab.com\): copy the URL from the GitLab page above \(for example, https://gitlab.my-sample-domain.xyz/\)
2.  Enter the gitlab-ci token for this runner: copy the token from the GitLab page above \(for example, gXppo8ZyDgqdFb1vPG-w\)
3.  Enter the gitlab-ci description for this runner: devops-simple-app-gitlab-runner
4.  Enter the gitlab-ci tags for this runner \(comma separated\): \(keep it empty\)
5.  Enter the executor: docker
6.  Enter the default Docker image \(for example, ruby:2.1\): alpine:latest

After the tool gives you back the hand, you should be able to see this runner in the GitLab web browser tab. Refresh the page and check at the bottom, you should see something like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122916/155928288138986_en-US.png)

Our GitLab is now ready to be used! But there are few more points to consider before creating our first project:

## User management {#section_ynr_jzm_qgb .section}

As administrator, there are few steps you need to follow in order to improve your GitLab account:

1.  Open GitLab in your web browser \(the URL must be like https://gitlab.my-sample-domain.xyz/\).
2.  Click your avatar on the top-right of the page and select **Settings**.
3.  Correctly set the **Full name** and **Email** fields and click **Edit profile settings**.
4.  Click **Account** from the left.
5.  Change your username and click **Update username**, and then confirm it again when the prompt appears \(this step improves security as attackers would have to guess your username in addition to your password\).

You may also want to control who can register on your GitLab server \(the default configuration allows anyone on internet to register\):

1.  Click **Admin area** from the top \(the wrench icon\).
2.  Click **Settings** from the left.
3.  Expand the **Sign-up restrictions** section.
4.  Uncheck the **Sign-up enabled** field.
5.  Click **Save changes**.

Now only administrators can create new users. This can be done by navigating to the **Overview** \> **Users** in the **Admin area**.

## Maintenance {#section_kkz_kzm_qgb .section}

Linux servers need to be upgraded from time to time: security patches must be installed as soon as possible and applications should be updated to their latest versions.

On Ubuntu instances, the following commands allow you to safely update your server:

``` {#codeblock_cvu_655_9et}
apt-get update
apt-get upgrade
```

Other commands such as `apt-get dist-upgrade` or `do-release-upgrade` are less safe, especially the last one since it can update Ubuntu to a newer LTS version that is not yet supported by Alibaba Cloud.

For more complex upgrade it may be more practical to replace the ECS instance:

1.  Create a [backup](https://alibabacloud-howto.github.io/devops/tutorials/devops_for_small_to_medium_web_applications/part_01_gitlab_installation_and_configuration.html#automatic-backup-configuration) of the existing GitLab data.
2.  Create a new ECS instance and install GitLab.

    **Note:** The GitLab version on the new ECS instance must be the same as the old one, if not the backup-restore process fails.

3.  Restore the backups into the new machine.
4.  Check the new instance works.
5.  Unbind the EIP from the old ECS instance and bind it to the new one.
6.  Release the old ECS instance.

Security updates can be automatically installed thanks to `unattended-upgrades`. For each ECS instance \(GitLab and its runner\), open a terminal \(using SSH or the web-terminal console\) and enter the following commands:

``` {#codeblock_x86_jhf_zh1}
# Install unattended-upgrades
apt-get install unattended-upgrades

# Check the default configuration is fine for you. Press CTRL+X to quit.
nano /etc/apt/apt.conf.d/50unattended-upgrades

# Enable automatic upgrades
dpkg-reconfigure --priority=low unattended-upgrades

# Edit the related configuration
nano /etc/apt/apt.conf.d/20auto-upgrades
```

The last configuration file can be modified in order to look like this:

``` {#codeblock_lzm_05x_nbz}
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
```

Save and quit by pressing CTRL + X. You can launch `unattended-upgrades` manually for testing:

``` {#codeblock_2e4_jjz_4zr}
unattended-upgrade -d
```

The logs of `unattended-upgrades` are printed in `/var/log/unattended-upgrades`.

More information about automatic update [can be found here](https://help.ubuntu.com/18.04/serverguide/automatic-updates.html.en).

## Upgrade {#section_akf_mzm_qgb .section}

The described architecture for GitLab is fine as long as the number of users is not too large. However, there are several solutions when things start to get slow:

-   When pipeline jobs take too much time to run, maybe adding more runners or using ECS instances with higher specs can help.
-   When GitLab itself become slow, the simplest solution is to migrate it to a stronger ECS instance type.

When a single GitLab instance become unacceptable, maybe because of performance issues or because [high-availability](https://en.wikipedia.org/wiki/High_availability) is required, the architecture can evolve into a distributed system involving the following cloud resources:

-   Additional ECS instances.
-   A server load balancer to distribute the load across ECS instances.
-   A NAS to let multiple ECS instances to share a common file storage system.
-   An external database.

As you can see the complexity can quickly increase. Tools such as [Packer](https://www.packer.io/) \(virtual machine image builder\), [Terraform](https://www.terraform.io/) \(infrastructure as code software\) or [Chef](https://www.chef.io/) / [Puppet](https://puppet.com/) / [Ansible](https://www.ansible.com/) / [SaltStack](https://www.saltstack.com/)\(configuration management\) can greatly help managing it: they require an initial investment but allow organizations to better manage their systems.

Another solution is to let other companies to manage this complexity for you. There are many [SaaS](https://en.wikipedia.org/wiki/Software_as_a_service) vendors such as [GitLab.com](https://about.gitlab.com/pricing/#gitlab-com) or [GitHub](https://github.com/business). Alibaba Cloud offers Codepipeline, but it is currently only available in Chinese.

