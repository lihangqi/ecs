# Upgrades {#ApiUpgrade .reference}

## Product upgrades {#Upgrade .section}

max\{20, current system disk capacity\}

\[max\{20, \[the size of the specified image file\]\}, 500\]

It is a string of 2 to 128 characters. It must begin with an English or a Chinese character and can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

-   Cloud: Basic cloud disk.
-   cloud\_efficiency: Ultra cloud disk.
-   cloud\_ssd: SSD Cloud Disks.
-   ephemeral\_ssd: Ephemeral SSD.

-   cloud: \[5, 2000\]
-   cloud\_efficiency: \[20, 32768\]
-   cloud\_ssd: \[20, 32768\]
-   ephemeral\_ssd: \[5, 800\]

The key of a tag of which n is from 1 to 20. Once you use this parameter, it cannot be a null string. It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://". The value of a tag of which n is a number from 1 to 20. Once you use this parameter, it can be a null string. It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".

The password can be \[8, 30\] characters in length. It must contain uppercase letters, lowercase letters, and numbers. The following special characters are allowed: \(\)\`~! @\#$%^&amp;\*-+=|\{\}\[\]:;‘&lt;\>,.? /

The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

It cannot begin with http:// or https://.

-   It cannot start or end with a period \(.\) or a hyphen \(-\) and it cannot have two or more consecutive periods \(.\) or hyphens \(-\).
-   For Windows: The host name can be \[2, 15\] characters in length. It can contain A-Z, a-z, numbers, periods \(.\), and hyphens \(-\). It cannot only contain numbers.
-   For other operating systems: The host name can be \[2, 64\] characters in length. It can be segments separated by periods \(.\). It can contain A-Z, a-z, numbers, and hyphens \(-\).

