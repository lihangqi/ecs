# How do I enable or disable the Meltdown and Spectre patches for Linux images? {#KnownIssueMeltdownSpectre2018 .concept}

This topic describes how Alibaba Cloud ECS responds to the Meltdown and Spectre vulnerabilities. You can learn about our measures for protecting ECS instances against these vulnerabilities.

## Context {#section_skt_htn_2gb .section}

The Meltdown and Spectre vulnerabilities exist in the Intel chips. Caused by the design flaw of the chip hardware, the vulnerabilities may lead to problems such as leakage of operating system kernel information, unauthorized access to system kernel data by applications, and more. You can go to the CVE website to check the vulnerability IDs:

-   [CVE-2017-5753](http://t.cn/E48m0VZ)
-   [CVE-2017-5715](http://t.cn/E48mmqP)
-   [CVE-2017-5754](http://t.cn/E48uvUp)

On January 20, 2018, Alibaba Cloud released a [security vulnerability notice](https://www.alibabacloud.com/help/faq-detail/64951.htm), describing the vulnerability details and impacts.

This topic describes the Alibaba Cloud public images that have been patched against these vulnerabilities, and how to disable the patches for better instance performance. The default security policy is as follows:

-   To protect against the Meltdown vulnerability, Page Table Isolation \(PTI\) is enabled by default.
-   To protect against the Spectre vulnerability, by default No Indirect Branch Restricted Speculation \(NOIBRS\) is enabled and is integrated with Retpoline and Indirect Branch Prediction Barriers \(IBPB\).

## How to enable or disable the Meltdown patch {#section_v3p_3tn_2gb .section}

The following public images have enabled the Meltdown patch \(PTI On\):

-   CentOS 7.5/7.6
-   Debian 9.6/8.10
-   Red Hat 7.5/7.6
-   SUSE Linux 15
-   Ubuntu 18.04
-   CoreOS 1911.3.0
-   FreeBSD 11.2
-   OpenSUSE 15

The above list is subject to change due to updates of Alibaba Cloud public images.

If you find enabling PTI impacts your instance performance, or you have other protective measures, you can disable PTI by following the steps below:

1.  Connect to your instance.
2.  Do the following according to your Linux distribution:
    -   CentOS, Debian, OpenSUSE, Red Hat, SUSE Linux and Ubuntu: Add the kernel parameter `nopti`.
    -   CoreOS: Run `vi /usr/share/oem/grub.cfg` to configure `pti=off`.
    -   FreeBSD: Run `vi /boot/loader.conf` to configure `vm.pmap.pti=0`.
3.  Restart the instance.

## How to enable or disable the Spectre patch {#section_orl_jtn_2gb .section}

Alibaba Cloud currently allows you to configure Indirect Branch Restricted Speculation \(IBRS\) and IBPB. By default, public images are protected against Spectre through Reptpoline and IBPB. Moreover, IBRS is disabled through the noibrs parameter. The following public images are involved:

-   CentOS 7.5/7.6
-   Debian 9.6/8.10
-   Red Hat 7.5/7.6
-   SUSE Linux 15
-   Ubuntu 18.04
-   CoreOS 1911.3.0
-   FreeBSD 11.2
-   OpenSUSE 15

The above list is subject to change due to updates of Alibaba Cloud public images.

If you need to restore the default settings of your operating system, or you find the current settings impact your instance performance, or you have other protective measures, you can disable the Spectre patch by following the steps below:

1.  Connect to your instance.
2.  Perform the corresponding operation according to the instructions in the following table.

    |Linux distribution|To restore the default settings of Alibaba Cloud images|To restore the default settings of operating systems|To disable the Spectre patch|
    |:-----------------|:------------------------------------------------------|:---------------------------------------------------|:---------------------------|
    |CentOS|Add the kernel parameter noibrs.|Remove the kernel parameter noibrs.|Add the kernel parameter spectre\_v2=off.|
    |Red Hat|
    |CoreOS|Run `vi /usr/oem/share/grub.cfg` to add the kernel parameter spectre\_v2=off.|Remove the kernel parameter spectre\_v2=off.|
    |OpenSUSE|Add the kernel parameter spectre\_v2=off.|
    |Debian|Retpoline and IBPB are enabled by default.|No need to modify the settings.|
    |Ubuntu|
    |SUSE Linux|Retpoline is enabled by default.|
    |FreeBSD|Add the kernel parameter hw.ibrs\_disable.|Remove the kernel parameter hw.ibrs\_disable.|Add the kernel parameter hw.ibrs\_disable.|

    **Note:** The kernel parameter `noibrs` does not work for OpenSUSE and CoreOS. You need to set `spectre_v2=off` for them.

3.  Restart the instance.

## How to detect whether protections are enabled {#section_twp_ktn_2gb .section}

1.  Connect to your instance.
2.  From [GitHub spectre-meltdown-checker Repo](https://github.com/speed47/spectre-meltdown-checker), obtain the spectre-meltdown-checker.sh script.
3.  Run the following commands in your instance:

    ``` {#codeblock_av3_160_ghf}
    chmod +x spectre-meltdown-checker.sh
    sudo bash spectre-meltdown-checker.sh
    ```

4.  Judge whether the Meltdown or Spectre patch has been enabled according to the script prompts.

## Reference {#section_dkd_ltn_2gb .section}

For the following operating systems, you can go to their website for more details:

-   [Red Hat](https://access.redhat.com/articles/3311301)
-   [SUSE Linux](https://www.suse.com/support/kb/doc/?id=7022512)
-   [Ubuntu](https://wiki.ubuntu.com/SecurityTeam/KnowledgeBase/SpectreAndMeltdown/MitigationControls)

