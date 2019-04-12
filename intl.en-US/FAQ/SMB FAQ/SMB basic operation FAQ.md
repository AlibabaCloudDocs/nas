# SMB basic operation FAQ {#concept_ufh_bbz_bhb .concept}

## Why is the disconnected state displayed when I use the net use command to view the status of a mount point? {#section_ltg_dbz_bhb .section}

If no operation is performed on a file system within 15 minutes, the connection is disconnected. The connection is established whenever an operation starts.

## What is the maximum capacity and performance of a CIFS or SMB file system? {#section_is4_wbz_bhb .section}

Currently, when an SMB file system is deployed on a NAS Capacity cluster, the maximum capacity and bandwidth for a single file system are subject to NAS Capacity. Other features, such as supports for a unique namespace, VPCs, and classic networks are the same as those of an NFS file system.

For more information, see [Network Attached Storage](https://www.aliyun.com/price/product#/nas/detail).

## Supported protocols and operating systems for an SMB file system {#section_g5j_bdz_bhb .section}

For more information, see [Restrictions on the SMB protocol](../../../../../reseller.en-US/Limits/SMB file system limits.md#).

For more information about unsupported features for an SMB file system, see [Unsupported features for an SMB file system](../../../../../reseller.en-US/Limits/Features not supported by SMB.md#).

## Restrictions when accessing an SMB file system {#section_ecq_5dz_bhb .section}

Similar to accessing an NFS file system, you cannot access an SMB file system from an ECS instance that is located in another region or from the Internet. You must connect to a VPC by using a dedicated leased line to access the file system.

To access a file system from external networks outside the VPC where the file system is located, see the following sections:

-   [Access NAS from an on-premises IDC using a VPN network](../../../../../reseller.en-US/Best Practices/Access a file system remotely/Access NAS from the local IDC through VPN.md#)
-   [Access NAS from an on-premises IDC using NAT](../../../../../reseller.en-US/Best Practices/Access a file system remotely/Access NAS from the local IDC through NAT Gateway.md#)
-   [Mount NAS file systems on ECS instances that are located in multiple VPCs](../../../../../reseller.en-US/Best Practices/Access a file system remotely/Mount NAS file systems on ECS instances that are located in multiple VPCs.md#)
-   [Mount NAS file systems on ECS instances that are owned by multiple accounts](../../../../../reseller.en-US/Best Practices/Access a file system remotely/Mount NAS file systems on ECS instances that are owned by multiple accounts.md#)

