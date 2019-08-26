# Convert image file format {#concept_obj_qpm_xdb .concept}

Only image files in qcow2, RAW, or VHD format can be imported. If you want to import images in other formats, you need to convert the format before importing the image. This topic describes how to use the qemu-img tool to convert other image file formats to VHD or RAW. Using qemu-img, you can convert RAW, qcow2, VMDK, VDI, VHD \(vpc\), VHDX, qcow1, or QED, to VHD, or implement conversion between RAW and VHD.

## Windows {#windows .section}

To install qemu-img and convert the image file format, follow these steps:

1.  Log on to your server or VM, download [qemu-img](https://qemu.weilnetz.de/w64/) and complete the installation. Installation path: C:\\Program Files\\qemu.
2.  Perform the following actions to create an environment variable for qemu-img:
    1.  Choose **Start** \> **Computer**, then right click **Properties**.
    2.  In the left-side navigation pane, click **Advanced System Settings**.
    3.  In the **System Properties** dialog box, click the **Advanced** tab, and then click **Environment Variables**.
    4.  In the Environment Variables dialog box, find the **Path** variable in the **System Variables** part, and then click **Edit**. If the **Path** variable does not exist, click **New**.
    5.  Add a system variable value:
        -   In the case of **Edit System Variable**: In the **Variable Value** field, add C:\\Program Files\\qemu. Different variable values are separated with semicolon \(;\).
        -   In the case of **New System Variable**: In the **Variable Name** field, enter Path. In the **Variable Value** field, enter C:\\Program Files\\qemu.
3.  Open **Command Prompt** in Windows and run the `qemu-img --help` command. If the result is displayed correctly, the environment variable is configured successfully.
4.  In the **Command prompt**, run the cd \[directory of the source image file\] command to change the directory. For example, `cd D:\ConvertImage`.
5.  Run the `qemu-img convert -f qcow2 -O raw centos.qcow2 centos.raw` command to convert the image file format. Where:
    -   -f is followed by the source image format.
    -   -O \(uppercase is required\) is followed by the converted image format, the source file name, and the target file name.

When the conversion is complete, the target file appears in the directory where the source image file is located.

## Linux {#linux .section}

To install qemu-img and convert the image file format, follow these steps:

1.  Install qemu-img, for example:
    -   For Ubuntu, run the command: `apt install qemu-img`.
    -   For CentOS, run the command: `yum install qemu-img`.
2.  Run the `qemu-img convert -f qcow2 -O raw centos.qcow2 centos.raw` command to convert the image file format. Where:

    -   -f is followed by the source image format.
    -   -O \(uppercase is required\) is followed by the converted image format, the source file name, and the target file name.
    When the conversion is complete, the target file appears in the directory where the source image file is located.


## Troubleshooting {#section_hkw_cgc_p2b .section}

If errors occur during qemu-img installation and there are no clear prompts about the missing dependent libraries, run `pip install -r requirements.txt` to install all the dependent libraries based on the libraries shown in the file requirements.txt of cloud-init.

## Next step {#section_yxz_vdc_p2b .section}

[Import custom images](reseller.en-US/User Guide/Images/Import images/Import custom images.md#)

