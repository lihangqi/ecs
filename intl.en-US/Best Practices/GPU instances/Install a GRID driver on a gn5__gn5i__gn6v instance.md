# Install a GRID driver on a gn5/gn5i/gn6v instance {#concept_66441_zh .concept}

If your GPU instance \(available in the gn5, gn5i and gn6v families\) requires OpenGL, you must install the GRID driver on the instance. The NVIDIA GRID license granted to the NVIDIA GPU \(such as P100, P4 and V100\) of gn5, gn5i and gn6v instances cannot meet the graphics requirements of OpenGL. However, you can use the trial version of the GRID driver to meet the requirements.

This article explains how to install the GRID driver and deploy a desktop environment on a Linux GPU instance running Ubuntu 16.04 or CentOS 7.3.

## Ubuntu 16.04 {#part1 .section}

This section describes how to install the GRID driver on a GPU instance running Ubuntu 16.04 64-bit.

## Prerequisites { .section}

-   You have created a gn5, gn5i or gn6v instance. For more information, see [create a compute optimized instance with GPUs](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create a compute optimized instance with GPUs.md#). Make sure that the instance can access the Internet.

    **Note:** We recommend that you use a **public image** rather than an image from the **marketplace** that is pre-installed with a NVIDIA driver. Otherwise, you have to disable the Nouveau driver after the instance is created. To disable the Nouveau driver, create a file named nouveau.conf in the directory of /etc/modprobe.d and add `blacklist nouveau` into the file.

-   You have installed a VNC application on your local machine. In this example, VNC Viewer is used.

## Install a GRID driver { .section}

To install the GRID driver, follow these steps:

1.  [Connect to the Linux instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the following commands in sequence to upgrade the system and install the KDE.

    ```language-shell
    apt-get update
    apt-get upgrade
    apt-get install kubuntu-desktop
    
    ```

3.  Run `reboot` to restart the system.
4.  [Connect to the Linux instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#) again, and then run the following commands to download and decompress the NVIDIA GRID driver package.

    The NVIDIA GRID driver package contains the drivers for various operating systems. For Linux OS, select **NVIDIA-Linux-x86\_64-390.57-grid.run**.

    ```language-shell
    wget https://nvidia-driver.oss-cn-huhehaote.aliyuncs.com/NVIDIA-Linux-x86_64-390.57-grid.run
    
    ```

5.  Run the following commands in sequence, then follow the prompts to install the NVIDIA GRID driver.

    ```language-shell
    chmod 777 NVIDIA-Linux-x86_64-390.57-grid.run
    . /NVIDIA-Linux-x86_64-390.57-grid.run
    
    ```

6.  Run `nvidia-smi` to verify the installation.

    If the following message appears, the driver is installed successfully.

    ![Test if the driver is installed successfully.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611965_en-US.png)

7.  Add License Server to activate the License:
    1.  Switch to the /etc/nvidia directory: `cd /etc/nvidia`.
    2.  Create a file named gridd.conf: `cp gridd.conf.template gridd.conf`.
    3.  Add the following lines about License Server to the gridd.conf file.

        ```language-shell
        ServerAddress=116.62.19.179
        ServerPort=7070 
        FeatureType=2
        EnableUI=TRUE
        
        ```

8.  Run the command to install x11vnc.

    ```language-shell
    apt-get install x11vnc
    
    ```

9.  Run `lspci | grep NVIDIA` to check GPU BusID.

    In this example, the GPU BusID is `00:07.0`.

10. Configure the X Server environment and restart the system:
    1.  Run `nvidia-xconfig --enable-all-gpus --separate-x-screens`.
    2.  Edit /etc/X11/xorg.conf: Add your GPU BusID to the `Section "Device"`. In this example, `BusID "PCI:0:7:0" is added`.

        ![Add GPU BusID.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611966_en-US.png)

    3.  Run `reboot` to restart the system.

## Verify installation { .section}

To verify the installation of the GRID driver, follow these steps:

1.  Run the following command to install the GLX application.

    ```language-shell
    apt-get install mesa-utils
    
    ```

2.  Run `startx` to start X Server.

    **Note:** 

    -   If the `startx` command cannot be found, run `apt-get install xinit` to install it.
    -   Running `startx` may result in the `hostname: Name or service not known` error. This error has no effect on starting X Server. Run `hostname` to obtain the host name of the instance, and then modify the /etc/hosts file by replacing the `hostname`, which is preceded by `127.0.0.1`, with the actual host name of your instance.

        ![An error occurs when running startx.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611967_en-US.png)

3.  Start a new terminal session of the SSH client and run the following command to start x11vnc.

    ```language-shell
    x11vnc -display :1
    
    ```

    If the following message appears, x11vnc has been restarted successfully. Now you can connect to the instance by using a VNC application. In this example, VNC Viewer is used.

    ![Run x11vnc.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611968_en-US.png)

4.  Log on to the ECS console, and [add security group rules](../../../../reseller.en-US/User Guide/Security groups/Add security group rules.md#) in the security group to allow inbound traffic from the Internet on the TCP 5900 port.
5.  On the local machine, start VNC Viewer and type in `Public IP address of the instance:5900` to connect to the instance and enter the KDE desktop.
6.  Run `glxinfo` to view the configurations supported by the current GRID driver:
    1.  Start a new terminal session of the SSH client.
    2.  Run `export DISPLAY=:1`.
    3.  Run `glxinfo –t` to list the configurations supported by the current GRID driver.
7.  Run `glxgears` to test the GRID driver:
    1.  On the KDE desktop, right-click the desktop and select **Run Command**.
    2.  Run `glxgears` to start the testing application. If the following figure appears, the GRID driver works normally.

        ![glxgears](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611970_en-US.png)


## CentOS 7 {#part2 .section}

This section describes how to install the GRID driver on a GPU instance running CentOS 7.3 64-bit.

## Prerequisites { .section}

-   You have created a gn5, gn5i or gn6v instance. For more information, see [Create a compute optimized instance with GPUs](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create a compute optimized instance with GPUs.md#). Make sure that the instance can access the Internet.
-   You have installed a VNC application on your local machine. In this example, VNC Viewer is used.

## Install a GRID driver { .section}

To install the GRID driver, follow these steps:

1.  [Connect to the Linux instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the following commands in sequence to upgrade the system and install the KDE.

    ```language-shell
    yum update
    yum install kernel-devel
    yum groupinstall "KDE Plasma Workspaces"
    
    ```

3.  Run `reboot` to restart the system.
4.  [Connect to the Linux instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#) again, and then run the following commands to download and decompress the NVIDIA GRID driver package.

    The NVIDIA GRID driver package contains the drivers for various operating systems. For Linux OS, select **NVIDIA-Linux-x86\_64-390.57-grid.run**.

    ```language-shell
    wget https://nvidia-driver.oss-cn-huhehaote.aliyuncs.com/NVIDIA-Linux-x86_64-390.57-grid.run
    
    ```

5.  Disable the nouveau driver:
    1.  Run `vim /etc/modprobe.d/blacklist.conf`, and add `blacklist nouveau` to the file.
    2.  Run `vim /lib/modprobe.d/dist-blacklist.conf` and add the following lines.

        ```language-shell
        blacklist nouveau
        options nouveau modeset=0
        
        ```

    3.  Run `mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img`.
    4.  Run `dracut /boot/initramfs-$(uname -r).img $(uname -r)`.
6.  Run `reboot` to restart the system.
7.  Run the following commands in sequence, then follow the prompts to install the NVIDIA GRID driver.

    ```language-shell
    chmod 777 NVIDIA-Linux-x86_64-390.57-grid.run
    . /NVIDIA-Linux-x86_64-390.57-grid.run
    
    ```

8.  Run `nvidia-smi` to verify the installation.

    If the following message appears, the driver is installed successfully.

    ![CentOS_Test if the driver is installed successfully.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611971_en-US.png)

9.  Add License Server to activate the License:
    1.  Run `cd /etc/nvidia` to switch to the /etc/nvidia directory.
    2.  Run `cp gridd.conf.template gridd.conf` to create a file named gridd.conf.
    3.  Add the following lines about License Server to the gridd.conf file.

        ```language-shell
        ServerAddress=116.62.19.179
        ServerPort=7070
        FeatureType=2
        EnableUI=TRUE
        
        ```

10. Run the following command to install x11vnc.

    ```language-shell
    yum install x11vnc
    
    ```

11. Run `lspci | grep NVIDIA` to check GPU BusID.

    In this example, the GPU BusID is `00:07.0`.

12. Configure the X Server environment:
    1.  Run `nvidia-xconfig --enable-all-gpus --separate-x-screens`.
    2.  Edit /etc/X11/xorg.conf: Add your GPU BusID to the `Section "Device"`. In this example, `BusID "PCI:0:7:0"` is added

        ![Add GPU BusId.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611966_en-US.png)

13. Run `reboot` to restart the system.

## Verify installation { .section}

To verify the installation of the GRID driver, follow these steps:

1.  Run `startx` to start X Server.
2.  Start a new terminal session of the SSH client and run the command to start x11vnc.

    ```language-shell
    x11vnc -display :0
    
    ```

    If the following message appears, x11vnc has been restarted successfully. Now you can connect to the instance by using a VNC application. In this example, VNC Viewer is used.

    ![Run x11vnc.](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611968_en-US.png)

3.  Log on to the ECS console, and [add security group rules](../../../../reseller.en-US/User Guide/Security groups/Add security group rules.md#) in the security group to allow inbound traffic from the Internet on TCP 5900 port.
4.  On the local machine, start VNC Viewer and type in `Public IP address of the instance:5900` to connect to the instance and enter the KDE desktop.
5.  Run `glxinfo` to view the configurations supported by the current GRID driver:
    1.  Start a new terminal session of the SSH client.
    2.  Run `export DISPLAY=:0`.
    3.  Run `glxinfo –t` to list the configurations supported by the current GRID driver.
6.  Run `glxgears` to test the GRID driver:
    1.  On the VNC Viewer, right-click the desktop and select **Run Command**.
    2.  Run `glxgears` to start the testing application. If the following image appears, the GRID driver works normally.

        ![glxgears](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9838/153950904611970_en-US.png)


