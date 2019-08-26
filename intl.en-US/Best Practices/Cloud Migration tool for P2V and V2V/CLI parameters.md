# CLI parameters {#CliParams .reference}

The Cloud Migration tool supports command line interface \(CLI\) parameters for version 1.2.8 and later. Run the `--help` command in the path of the Cloud Migration tool to view the list of the parameters. You can configure the Cloud Migration tool, adjust user-defined usage habits, and clear the client\_data file with one click. No need to open the various JSON files. If you are using a version earlier than 1.2.8 of the Cloud Migration tool, [download the compressed package file](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip) for a better experience. To use CLI parameters, you must have some prior knowledge of the migration tool. To learn more about the tool, see the usage of the [Cloud Migration tool](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

## Cloud Migration tool parameters for Windows {#section_tnt_qy1_kfb .section}

A complete list of CLI parameters of the Cloud Migration tool for Windows is as follows:

```
usage: go2aliyun_client.exe [options]
options:
  --help                        show usage.
  --version                     show version.
  --nocheckversion              no check for new version.
  --noenterkey                  no enter key to exit.
  --progressfile                set progress file path.
  --cleardata                   clear client data and server ecs.
  --accesssid=<accesss_id>      set access id.
  --secretkey=<secret_key>      set secret key.
  --regionid=<region_id>        set region id.
  --imagename=<image_name>      set image name.
  --systemdisksize=<sdsize>     set system disk size.
  --platform=<platform>         set platform.
  --architecture=<arch>         set architecture.
  --datadisks=<data_disks>      set data disks.
    data_disks=data_disk_index|data_disk_size|src_path;
    e.g. --data_disks=1|100|D:;2|150|E:
  --bandwidthlimit=<limit>      set bandwidth limit.
  --netmode=<net_mode>          set net mode.
  --vpcid=<vpc_id>              set vpc id.
  --vswitchid=<vswitch_id>      set vswitch id.
  --zoneid=<zone_id>            set zone id.
  --securegroupid=<sgid>        set secure group id.
```

## Cloud Migration tool parameters for Linux {#section_j4t_qy1_kfb .section}

A complete list of CLI parameters of the Cloud Migration tool for Linux is as follows:

```
usage: ./go2aliyun_client [options]
options:
  --help                       show usage.
  --version                    show version.
  --nocheckversion             no check for new version.
  --noenterkey                 no enter key to exit.
  --progressfile               set progress file path. 
  --cleardata                  clear client data and server ecs.
  --accesssid=<accesss_id>     set access id.
  --secretkey=<secret_key>     set secret key.
  --regionid=<region_id>       set region id.
  --imagename=<image_name>     set image name.
  --systemdisksize=<sdsize>    set system disk size.
  --platform=<platform>        set platform.
  --architecture=<arch>        set architecture.
  --datadisks=<data_disks>     set data disks.
    data_disks=data_disk_index|data_disk_size|src_path;
    e.g. --data_disks=1|100|/mnt/disk1;2|150|/mnt/disk2
  --bandwidthlimit=<limit>     set bandwidth limit.
  --netmode=<net_mode>         set net mode.
  --vpcid=<vpc_id>             set vpc id.
  --vswitchid=<vswitch_id>     set vswitch id.
  --zoneid=<zone_id>           set zone id.
  --securegroupid=<sgid>       set secure  group id.
```

## General parameters {#section_z4t_qy1_kfb .section}

The general parameters of the Cloud Migration tool for both Windows and Linux are as follows: General parameters are usually used for adjusting usage habits and interactive interfaces of the Cloud Migration tool. They do not affect configurations of the tool or the cloud migration process.

|Parameters|Description|
|----------|-----------|
|nocheckversion|The migration tool stops version update reminds.|
|noenterkey|The migration tool does not give a prompt before completion. Instead, it exits directly.|
|progressfile|Sets the migration progress output file. The file contains two rows in the following format:-   The first row contains one of the four progress indicators: `PrepareForRsync` \(data transmission preparation stage\), `DoRsync` \(data transmission stage\), `CreateImage` \(image creation stage\), and `Finished` \(cloud migration finished stage\).
-   The second row contains the progress value, which shows the progress of each stage. The value is an Integer ranging from 0 to 100.

|
|cleardata|Clears the client\_data file and releases the ****`Running` intermediate instance.|

**Warning:** Do not use the `cleardata` parameter before your cloud migration job is complete. Otherwise, the cloud migration are interrupted and the migration progress becomes invalid.

## User\_config parameters {#section_fpt_qy1_kfb .section}

The relevant CLI parameters for user\_config configuration are as follows. For more information about user\_config, see [the usage of the Cloud Migration tool](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

**Note:** After you use CLI parameters to configure user\_config, the Cloud Migration tool uses your new configuration and ignores the configuration file.

```
--accesssid=<accesss_id>     # Sets AccessKey ID in user_config.
--secretkey=<secret_key>     # Sets AccessKey Secret in user_config.
--regionid=<region_id>       # Sets Region ID in user_config.
--imagename=<image_name>     # Sets user-defined image name in user_config.
--systemdisksize=<sdsize>    # Sets system disk capacity in user_config.
--platform=<platform>        # Sets the mapping image releasing platform in user_config.
--architecture=<arch>        # Sets the image architecture in user_config.
--datadisks=<data_disks>     # Sets data disks in user_config. Disk values are separated by vertical bars (|) and semicolons (;), for example, data_disk_index|data_disk_size|src_path;
--bandwidthlimit=<limit>     # Sets the upper limit of the public network outbound bandwidth in user_config.
```

## Client\_data parameters {#section_opt_qy1_kfb .section}

The following section describes relevant parameters for cloud migration through VPC intranet. For more information, see [VPC Intranet Network Cloud Migration](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Cloud migration through VPC intranet.md#).

```
--netmode=<net_mode>        # Sets cloud migration method in client_data. The values can be 0, 1, or 2.
--vpcid=<vpc_id>            # Sets the VPC that has configured Express Connect or VPN Gateway in client_data.
--vswitchid=<vswitch_id>    # Sets the VSwitch under the VPC in client_data.
--securegroupid=<sgid>      # Sets the security group under the VPC in client_data.
```

