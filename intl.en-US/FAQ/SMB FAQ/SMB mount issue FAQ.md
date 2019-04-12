# SMB mount issue FAQ {#concept_dnz_nsy_bhb .concept}

## You can not mount a NAS file system whose protocol type is SMB on an ECS instance that runs Windows Server Version 1709. {#section_fmv_wsy_bhb .section}

-   Symptoms

    An error occurred while running the following command.

    ```
    C:\Users\Administrator>net use z: \7b33d498e4-nds21.ap-southeast-1.nas.aliyuncs.com\myshare 
    System error 1272 has occurred.
    You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.
    ```

-   Solutions

    The preceding issue occurs when the security policies of Windows Server Version 1709 do not allow access to a remote shared directory by guest users.

    You can use the following steps to resolve the issue:

    -   Locate and modify the following key.

        ```
        [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
        "AllowInsecureGuestAuth"=dword:0
        ```

        Change to:

        ```
        [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
        "AllowInsecureGuestAuth"=dword:1
        ```

    -   Switch to Powershell and enter the following command:

        ```
        New-ItemProperty -Path $registryPath -Name $name -Value $value -PropertyType DWORD -Force
        ```

    For more information, see [Guest access in SMB2 disabled by default in Windows 10, Windows Server 2016 version 1709, and Windows Server 2019](https://support.microsoft.com/en-us/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser).


## How to mount an SMB file system on an ECS instance that runs Linux {#section_idm_frz_bhb .section}

Currently, you cannot mount a NAS file system whose protocol type is SMB on an ECS instance that runs Linux.

To mount a file system, use the following Linux command.

```
mount -t cifs [MOUNT POINT] [LOCAL DIRECTORY] -o username=guest,vers=3.0
```

**Note:** Use version-specific Linux commands to mount an SMB file system.

When using the `-o username=guest` switch for a mount command by using a later version of Linux, you are required to enter a password. We recommend that you use the following command.

```
mount -t cifs [MOUNT POINT] [LOCAL DIRECTORY] -o guest,vers=3.0
```

## An error occurred while connecting to the SMB file system {#section_zs4_mkz_bhb .section}

Symptoms

This issue occurs when both an NFS and SMB file system are used. When you fail to mount an NFS file system by using the net use command, an error occurs when you mount an SMF file system.

Solutions

Ensure that a file system to be mounted is running as expected. You can stop mounting the file system and retry in five minutes. If the issue still persists, open a ticket.

## A mounted SMB directory is only available to the administrator. {#section_xw4_zkz_bhb .section}

This issue occurs when user accounts in Windows are isolated from one another.

You need to create a shared link for multiple users. For example, you can use the following command to create a shared link named myshare in drive C.

```
mklink /D C:\myshare \xxxxxxx-xxxx.cn-beijing.nas.aliyuncs.com\myshare\
```

## An error occurred while loading files that are located in a shared SMB volume by using IIS on an ECS instance that runs Windows Server 2016 {#section_yw4_zkz_bhb .section}

For more information, see [Install and configure Active Directory domains](https://yq.aliyun.com/articles/692463).

## Best practices for deploying IIS in a NAS file system {#section_zw4_zkz_bhb .section}

An HTTP error 500.19 with error code 0x8007003a occurred while mounting an SMB file system on an ECS instance that runs Windows 2016. For more information, see [Best practices for deploying IIS in a NAS file system](https://yq.aliyun.com/articles/692462).

## Can I mount an NFS file system and SMB file system on the same ECS instance? {#section_k2w_b2z_bhb .section}

No.

We recommend that you do not access an SMB file system using a Linux client due to several encoding issues. For example, the supported character sets and the length of a file name for Windows and Linux are different. In Windows, a maximum length of 255 characters encoded with Unicode is supported. However, in Linux, a maximum length of 255 characters encoded with UTF-8 is supported.

If this feature is required for specific uses, you can mount an SMB file system on an ECS instance that runs Linux whose kernel supports SMB2.

Run either one of the following mount commands: `mount -t cifs -o vers=2.0 \\<a mount point>\myshare /mnt` or `mount -t cifs -o vers=2.0 //<a mount point>/myshare /mnt`. If a password is required, press Enter.

Ensure that a CIFS file system is supported by a specific Linux kernel: In the /boot directory, check the value of CONFIG\_CIFS. A value of y or m indicates that a CIFS file system can be mounted.

The details are shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/137459/155503674240796_en-US.png)

**Note:** 

-   You need to install cifs-utils before running the preceding command. Take CentOS as an example. You can run the following command to install cifs-utils.

    ```
    yum install samba-client samba-common cifs-utils
    ```

-   If one or more features of CIFS are not supported on the current version of Linux, we recommend that you upgrade the Linux kernel to version 3.10.0-514 or later.

