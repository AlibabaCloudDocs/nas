# Known issues on an NFS client {#concept_zzg_t32_jhb .concept}

As an NFS client is a part of a kernel. Therefore, errors may occur when you use an NFS client due to a number of existing defects in a kernel. To improve the user experience of an NFS client, we recommend that you use kernels with latest versions. The following kernels are not recommended.

## No response from an NFS file system due to an abnormal TCP connection {#section_i3z_hje_dhq .section}

If either one of the following conditions is met, an NFS file system may be inaccessible to end-users. This is caused by an abnormal TCP connection in situations, such as unstable network connections and server failovers.

-   The kernel version is earlier than 3.10.0-693.2.2.
-   The kernel version is 3.10.0-693.2.2 or later, but the noresvport option is not enabled for NFS mounting.

**Note:** You can run the `uname -a` command to check the version of a kernel.

If a connection is abnormal, you need to re-mount a file system on an ECS instance. For more information about how to mount a file system, see [Mount an NFS file system in Linux](../../../../reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mount an NFS file system in Linux.md#). You can use the recommended parameters to mount a file system.

After the noresvport option is enabled when you mount a file system, you must run the `ss -ant| grep 2049` command to view the number of the port used for mounting a file system as shown in the following figure. If the port number is greater than 1024, it indicates that the file system is mounted. Otherwise, you must unmount all file systems. You can run the `mount | grep nas` command to ensure no file system is mounted. Then, you can re-mount a file system.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156759/155868802246656_en-US.png)

**Notice:** We recommend that you do not use kernel versions that range from 2.6.32-696 to 2.6.32-696.10.1. The issue of no system response is more prone to occur on one of the kernel versions within this range. For more information, see [RHEL6.9: NFSv4 TCP transport stuck in FIN\_WAIT\_2 forever](https://access.redhat.com/solutions/3053801).

## No response from an NFS file system due to kernel defects {#section_g0k_uvc_9ei .section}

When the kernel version that you are using is one of the early versions, an NFS file system may have no response. When you perform operations, such as open, read, and write files on an NFS client, a deadlock issue occurs due to failover at the NFS backend. This results in no response being returned from an NFS file system.

-   Redhat 6/CentOS 6 2.6.32-696.3.1.el6
-   Redhat 7/CentOS 7 3.10.0-229.11.1.el7 and earlier versions
-   Ubuntu 15.10 Linux 4.2.0-18-generic

When no response is returned from an operation, we recommend that you restart an ECS instance. For more information, see [RHEL7: NFSv4 client loops with WRITE / NFS4ERR\_STALE\_STATEID - if NFS server restarts multiple times within the grace period](https://access.redhat.com/solutions/1427473).

## No support for the chown command and API operations {#section_78h_hzk_1vs .section}

When the kernel version is 2.6.32, the chown command and system APIs are not supported on an NFS client.

## Unresponsive ls operation {#section_2iz_ytx_alx .section}

When the kernel version is 2.6.32-696.1.1.el6 or earlier, you cannot stop an ls operation. This occurs when you perform operations, such as adding and removing files or folders.

We recommend that you can upgrade the kernel version to fix the issue.

