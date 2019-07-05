# Known issues on an NFS client {#concept_zzg_t32_jhb .concept}

An NFS client is a part of a kernel. Therefore, errors may occur when you use an NFS client due to several preexisting defects in a kernel. We recommend that you use the following kernel versions to obtain the best user experience for NFS clients.

## Recommended Linux versions {#section_5ti_22q_ew2 .section}

We recommend that you use Alibaba Cloud official images whose kernel versions are strictly tested and verified to ensure system stability. These versions are listed as follows:

-   CentOS 6.9 and later
-   Red Hat Enterprise Linux \(RHEL\) 6.9 and later
-   Ubuntu 14.04, 16.04, and 18.04
-   Debian 8 and later
-   SUSE 11 and later
-   openSUSE 42.3 and later
-   AliOS 17 and later

## \(Priority: High\) Unresponsive file systems caused by the network stack defect of a kernel {#section_i3z_hje_dhq .section}

When the kernel version of a Linux system falls in the range of \[2.6.32-296, 2.6.32-696.10.1\), an unresponsive file system issue may occur. When repeated requests are sent to an NFS server but without any response, the network stack defect may be triggered.

If no response is received from a file system, we recommend that you restart the ECS instance where you perform an operation on the file system. For more information, see [RHEL6.9: NFSv4 TCP transport stuck in FIN\_WAIT\_2 forever](https://access.redhat.com/solutions/3053801).

## \(Priority: High\) Unresponsive file systems caused by a kernel defect {#section_g0k_uvc_9ei .section}

When the kernel version is one of the following versions, an unresponsive file system issue occurs. An NFS server failover may cause a deadlock when you open a connected NFS client or read/write a file system by using the NFS client. This results in the unresponsive file system issue.

-   RHEL 6 and CentOS 6 2.6.32-696.3.1.el6
-   Earlier versions of RHEL 7 and CentOS 7 3.10.0-229.11.1.el7
-   Ubuntu 15.10 Linux 4.2.0-18-generic

When no response is received from a file system, we recommend that you restart the ECS instance where you perform an operation on the file system. For more information, see [RHEL7: NFSv4 client loops with WRITE / NFS4ERR\_STALE\_STATEID - if NFS server restarts multiple times within the grace period](https://access.redhat.com/solutions/1427473).

## \(Priority: Low\) Unsupported chown command and system API calls {#section_78h_hzk_1vs .section}

When the kernel version is 2.6.32, you cannot run the chown command and call system API operations on an NFS client.

## \(Priority: Low\) Unable to stop an ls operation {#section_2iz_ytx_alx .section}

When the kernel version is 2.6.32-696.1.1.el6 and earlier, you cannot stop an ls operation. This occurs when you create or delete files and folder at the same time as the ls operation.

We recommend that you upgrade to the latest kernel version to resolve the issue.

