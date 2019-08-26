# Known issues {#concept_e3m_ktl_jgb .concept}

This topic describes the known issues and corresponding fixes of Alibaba Cloud images for different operating systems.

## Debian: Classic network configuration issues {#section_zyc_kxl_jgb .section}

-   **Issue**: IP addresses cannot be automatically assigned to classic network instances through Dynamic Host Configuration Protocol \(DHCP\), because the Debian system disables the systemd-networkd service by default.
-   **Image ID**: debian\_9\_06\_64\_20G\_alibase\_20181212.vhd
-   **Fix**: Run the following commands to resolve the issue.

    ```
    systemctl enable systemd-networkd
    systemctl start systemd-networkd
    ```


