# 如何为Linux服务器安装GRUB {#concept_222285 .concept}

通过迁云工具迁移Linux源服务器时，若Linux源服务器的内核版本较低（如CentOS 5和Debian 7）、自带的系统引导程序GRUB（ GRand Unified Bootloader）版本低于1.99，日志文件提示Do Grub Failed时，您需要将GRUB升级至1.99及以上版本。

## 安装GRUB {#section_318_zck_gn7 .section}

本文以GRUB 1.99版本为例，介绍在Linux服务器上安装系统引导程序GRUB的操作步骤。安装GRUB 1.99以上版本的操作步骤与此相同，主要差异在于安装过程中需[下载相应版本的GRUB源码包](https://alpha.gnu.org/gnu/grub/)。

1.  登录Linux源服务器。
2.  依次运行以下命令查看原grub、grub-install 以及 grub-mkconfig的路径：

    ``` {#codeblock_mtc_wae_09v}
    # which grub
    # which grub-install
    # which grub-mkconfig
    ```

3.  使用`mv`命令为旧版本grub、grub-install 以及 grub-mkconfig改名以备份文件。您可以在使用迁云工具迁移服务器后，恢复原名以使用原配置。

    ``` {#codeblock_nmk_42b_4bf}
    # mv /sbin/grub /sbin/grub-old
    # mv /sbin/grub-install /sbin/grub-install-old 
    # mv /sbin/grub-mkconfig /sbin/grub-mkconfig-old
    ```

4.  运行`yum install -y bison gcc make`安装GRUB依赖的bison、gcc以及make工具。
5.  依次运行以下命令安装flex。

    ``` {#codeblock_r6c_dbw_bys}
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

6.  依次运行以下命令安装GRUB 1.99依赖。

    ``` {#codeblock_5ru_kgc_2q0}
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

    **说明：** 若编译过程中出现了`-Werror`报错，您可以定位到编译对象的编译文件makefile中，去掉`-Werror`选项重新编译。

7.  运行`grub-install --version`命令，检查GRUB版本是否更新为1.99。

## 下一步 {#section_4ps_1tm_q1f .section}

1.  成功更新系统引导程序GRUB为1.99版本后，您可以使用[使用迁云工具迁移服务器至阿里云](../../../../cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)。
2.  （可选）迁云成功后，运行以下命令将GRUB恢复为旧版本：

    ``` {#codeblock_pz8_1xf_7ay}
    # rm /sbin/grub-install
    # rm /sbin/grub-mkconfig
    # rm /boot/grub/grub.cfg
    # mv /sbin/grub-old /sbin/grub
    # mv /sbin/grub-install-old /sbin/grub-install
    ```


