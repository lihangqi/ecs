# Code quality {#concept_j2h_dbn_qgb .concept}

## Introduction {#section_nht_2bn_qgb .section}

Before we continue on the way to deployment, it is important to add a stage in our pipeline to improve the code quality of our application. In this tutorial we are introducing [SonarQube](https://www.sonarqube.org/), a tool that can help us to find bugs before they arrive in production, and help us to manage the [technical debt](https://en.wikipedia.org/wiki/Technical_debt).

## SonarQube infrastructure {#section_oht_2bn_qgb .section}

Let’s create an ECS instance with [SonarQube](https://www.sonarqube.org/):

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Click **Create Instance**.
3.  If needed, select **Advanced Purchase** \(also named **Custom**\).
4.  Fill the wizard with the following information:
    -   Billing Method = Pay-As-You-Go
    -   Region = the same region and availability zone as your GitLab server
    -   Instance Type = filter by vCPU = 2, Memory = 4 GiB, Current Generation tab, and select a remaining type such as **ecs.n4.large**
    -   Image = Ubuntu 18.04 64bit
    -   System Disk = Ultra Disk 40 GiB
    -   Network = VPC, select the same VPC and VSwitch as the GitLab server
    -   Do NOT assign a public IP \(we will create an EIP instead, which is more flexible\)
    -   Security Group = select the group **devops-simple-app-security-group**
    -   Log on Credentials = select **Password** and choose one
    -   Instance Name = devops-simple-app-sonar
    -   Host = devops-simple-app-sonar
    -   Read and accept the terms of service
5.  Finish the instance creation by clicking **Create Instance**.
6.  Go back to the ECS console, select **Instances** from the left-side navigation pane, and choose your region on top the screen. You can see your new instance.
7.  Click **EIP** from the left-side navigation pane.
8.  On the new page, click **Create EIP**.
9.  Fill the wizard with the following information:
    -   Region = the region where you have created you ECS
    -   Max Bandwidth = 1 Mbps
    -   Quantity = 1
10. Click **Buy Now**, select the agreement of service, and click **Activate**.
11. Go back to the EIP console and check your new EIP.
12. Next to you new EIP, click **Bind**.
13. In the new form, select:
    -   Instance Type = ECS Instance
    -   ECS Instance = devops-simple-app-sonar/i-generatedstring
14. Click **OK** to bind the EIP to you ECS instance.
15. Copy the IP Address of your EIP \(it should be something like 47.74.253.23\).

The ECS instance is ready, let’s register a sub-domain for this machine:

1.  Log on to the [Domain console](https://partners-intl.console.aliyun.com/#/dc).
2.  On the row corresponding to your domain \(for example, **my-sample-domain.xyz**\), click **Resolve**.
3.  Click **Add Record**.
4.  Fill the new form with the following information:
    -   Type = A- IPV4 address
    -   Host = sonar
    -   ISP Line = Outside mainland China
    -   Value = The EIP IP Address \(for example 47.74.253.23\)
    -   TTL = 10 minute\(s\)
5.  Click **OK** to add the record.

SonarQube requires a database, let’s create a PostgreSQL RDS instance:

1.  Log on to the [ApsaraDB for RDS console](https://partners-intl.console.aliyun.com/#/rdsnext).
2.  Click **Create Instance**.
3.  Fill the form with the following information:
    -   Select **Pay-As-You-Go**
    -   Region = the same as your ECS instance
    -   DB Engine = PostgreSQL
    -   Version = 9.4
    -   Edition = High-availability
    -   Zone = the same as your ECS instance
    -   Network type = VPC, select the same VPC and availability zone as your ECS instance
    -   Type = 2 cores, 4 GB \(type rds.pg.s2.large\)
    -   Capacity = 20GB
    -   Quantity = 1
4.  Click **Buy Now**, accept the **Product Terms of Service** and **Service Level Notice and Terms of Use**, and click **Pay Now**.
5.  Go back to the ApsaraDB for RDS console and wait for the RDS instance to start \(it can take few minutes\).
6.  Set a name for your RDS instance by moving your mouse cursor over it and by clicking the pen icon. Set the name **devops-simple-app-sonar-rds** and confirm.
7.  Click the instance ID.
8.  Click **Set Whitelist** in the **Basic Information** \> **Intranet Address** section.
9.  Click **Add a Whitelist Group**.
10. Click **Upload ECS Intranet IP Address**.
11. In the **Whitelist** field, move your mouse cursor on top of the first IP address.
12. A bubble appears. Move your mouse cursor on top of the **Instance Name** bubble field.
13. If the instance name is devops-simple-app-sonar, select this IP address. If not, repeat on the next IP address.
14. After you have selected exactly one IP address, set the group name devops\_simple\_app\_sonar\_wlg.
15. Click **OK** to close the pop-up window.

**Note:** The whitelist is a security feature: only the ECS instances in this list can access the database.

Let’s now create a database account and collect connection information:

1.  Click **Accounts** from the left-side navigation pane.
2.  Click **Create Initial Account**.
3.  Fill the form with the following information:
    -   Database Account = sonarqube
    -   Password = YourS0narP@ssword
    -   Re-enter Password = YourS0narP@ssword
4.  Click **OK** to create the account.
5.  Click **Connection Options** from the left-side navigation pane, and save the **Intranet Address** in the **Connection Information** section \(it should be something like r**m-gs5wm687b2e3uc770.pgsql.singapore.rds.aliyuncs.com**\).

## SonarQube installation {#section_g3t_2bn_qgb .section}

We can now install SonarQube. Open a terminal and enter the following commands:

```
# Connect to the ECS instance
ssh root@sonar.my-sample-domain.xyz # Use the password you set when you have created the ECS instance

# Update the machine
apt-get update
apt-get upgrade

# Install tools
apt-get install unzip default-jdk postgresql-client

# Connect to the database (use the "Intranet Address" you saved in the paragraph above)
psql postgresql://rm-gs5wm687b2e3uc770.pgsql.singapore.rds.aliyuncs.com:3433/postgres -U sonarqube
```

The new command line allows you to configure the PostgreSQL database:

```
-- Create a database
CREATE DATABASE sonarqube;

-- Quit
\q
```

Back to Bash, continue the installation:

```
# Create a Linux user for SonarQube
adduser --system --no-create-home --group --disabled-login sonarqube

# Create directories where we will put SonarQube files
mkdir /opt/sonarqube
mkdir -p /var/sonarqube/data
mkdir -p /var/sonarqube/temp

# Download and unzip SonarQube (LTS version)
cd /opt/sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-6.7.5.zip # URL from https://www.sonarqube.org/downloads/
unzip sonarqube-6.7.5.zip
rm sonarqube-6.7.5.zip

# Change the SonarQube file owner
chown -R sonarqube:sonarqube /opt/sonarqube
chown -R sonarqube:sonarqube /var/sonarqube

# Configure SonarQube
nano sonarqube-6.7.5/conf/sonar.properties
```

In the configuration file:

1.  Scroll to **\# User credentials**, uncomment and set the properties:
    -   sonar.jdbc.username=sonarqube
    -   sonar.jdbc.password=YourS0narP@ssword
2.  Scroll to **\#—– PostgreSQL 8.x or greater**, uncomment and set the property:
    -   sonar.jdbc.url=jdbc:postgresql://rm-gs5wm687b2e3uc770.pgsql.singapore.rds.aliyuncs.com:3433/sonarqube \# Set the **Intranet Address**
3.  Scroll to **\# WEB SERVER**, uncomment and set the property:
    -   sonar.web.javaAdditionalOpts=-server
4.  Scroll to **\# OTHERS**, uncomment and set the properties:
    -   sonar.path.data=/var/sonarqube/data
    -   sonar.path.temp=/var/sonarqube/temp

Save and quit by pressing CTRL + X, then continue the installation:

```
# Create a service file for Systemd
nano /etc/systemd/system/sonarqube.service
```

Copy the following content in this new file \(set the right path in “ExecStart” and “ExecStop”\):

```
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/opt/sonarqube/sonarqube-6.7.5/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/sonarqube-6.7.5/bin/linux-x86-64/sonar.sh stop

User=sonarqube
Group=sonarqube
Restart=always

[Install]
WantedBy=multi-user.target
```

Save and quit by pressing CTRL+X. Back to Bash, continue the installation:

```
# Start SonarQube
systemctl start sonarqube.service

# Wait few seconds and check it worked (the text must finish with "SonarQube is up")
cat sonarqube-6.7.5/logs/sonar.log

# You can also check that the following command returns some HTML
curl http://localhost:9000

# Configure SonarQube to automatically start when the machine reboot
systemctl enable sonarqube.service
```

Now that SonarQube is started, we need to configure a [reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy) to let users to connect to SonarQube via HTTPS. Enter the following commands in your terminal:

```
# Install Nginx and Let's Encrypt tooling
apt-get install software-properties-common
add-apt-repository ppa:certbot/certbot
apt-get update
apt-get install nginx python-certbot-nginx

# Configure Nginx to act as a reverse proxy for SonarQube
nano /etc/nginx/sites-available/sonarqube
```

Copy the following content in the new file \(set the correct “server\_name” according to your domain\):

```
server {
    listen 80;
    server_name sonar.my-sample-domain.xyz;

    location / {
        proxy_pass http://127.0.0.1:9000;
    }
}
```

Back to Bash, continue the installation:

```
# Enable the new configuration file
ln -s /etc/nginx/sites-available/sonarqube /etc/nginx/sites-enabled/sonarqube

# Disable the default Nginx configuration
rm /etc/nginx/sites-enabled/default

# Check the configuration syntax
nginx -t

# Start Nginx
systemctl start nginx
```

To check if the installation is successful, open a new web browser tab to `http://sonar.my-sample-domain.xyz/` \(adapt the URL for your domain\). If everything went well, you should see something like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799739341_en-US.png)

We now need to configure HTTPS. Enter the following commands in your terminal:

```
# Install the Let's Encrypt certificate (adapt for your domain)
certbot --nginx -d sonar.my-sample-domain.xyz
# Note: set your email address and accept the HTTP-to-HTTPS redirection

# The certificate will be automatically renewed. If you want, you can check the Cron configuration:
nano /etc/cron.d/certbot

# Check the renewal process with the following command
certbot renew --dry-run
# The logs should contain "Congratulations, all renewals succeeded" with your domain name (for example, sonar.my-sample-domain.xyz)

# Restart Nginx
systemctl restart nginx

# Configure Nginx to automatically start when the machine reboot
systemctl enable nginx
```

Refresh your web browser tab with SonarQube and check the URL: the protocol HTTPS must replace HTTP.

## SonarQube configuration {#section_r3t_2bn_qgb .section}

We now need to change the administrator password:

1.  Open your web browser tab with SonarQube \(URL like https://sonar.my-sample-domain.xyz/\).
2.  Click **Log in** on the top-right of the page.
3.  Fill the new form like this:
    -   Login = admin
    -   Password = admin
4.  Click **Log in**.
5.  Click your avatar on the top-right of the page and select **My Account**.
6.  Click **Security**.
7.  Change the password with the following values:
    -   Old Password = admin
    -   New Password = YourS0narQubeP@ssword
    -   Confirm Password = YourS0narQubeP@ssword
8.  Click **Change password**, and the message The **password has been changed!** is displayed.

Let’s create a normal user:

1.  Click **Administration** from the top.
2.  Click **Security** in the top-sub-menu and select **Users**.
3.  Click **Create User**.
4.  Fill the new form like this \(adapt the values\):
    -   Login = johndoe
    -   Name = John Doe
    -   Email = john.doe@your-company.com
    -   Password = JohnDoeP@ssw0rd
5.  Click **Create**.

Let’s now force users to log in in order to work on SonarQube:

1.  Click **Configuration** from the top-sub-menu and select **General Settings**.
2.  Click **Security** from the left-side navigation pane.
3.  Enable the switch in the **Force user authentication** property and confirm by clicking **Save**.

Now that user configuration is done, let’s create our quality gate \(the set of conditions to meet in order to let SonarQube to consider a code analysis as successful\):

1.  Click **Quality Gates** from the top.
2.  Click **SonarQube way** on the left panel.
3.  Click **Copy** on the top-right of the page.
4.  Set the name **Stricter SonarQube way** and click **Copy**.
5.  Add the following conditions \(by clicking **Add Condition** widget below the existing conditions\):
    -   Metric = Coverage, Operator = is less than, Error = 70
    -   Metric = Unit Test Errors, Operator = is not, Error = 0
    -   Metric = Unit Test Failures, Operator = is not, Error = 0
    -   Metric = Blocker Issues, Operator = is not, Error = 0
    -   Metric = Critical Issues, Operator = is not, Error = 0
    -   Metric = Major Issues, Operator = is not, Error = 0
6.  Do not forget to click **Add** next to the conditions you just added.
7.  Click **Set as Default** on the top-right of the page.

The quality gate should look like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799739349_en-US.png)

SonarQube is now ready! Let’s integrate it with our CI pipeline.

## Code analysis pipeline stage {#section_bjt_2bn_qgb .section}

The first step is to obtain a token from SonarQube:

1.  Open your web browser tab with SonarQube \(URL like https://sonar.my-sample-domain.xyz/\);
2.  If you are still logged in as **admin**, log out by clicking your avatar on the top-right of the page and select **Log out**.
3.  Login with your username and password \(do not use the **admin** user\).
4.  Click your avatar on the top-right of the screen and select **My Account**.
5.  Click **Security** from the top-sub-menu.
6.  Next to **Generate New Token**, set the name **todolist** and click **Generate**.
7.  You should see a new token appearing \(something like **cfe2e3d7d7a15df20e3ecb7de53b6a23b3757474**\).

**Note:** The following part of this section will modify two files: [pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) and [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/). You can see the results by browsing in the [sample-app/version2](https://github.com/alibabacloud-howto/devops/tree/master/tutorials/devops_for_small_to_medium_web_applications/sample-app/version2) folder.

The second step is to modify the [pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) file by adding two Maven plugins:

-   [JaCoCo](https://www.eclemma.org/jacoco/), used to analyze the code coverage of our unit tests.
-   [SonarQube](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven), used to communicate with our SonarQube server.

[JaCoCo](https://www.eclemma.org/jacoco/) is independent from SonarQube, it allows us to check which part of our code is covered by our tests. The following code contains the additions to our pom.xml file:

```
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <!-- ... -->
    <properties>
        <!-- ... -->
        <jacoco-maven-plugin.version>0.8.2</jacoco-maven-plugin.version>
        <!-- ... -->
    </properties>
    <!-- ... -->
    <build>
        <plugins>
            <!-- ... -->
            <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>${jacoco-maven-plugin.version}</version>
                <configuration>
                    <append>true</append>
                </configuration>
                <executions>
                    <execution>
                        <id>agent-for-ut</id>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>jacoco-site</id>
                        <phase>verify</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

JaCoCo Maven plugin is executed during the **verify** phase, which happens between **package** and **install**. After its execution, this plugin generates several files:

-   target/site/jacoco - A report containing coverage results in multiple formats \(HTML, XML and CSV\). You can check it by running `mvn clean install` from your project directory and by opening `target/site/jacoco/index.html` in your web browser.
-   target/jacoco.exec - Data used to generate the HTML, XML and CSV reports.

The SonarQube Maven plugin reads the reports generated by JaCoCo and [Surefire](https://maven.apache.org/surefire/maven-surefire-plugin/) \(the Maven plugin that runs our [JUnit](https://junit.org/) tests\). The following code contains the addition into our pom.xml file for this plugin:

```
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <!-- ... -->
    <properties>
        <!-- ... -->
        <sonar-maven-plugin.version>3.5.0.1254</sonar-maven-plugin.version>
        <sonar.sources>src/main/java,src/main/js,src/main/resources</sonar.sources>
        <sonar.exclusions>src/main/resources/static/built/*</sonar.exclusions>
        <sonar.coverage.exclusions>src/main/js/**/*</sonar.coverage.exclusions>
        <!-- ... -->
    </properties>
    <!-- ... -->
    <build>
        <plugins>
            <!-- ... -->
            <plugin>
                <groupId>org.sonarsource.scanner.maven</groupId>
                <artifactId>sonar-maven-plugin</artifactId>
                <version>${sonar-maven-plugin.version}</version>
            </plugin>
        </plugins>
    </build>
</project>
```

This plugin is not automatically executed when running `mvn clean install`. You can run it **manually** with the following command:

```
mvn clean install sonar:sonar \
    -Dsonar.host.url=https://sonar.my-sample-domain.xyz \
    -Dsonar.login=cfe2e3d7d7a15df20e3ecb7de53b6a23b3757474 \
    -Dsonar.branch=master \
    -Dmaven.test.failure.ignore=true
```

As you can see, the plugin needs to be configured with the following properties:

-   `sonar.host.url` must be set to your SonarQube server URL.
-   `sonar.login` must contain the token that SonarQube generated for you.
-   `sonar.branch` must contain the Git branch name. Please note that this feature is working but deprecated in SonarQube version 6.x \(and removed in the version 7.x\). It is now replaced by `sonar.branch.name` and `sonar.branch.target`. However, this functionality is not free anymore. You can read [the official documentation](https://docs.sonarqube.org/latest/branches/overview/) if you are interested in purchasing [the Developer Edition](https://www.sonarsource.com/plans-and-pricing/developer/). A cheaper alternative for the versions 7.x is to set the `sonar.projectKey` property with a name that contains the branch name.
-   `maven.test.failure.ignore` must be set to `true` to run the SonarQube analysis even when some tests fail.

The third step is to modify the [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/) file with the following changes:

```
image: maven:3.6.0-jdk-8

variables:
  MAVEN_OPTS: "-Dmaven.repo.local=./.m2/repository"
  SONAR_URL: "https://your_sonarqube.url"
  SONAR_LOGIN: "token_generated_by_sonarqube"

cache:
  paths:
    - ./.m2/repository
    - ./.sonar/cache

stages:
  - build
  - quality

build:
  stage: build
  script: "mvn package -DskipTests=true"

quality:
  stage: quality
  script:
    - "mvn clean install sonar:sonar -Dsonar.host.url=$SONAR_URL -Dsonar.login=$SONAR_LOGIN -Dsonar.branch=$CI_COMMIT_REF_NAME -Dmaven.test.failure.ignore=true -Duser.home=."
    - "wget https://github.com/gabrie-allaigre/sonar-gate-breaker/releases/download/1.0.1/sonar-gate-breaker-all-1.0.1.jar"
    - "java -jar sonar-gate-breaker-all-1.0.1.jar -u $SONAR_LOGIN"
  artifacts:
    paths:
      - target/*.jar
```

This file contains the following modifications:

-   A new stage **quality** has been added under the `stages` block.
-   The `build` block has been simplified: the unit test execution has been disabled thanks to the `-DskipTests=true` parameter, and the `artifacts` block has been removed.
-   The new `quality` block contains 3 commands: the first one runs the unit tests and launch the SonarQube analysis, and the second and third ones wait for the analysis to complete and break the pipeline if there is a problem \(for example, a unit test failed or the quality gate is not respected\).
-   Two `variables` have been added:
    -   SONAR\_URL will contain the URL to your SonarQube server.
    -   SONAR\_LOGIN will contain the generated SonarQube token.

Before committing these two files, we need to properly set the `SONAR_URL` and `SONAR_LOGIN` variables:

1.  Open GitLab \(the URL must be like https://gitlab.my-sample-domain.xyz/\).
2.  Sign in if necessary;
3.  Click **Projects** in the top menu and select **Your projects**.
4.  Click the **todolist** project.
5.  In the left-side navigation pane, select **Settings** \> **CI/CD**.
6.  Expand the **Variables** panel, and create the following variables:
    -   SONAR\_URL = your SonarQube server URL \(for example, https://sonar.my-sample-domain.xyz\)
    -   SONAR\_LOGIN = your SonarQube token \(for example, cfe2e3d7d7a15df20e3ecb7de53b6a23b3757474\)
7.  Click **Save variables**.

You can now commit the two modified files and let GitLab to run your new pipeline! Please execute the following commands in your terminal:

```
# Go to the project folder
cd ~/projects/todolist

# Check the files to commit
git status

# Add the files
git add .gitlab-ci.yml pom.xml

# Commit the files and write a comment
git commit -m "Add a quality stage in the pipeline."

# Push the commit to the GitLab server
git push origin master
```

Check your new GitLab pipeline: in your GitLab web browser tab, click **CI/CD** from the left-side navigation pane. You should get something like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799739358_en-US.png)

As you can see, there is now two stages in the pipeline. You can click them to check detailed logs.

Have a look at your SonarQube server: open your web browser tab with SonarQube \(URL like https://sonar.my-sample-domain.xyz/\). You should see your project:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799739359_en-US.png)

Click your project name. You should see something like this:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839360_en-US.png)

Explore this interface by yourself, for example click on the coverage percentage: you will get a list of Java files with their coverage percentage. If you click one of these files you can see which line is covered and which one is not.

**Note:** Code coverage is a good indicator before you attempt to execute a major [code refactoring](https://en.wikipedia.org/wiki/Code_refactoring): like a safety net, a good code coverage means that you have a greater chance that your unit tests will catch bugs before they hit production.

## CI pipeline testing {#section_ujt_2bn_qgb .section}

Let’s break our pipeline!

Let’s start with a unit test:

```
# Go to the project folder
cd ~/projects/todolist

# Open a test file
nano src/test/java/com/alibaba/intl/todolist/controllers/TaskControllerTest.java
```

At the line 87 of this file, change:

```
assertEquals("Task 2", createdTask2.getDescription());
```

Into:

```
assertEquals("Task 2222222222", createdTask2.getDescription());
```

Save by pressing CTRL + X, then commit the change:

```
# Check the files to commit
git status

# Add the file
git add src/test/java/com/alibaba/intl/todolist/controllers/TaskControllerTest.java

# Commit the file and write a comment
git commit -m "Break a unit test on purpose."

# Push the commit to the GitLab server
git push origin master
```

Have a look at your GitLab pipeline:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839361_en-US.png)

And your SonarQube project:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839362_en-US.png)

Let’s now fix the test:

```
# Open the file to fix
nano src/test/java/com/alibaba/intl/todolist/controllers/TaskControllerTest.java
```

Restore the the line 87 \(set T**ask 2** instead of **Task 2222222222**\), save with CTRL + X, and commit:

```
# Check the files to commit
git status

# Add the file
git add src/test/java/com/alibaba/intl/todolist/controllers/TaskControllerTest.java

# Commit the file and write a comment
git commit -m "Fix the unit test."

# Push the commit to the GitLab server
git push origin master
```

Your GitLab pipeline and SonarQube project should be successful.

Now let’s break something else:

```
# Open another file to break
nano src/main/java/com/alibaba/intl/todolist/controllers/MachineController.java
```

Insert the following lines at the end of the class \(line 71, before the last brace\):

```
private String dummy = "example";

    public synchronized String getDummy() {
        return dummy;
    }

    public void setDummy(String dummy) {
        this.dummy = dummy;
    }
```

Save with CTRL + X and continue:

```
# Check the files to commit
git status

# Add the file
git add src/main/java/com/alibaba/intl/todolist/controllers/MachineController.java

# Commit the file and write a comment
git commit -m "Add a potential data race issue."

# Push the commit to the GitLab server
git push origin master
```

Have a look at your GitLab pipeline:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839363_en-US.png)

And your SonarQube project:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839364_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123240/155324799839365_en-US.png)

This time the problem comes from a bug inside the code.

**Note:** Thread-safety issues are usually quite hard to fix because the bugs are not easy to reproduce.

Let’s fix the code:

```
# Open the file to fix
nano src/main/java/com/alibaba/intl/todolist/controllers/MachineController.java
```

Remove the added lines \(starting from line 71\), then save with CTRL + X and continue:

```
# Check the files to commit
git status

# Add the file
git add src/main/java/com/alibaba/intl/todolist/controllers/MachineController.java

# Commit the file and write a comment
git commit -m "Fix the potential data race issue."

# Push the commit to the GitLab server
git push origin master
```

The GitLab pipeline and SonarQube project should be green again.

