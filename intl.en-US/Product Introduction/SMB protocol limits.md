# SMB protocol limits {#concept_67161_zh .concept}

NAS supports the SMB protocol. However, you must pay attention to some limits.

## Introduction {#section_kyd_wcb_hfb .section}

Server Message Block \(SMB\), also known as Common Internet File System \(CIFS\), usually refers to SMB protocols earlier than SMB2. SMB is an application-layer communication protocol used to access files, printers, and other shared resources on networks. The SMB mentioned in NAS documentations refers to SMB 2.0 and later versions, which are supported by Alibaba Cloud NAS.

Compared to NFS, the SMB protocol is more suitable for Windows clients. Many versions of Windows provide excellent support for the SMB protocol, and most Windows applications can access Alibaba Cloud NAS through the SMB protocol without modification. We recommend that you use SMB as the file system on your Windows clients.

## Features {#section_ogq_xcb_hfb .section}

SMB provides the following functions:

-   It supports SMB 2.0 and later versions, with corresponding support for Windows Vista, Windows Server 2008, and all later versions of Windows, but does not support Windows XP, Windows Server 2003, and earlier versions. The main reason is that SMB 1.0, in comparison to SMB 2.0 and later versions, has major design differences and serious defects in performance and functions, and Microsoft no longer provides support for earlier versions of Windows and Windows that only supports SMB 1.0.

-   The file system capacity and performance can be linearly scaled in a single namespace. The maximum capacity for a single file system is petabyte-sized data with up to one billion of files.

-   SMB supports secure access control in VPCs and classic networks to protect the privacy of user data. SMB provides mount point permission groups and supports RAM for console access \(RAM APIs\).

-   Access method: Each mount point provides only one share, all named myshare. You can use `\\mount_point\myshare` to access this SMB share. Your multiple virtual hosts in an Alibaba Cloud classic or VPC network can simultaneously access the same SMB file system.

-   The same as the NFS, SMB is based on the same distributed and highly-available underlying file system, so it provides the same SLA. The restrictions on file quantities and lengths are also the same as those in NFS.


## Limits {#section_wfn_1db_hfb .section}

Public cloud environments and traditional enterprise environments are different, especially in diversity and complexity of clients. A few SMB functions are not supported. These unsupported functions have no effect on the operation of most applications. The following functions are unsupported:

-   Access by Linux clients

-   Access to the same file system from both NFS and SMB, or direct access to an SMB file system over a WAN

-   File and directory ACLs \(file system ACLs are supported\)

-   File extended attributes and Oplocks and Lease-based client caching

-   Sparse files, file compression, NIC status queries, reparse points, and other IOCTL/FSCTL operations

-   Alternate data streams

-   SMB Direct, SMB Multichannel, SMB Directory Leasing, Persistent File Handle, and other protocol functions provided by SMB 3.0 and later versions


