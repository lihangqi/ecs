# Install GRUB v1.99 in a Linux server {#concept_222285 .concept}

This topic describes how to install GRand Unified Bootloader \(GRUB\) in a Linux server by using GRUB v1.99 as an example. To install GRUB of a later version, you need to [download the relevant GRUB package](https://alpha.gnu.org/gnu/grub/).

## Background information {#section_btt_xpm_vhb .section}

When you migrate a source Linux server by using the Cloud Migration tool, if the source Linux server has a low kernel version \(such as CentOS 5 and Debian 7\), and the version of the built-in system boot program GRUB is lower than v1.99, the log file indicates `Do Grub Failed`. In this case, you need to upgrade GRUB to v1.99 or later.

## Procedure {#section_318_zck_gn7 .section}

1.  Log on to the source Linux server.
2.  Run the following commands to view the directories of the original grub, grub-install, and grub-mkconfig:

    ``` {#codeblock_u5w_ycu_1y9}
    # which grub
    # which grub-install
    # which grub-mkconfig
    ```

3.  Run the `mv` command to rename the original grub, grub-install, and grub-mkconfig files for backup.

    **Note:** After you migrate your server by using the Cloud Migration tool, you can reinstate the original files by changing their names back to the original ones.

    ``` {#codeblock_ba6_oa2_cx1}
    # mv /sbin/grub /sbin/grub-old
    # mv /sbin/grub-install /sbin/grub-install-old 
    # mv /sbin/grub-mkconfig /sbin/grub-mkconfig-old
    ```

4.  Run the `yum install -y bison gcc make` command to install the dependencies of GRUB, which include bison, gcc, and make.
5.  Run the following commands to install flex.

    ``` {#codeblock_4p3_aw9_73n}
    # test -d /root/tools || mkdir -p /root/tools
    # cd /root/tools
    # wget https://github.com/westes/flex/releases/download/v2.6.4/flex-2.6.4.tar.gz
    # tar xzf flex-2.6.4.tar.gz
    # cd flex-2.6.4
    # mkdir -p build
    # cd build
    # ../configure
    # make && make install
    # ln -s /usr/local/bin/flex /usr/bin/flex
    ```

6.  Run the following commands to install the dependencies of GRUB v1.99.

    ``` {#codeblock_c8h_65w_d6n}
    # test -d /root/tools || mkdir -p /root/tools
    # cd /root/tools
    # wget https://alpha.gnu.org/gnu/grub/grub-1.99~rc1.tar.gz
    # tar xzf grub-1.99~rc1.tar.gz
    # cd grub-1.99~rc1
    # mkdir -p build
    # cd build
    # ../configure
    # sed -i -e "s/-Werror//" ./grub-core/Makefile
    # sed -i -e "s/-Werror//" ./Makefile
    # make && make install
    # ln -s /usr/local/sbin/grub-install /sbin/grub-install
    # ln -s /usr/local/sbin/grub-mkconfig /sbin/grub-mkconfig
    ```

    **Note:** If the error `-Werror` occurs, we recommend that you locate the error in the makefile, remove the `-Werror` option, and then try again.

7.  Run the `grub-install --version` command to verify GRUB is updated to v1.99.

## What to do next {#section_4ps_1tm_q1f .section}

1.  After you update GRUB to v1.99, you can [migrate your server to Alibaba Cloud by using the Cloud Migration tool](../../../../intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).
2.  \(Optional\) After your servers are successfully migrated to Alibaba Cloud, run the following commands to use the earlier version of GRUB.

    ``` {#codeblock_z7t_4xi_u39}
    # rm /sbin/grub-install
    # rm /sbin/grub-mkconfig
    # rm /boot/grub/grub.cfg
    # mv /sbin/grub-old /sbin/grub
    # mv /sbin/grub-install-old /sbin/grub-install
    ```


