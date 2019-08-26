# Vim教程 {#concept_188767 .concept}

Vim是从vi发展而来的文本编辑器，可以用颜色或底线等方式来显示一些特殊的信息。Vim是Linux中必不可少的工具，搭建网站修改配置文件时经常用到。本教程介绍Vim的模式和常用操作。

## Vim模式 {#section_u9e_ujf_y2m .section}

|模式|作用|模式转换|
|--|--|----|
|普通模式 （Normal Mode）

 |在该模式下，您可以复制、粘贴、删除字符或行。| -   运行`vim <文件名>`打开文件时，即进入普通模式。
-   在其他四个模式下，按`Esc`键即进入普通模式。

 |
|插入模式 （Insert Mode）

 |在该模式下，您可以插入字符。|在普通模式下，按`i,I,a,A,o,O`中任一字符即进入插入模式。 **说明：** 进入插入模式后，编辑器左下角会显示`-- INSERT --`。

 |
|替换模式 （Replace Mode）

 |在该模式下，您可以替换字符。|在普通模式下，按`R`即进入替换模式。 **说明：** 进入替换模式后，编辑器左下角会显示`-- REPLACE --`。

 |
|可视模式 （Visual Mode）

 |在该模式下，您可以选择文本。命令（如，复制、替换、删除等）仅作用于选中的文档。|在普通模式下，按`v`即进入可视模式。 **说明：** 进入可视模式后，编辑器左下角会显示`-- VISUAL --`。

 |
|命令模式 （Command Mode）

 |在该模式下，您可以查找字符串、替换字符串、显示行号、保存修改、退出编辑器等。|在普通模式下，按`:`即进入命令模式。|

## 插入 {#section_tr1_ny1_buk .section}

 **基本命令** 

-   i：在当前字符的左边插入。
-   I：在当前行的行首插入 。
-   a：在当前字符的右边插入。
-   A：在当前行的行尾插入。
-   o：在当前行下面插入一个新行。
-   O：在当前行上面插入一个新行。

 **示例** 

本示例中使用的example.conf文件，如下所示：

``` {#codeblock_x1k_glz_ckt}
# To be able to use the functionality of a module which was built as a DSO you
# have to place corresponding `LoadModule' lines at this location so the
# directives contained in it are actually available _before_ they are used.
# Statically compiled modules (those listed by `httpd -l') do not need
# to be loaded here.
#
# Example:
# LoadModule foo_module modules/mod_foo.so
#
Include conf.modules.d/*.conf			
```

例1：在配置文件example.conf的第一行，插入`Location`。步骤如下：

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  按`i`进入插入模式。
3.  输入`Location`。
4.  按回车键换行。
5.  按`Esc`键退出插入模式。
6.  按`:wq`保存文件并退出。

    插入完成后，example.conf文件如下所示：

    ``` {#codeblock_bro_cl9_h9w}
    Location
    # To be able to use the functionality of a module which was built as a DSO you
    # have to place corresponding `LoadModule' lines at this location so the
    # directives contained in it are actually available _before_ they are used.
    # Statically compiled modules (those listed by `httpd -l') do not need
    # to be loaded here.
    #
    # Example:
    # LoadModule foo_module modules/mod_foo.so
    #
    Include conf.modules.d/*.conf			
    ```


例2：在配置文件example.conf第十行的行首，插入`#`。步骤如下：

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  按`:10`将光标定位到第10行。
3.  按`I`进入插入模式。
4.  输入`#`。
5.  按`Esc`键退出插入模式。
6.  按`:wq`保存文件并退出。

    插入操作完成后，example.conf文件如下所示：

    ``` {#codeblock_i6k_pyq_yjx}
    # To be able to use the functionality of a module which was built as a DSO you
    # have to place corresponding `LoadModule' lines at this location so the
    # directives contained in it are actually available _before_ they are used.
    # Statically compiled modules (those listed by `httpd -l') do not need
    # to be loaded here.
    #
    # Example:
    # LoadModule foo_module modules/mod_foo.so
    #
    #Include conf.modules.d/*.conf		
    ```


例3：在配置文件example.conf中，在`Include conf.modules.d/*.conf`行的下一行插入`LoadModule rewrite_module modules/mod_rewrite.so`。步骤如下：

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  运行`/Include conf.modules.d/*.conf`找到目标行。
3.  按`o`进入插入模式。
4.  输入`LoadModule rewrite_module modules/mod_rewrite.so`。
5.  按`Esc`键退出插入模式。
6.  按`:wq`保存文件并退出。

    插入完成后，example.conf文件如下所示：

    ``` {#codeblock_pog_fe4_zys}
    # To be able to use the functionality of a module which was built as a DSO you
    # have to place corresponding `LoadModule' lines at this location so the
    # directives contained in it are actually available _before_ they are used.
    # Statically compiled modules (those listed by `httpd -l') do not need
    # to be loaded here.
    #
    # Example:
    # LoadModule foo_module modules/mod_foo.so
    #
    Include conf.modules.d/*.conf
    LoadModule rewrite_module modules/mod_rewrite.so							
    ```


## 替换 {#section_tq7_lnt_5in .section}

 **基本命令** 

R：替换光标高亮的字符，直至按下`Esc`键退出替换模式。

 **示例** 

本示例使用的example.conf文件，如下所示：

``` {#codeblock_4ll_e6h_c6q}
# AllowOverride controls what directives may be placed in .htaccess files.
# It can be "All", "None", or any combination of the keywords:
#   Options FileInfo AuthConfig Limit
#
AllowOverride None				
```

例：将配置文件example.conf中的`AllowOverride None`更改为`AllowOverride All`。

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  运行`/AllowOverride None`找到目标。
3.  移动光标至`None`的首字母。
4.  按`R`进入替换模式。
5.  输入`All`和一个空格。

    **说明：** `None`中共包含4个字符，而`All`只包含3个字符，因此输入All之后，需再输入一个空格。

6.  按`Esc`键退出替换模式。
7.  按`:wq`保存文件并退出。

    更改后的example.conf文件，如下所示：

    ``` {#codeblock_dd0_djk_dzz}
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   Options FileInfo AuthConfig Limit
    #
    AllowOverride All							
    ```


## 删除 {#section_lh9_ubw_4fb .section}

 **基本命令** 

-   x：删除光标高亮的那一个字符。
-   nx（n为数字）： 删除光标高亮的字符及其后面的n-1个字符。
-   dd：删除光标所在的那一行。
-   ndd（n为数字）：删除光标所在行及其下面的n-1行。

 **示例** 

本示例中使用的example.conf文件如下所示：

``` {#codeblock_vi3_na4_4m3}
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen 80				
```

例1：在配置文件example.conf中，将`#Listen 12.34.56.78:80`行首的`#`删除。步骤如下：

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  运行`/#Listen 12.34.56.78:80`找到目标，光标此时定位在`#`字符上。
3.  按`x`删除`#`。
4.  按`:wq`保存文件并退出。

    删除完成后，example.conf文件如下所示：

    ``` {#codeblock_mc4_0cw_gk2}
    # Listen: Allows you to bind Apache to specific IP addresses and/or
    # ports, instead of the default. See also the <VirtualHost>
    # directive.
    #
    # Change this to Listen on specific IP addresses as shown below to
    # prevent Apache from glomming onto all bound IP addresses.
    #
    Listen 12.34.56.78:80  
    Listen 80						
    ```


例2：在配置文件example.conf中，将`#Listen 12.34.56.78:80`行和下一行的内容删掉。步骤如下：

1.  运行`vim example.conf`命令打开文件，进入普通模式。
2.  运行`/#Listen 12.34.56.78:80`找到目标。
3.  按`2dd`删除以下内容。

    ``` {#codeblock_jon_hsp_13h}
    #Listen 12.34.56.78:80
    Listen 80
    ```

4.  按`:wq`保存文件并退出。

    删除完成后，example.conf文件如下所示：

    ``` {#codeblock_r91_1ko_l9l}
    # Listen: Allows you to bind Apache to specific IP addresses and/or
    # ports, instead of the default. See also the <VirtualHost>
    # directive.
    #
    # Change this to Listen on specific IP addresses as shown below to
    # prevent Apache from glomming onto all bound IP addresses.
    #						
    ```


