# Troubleshoot issues when you access an SMB file system from an ECS instance running Linux {#concept_1580359 .concept}

This topic describes common issues, causes, and solutions when you access an SMB file system from an ECS instance running Linux.

## Unable to mount an SMB file system {#section_eqa_mer_pey .section}

Cause:

-   You are using an earlier or incompatible version of Linux. Linux distributions that are supported by an SMB file system are listed as follows:
    -   CentOS 7.6 64-bit \(3.10.0-957.5.1.el7.x86\_64\)
    -   Ubuntu 18.04 64-bit \(4.15.0-48-generic\)
    -   Debian 9.9 64-bit \(4.9.0-9-amd64\)
    -   SUSE Enterprise Server 12 SP2 64-bit \(4.4.74-92.35-default\)
    -   OpenSUSE 42.3 64-bit \(4.4.90-28-default\)
    -   Aliyun Linux \(4.19.34-11.al7.x86\_64\)
    -   CoreOS \(4.19.43-coreos VersionID=2079.4.0\)
-   The cifs-utils tool is not installed on a client or the mount.cifs file does not exist in a folder that is specified in the PATH environment variable.
-   No connection is established between a network that hosts the ECS instance running Linux and the other network that hosts the SMB file system.

    -   The ECS instance running Linux and the SMB file system are owned by different Alibaba Cloud accounts.
    -   The ECS instance running Linux and the SMB file system reside in different regions.
    -   The ECS instance running Linux and the SMB file system reside in different networks including VPCs and classic networks that cannot communicate with each other.

        **Note:** The connection between the network of an IDC where a local Linux server resides and the network where an SMB file system resides is not established by using Express Connect.

    -   The IP address of the ECS instance running Linux is not specified in the whitelist of the SMB file system.
    -   The firewall of the ECS instance running Linux denies access to the IP address or port 445 of the SMB file system.
    -   The ECS instance running Linux connects to the SMB file system by using an unsupported TCP port. An SMB file system only supports port 445.
    **Note:** 

    You can use the `ping <VolumeDomainName>` and `telnet <VolumeDomainName> 445` commands to check network connections.

    If port 445 is not enabled on the target ECS instance, we recommend that you add rules for port 445 to the security group of the target ECS instance. For more information, see [Add security group rules](../../../../reseller.en-US/Security/Security groups/Add security group rules.md#).

-   The administrator of the ECS instance running Linux does not have the root permissions or is not authorized to use the mount command. You can use the sudo command to authorize the administrator to use the mount command.
-   The type of file system is not set to Common Internet File System \(CIFS\) when you mount the file system.
-   The vers of a file system is not set to 2.1 or 3.0 when you mount the file system.
-   You do not grant permissions to members of the Guest user group to mount a file system.
-   You specify an invalid value for uid, gid, dir\_mode, or file\_mode when mounting a file system.
-   The SELinux settings for the directory of the target mount point are invalid.
-   The maximum number of mounted file systems for a single file system on an ECS instance running Linux is exceeded \(1,000\). This type of issues is prone to occur when you mount a file system on a node of Container Service for Kubernetes.

Solution:

1.  Troubleshoot the issue by referring to [Access an SMB file system from an ECS instance running Linux](../../../../reseller.en-US/Best Practices/Access an SMB file system from an ECS instance running Linux.md#) and checking the preceding causes.
2.  Check the /var/log/messages file and the output of the dmesg command.
3.  Contact Alibaba Cloud Technical Support.

    You need to provide the version of Linux, ouput of the mount commands, files stored in /var/log/messages, and output of the dmesg command.


## Poor performance of a file system {#section_hrg_428_p2v .section}

If the performance of an SMB file system is poor, the possible causes of the issue are listed as follows:

-   Cause 1: The throughput of a single SMB file system is related to the available storage space. The maximum throughput \(read and write\) of a single file system is limited by the current storage capacity.

    Solution: You can use the fio tool to test the performance of an SMB file system. For more information, see [Performance testing for NAS](../../../../reseller.en-US/Performance/Performance testing for NAS.md#).

-   Cause 2: The bandwidth for a single ECS instance running Linux is low.

    Solution: You can use multiple ECS instances to achieve the expected performance.

-   Cause 3: The cache for an SMB file system on a client is disabled.

    Solution: You can enable the cache by setting the cache parameter to strict when you mount an SMB file system. The default value of this parameter is strict. If you set this parameter to none, cache is disabled. You can use the `sudo mount | grep cifs` command to check the value of the cache parameter.

-   Cause 4: The size of the I/O throughput for an SMB client is set to an invalid value.

    Solution: You can change the value of rsize or wsize based on your business requirements. The default value is 1048576.

-   Cause 5: The CPU or memory specification of the ECS instance running Linux is low, or most CPU or memory usage is occupied by other processes.

    Solution: You can select appropriate specifications of components for the ECS instance. You must balance the usage of CPU and memory resources for each process to ensure that the file system is running as expected. You can use the `top` command to check the usage of CPU and memory.

-   Cause 6: The atime option is specified when you mount a file system.

    Solution: If your business is not sensitive to the access time, we do not recommend that you specify the atime option.

-   Cause 7: You can encounter scenarios such as using a file system client as a Web server on which a large number of read operations and a few write operations with alerts occur.

    Solution: You can enable a cache specific to a Web server such as Apache on the file system client or contact Alibaba Cloud Technical Support to enable the acceleration feature for Web server scenarios.


## Slow to migrate or replicate files from a file system {#section_e7b_fhw_xgb .section}

If you have excluded the preceding performance issues of a file system, this issue may occur because you do not migrate or replicate files in parallel. You can use the following open-source tools to migrate or replicate files.

-   [GNU parallel](https://github.com/martymac/fpart) 

    **Note:** 

    -   Specify an appropriate number of threads based on system resources.
    -   Example: find \* -type | parallel --will-cite -j 10 cp \{\} /mnt/smb/ &
-   [Fpart](https://github.com/martymac/fpart)
-   [Fpsync](https://github.com/martymac/fpart/blob/master/tools/fpsync)
-   [multi](https://github.com/pkolano/mutil)

## An error message "Permission denied" occurred while accessing a file system {#section_8i1_xfh_84q .section}

Cause: You specify an invalid value for the uid, gid, file\_mode, or dir\_mode parameter when you mount a file system.

Solution: You need to check whether you specify a valid value for each of the mount parameters, such as uid, gid, file\_mode, and dir\_mode. For more information, see [Access an SMB file system from an ECS instance running Linux](../../../../reseller.en-US/Best Practices/Access an SMB file system from an ECS instance running Linux.md#).

## Unable to change uppercase letters to lowercase letters or lowercase letters to uppercase letters for a filename {#section_8q1_l27_fm1 .section}

The filename of an SMB file system is not case sensitive. This rule also applies to Windows. However, you cannot change uppercase letters to lowercase letters or lowercase letters to uppercase letters for a filename.

You can work around this issue by changing a filename with uppercase letters or lowercase letters to a different filename. Then, you can change the new filename to a filename with lowercase letters or uppercase letters.

## Unable to change the owner of a file and mode of a file or directory {#section_hb7_l5k_cab .section}

You can only specify the owner of a file and mode of a file or directory in a file system when you mount the file system. For more information, see [Access an SMB file system from an ECS instance running Linux](../../../../reseller.en-US/Best Practices/Access an SMB file system from an ECS instance running Linux.md#).

## Unable to use access control lists \(ACLs\) {#section_z5v_3ve_8tn .section}

You cannot use ACLs in NAS. If you need to use ACLs, we recommend that you contact Alibaba Cloud Technical Support.

## Unable to create symbolic links {#section_bcg_1m4_4aa .section}

Cause: The mfsymlinks option is not specified or SMB 2.0 is used when you mount a file system.

Solution: When you mount a file system, we recommend that you use SMB 2.1 or 3.0 and specify the mfsymlinks option.

## No response received from an SMB mount point {#section_xdu_zdp_v6k .section}

Cause: On a Linux distribution with a kernel of 3.10.0-514 or earlier, you may fail to access a mount point because the SMB driver crashes. When multiple clients access a file system mounted on a Linux distribution in parallel, a crash may occur. The following snippet shows an example stack. Example log entries in the kernel log file are shown as follows.

``` {#codeblock_5q0_ern_1vq}
...
[<ffffffffc03c9bc1>] cifs_oplock_break+0x1f1/0x270 [cifs]
[<ffffffff810a881a>] process_one_work+0x17a/0x440
[<ffffffff810a8d74>] rescuer_thread+0x294/0x3c0
...
```

Solution:

-   Re-mount the file system by setting the cache parameter to none. However, this may affect the performance of the file system.
-   Upgrade the operating system of the ECS instance running Linux.

