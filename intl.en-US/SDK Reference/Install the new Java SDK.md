# Install the new Java SDK {#concept_34917_zh .concept}

Earlier versions of Java SDKs were downloadable as standalone packages, while the new Alibaba Cloud Java SDKs are distributed through Maven. All the Java SDKs of Alibaba Cloud are located in the same Maven repository for easy management.

## Download Maven {#section_dwn_tvm_2gb .section}

Go to the [official Maven download page](http://maven.apache.org/download.cgi), and download the Maven software that corresponds to your operating system. You can verify the downloaded files by checking the Checksum files. The following screenshot is from the Windows 7 64-bit operating system, and the development environment is Eclipse Luna.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/155065310413402_en-US.png)

## Install Java SDKs {#section_dg4_vvm_2gb .section}

1.  Go to the [Java SDK download page](http://develop.aliyun.com/sdk/java), and add the Maven repository storing Alibaba Cloud SDKs to the Maven software.

2.  Decompress the downloaded Maven package, and add the following Maven repository information to the settings.xml file in the conf directory.

```
<repositories>
	<repository>
		<id>sonatype-nexus-staging</id>
		<name>Sonatype Nexus Staging</name>
		<url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
		<releases>
			<enabled>true</enabled>
		</releases>
		<snapshots>
			<enabled>true</enabled>
		<snapshots>
	</repository>
</repositories>
```

3.  Create a Maven project in either of the following ways:

-   Method 1: Add a Maven project to Eclipse.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/155065310413404_en-US.png)

-   Method 2: Convert an existing project to a Maven project.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/155065310413405_en-US.jpg)

4.  Add dependencies to the Maven project in either of the following ways:

-   Method 1: Add the selected dependencies through the graphical interface.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/155065310413406_en-US.jpg)

-   Method 2: Open the pom.xml file under the maven project, and add information similar to the following: You can add different dependencies as needed.

    ```
    <dependencies>
    	<dependency>
    		<groupId>com.aliyun</groupId>
    		<artifactId>aliyun-java-sdk-core</artifactId>
    		<version>2.1.6</version>
    	</dependency>
    	<dependency>
    		<groupId>com.aliyun</groupId>
    		<artifactId>aliyun-java-sdk-sts</artifactId>
    		<version>2.1.0</version>
    	</dependency>
    	<dependency>
    		<groupId>com.aliyun</groupId>
    		<artifactId>aliyun-java-sdk-yundun</artifactId>
    		<version>2.1.3</version>
    	</dependency>
    	<dependency>
    		<groupId>com.aliyun</groupId>
    		<artifactId>aliyun-java-sdk-slb</artifactId>
    		<version>2.0.0-rc1</version>
    	</dependency>
    </dependencies>
    ```

5.  Save the changes. The corresponding Alibaba Cloud SDK JAR packages are automatically downloaded and added to the Maven dependencies.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/155065310413408_en-US.jpg)


## How to distinguish old SDKs from new SDKs { .section}

If you are using an earlier version of SDK, we recommend that you switch to the latest version to explore its new features. The following table shows the differences between old SDKs and new SDKs.

|Item|Earlier SDK|New SDKs|
|:---|:----------|:-------|
|How to submit a request|execute\(\)|getAcsResponse\(\)|
|How to store the classes of AccessKey and AccessKeySecret|AliyunClient|IClientProfile|
|How to store the credential objects|new DefaultAliyunClient\(APIUrl, Access Key, Access Key Secret\)|DefaultProfile.getProfile\(RegionId, Access Key, Access Key Secret\)|
|Package prefix|com.aliyun.api|com.aliyuncs|

