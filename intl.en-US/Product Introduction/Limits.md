# Limits {#concept_710882 .concept}

This topic describes the limits when you use Alibaba Cloud Network Attached Storage \(NAS\) and its resources. It also includes the limits when you use a client to access NAS resources.

## Limits on resources {#section_h8b_ezf_vtt .section}

The following table lists limits on NAS resources.

|Resource|Description|
|--------|-----------|
|Maximum number of file systems for each account in a region|20|
|Maximum number of mount points in each file system| 2

 |

## Limits on NFS clients {#section_fmv_kcb_lli .section}

Limits on the usage of NFS clients are listed as follows:

-   You can open a maximum of 32,768 files at a time on an NFS client. Files in the list folder and its subfolders are not included in the total number of open files.
-   Each unique mount on an NFS client can acquire a maximum total of 8,192 locks across up to 256 unique file or process pairs. For example, a single process can acquire one or more locks on 256 separate files, or 8 processes can each acquire one or more locks on 32 files.
-   We do not recommend that you use an NFS client in a Windows environment to access an NFS file system.

## Limits on SMB clients {#section_xay_tb2_7n5 .section}

Any one particular file or folder can at any one time be opened a maximum of 8,192 times. This applies across all compute nodes on which file systems are mounted and users that share access to these file systems. This represents a maximum of 8,192 active file handlers for each file or folder. A maximum of 65,536 active file handlers can exist on a file system.

## Limits on file systems {#section_pt0_zzh_bzz .section}

The following lists the limits specific to Alibaba Cloud NAS file systems:

-   Maximum number of files in a single file system: 1 billion.
-   Maximum length of a file system name: 255 bytes.
-   Maximum size of a single file: 32 TB.
-   Maximum directory depth: 1,000 levels.
-   Maximum capacity of a single file system: 10 PB for NAS Capacity and 1 PB for NAS Extreme.
-   Maximum number of mount points for a single file system: 1,000.
-   On Linux systems, mappings between user IDs \(UIDs\) and usernames and mappings between group IDs \(GIDs\) and group names are defined in configurations files. For NFSv3-compliant file systems, if the mapping between an ID and a name is defined in a configuration file, the name is displayed. If no mapping can be found for an ID, the ID is displayed.
-   For NFSv4-compliant file systems, the usernames and group names are displayed as nobody for all files if the version of a Linux kernel is earlier than 3.0. If the kernel version is later than 3.0, the rule used by NFSv3-compliant file systems applies.
-   We recommend that you do not run the chown or chgrp command if the following conditions are met: the file or directory is stored on an NFSv4-compliant file system and the Linux kernel version is earlier than 3.0. If you run either command in this case, the UID and GID of the file or directory are changed to nobody.
-   NAS supports protocols including SMB 2.1 and later and operating systems including Windows 7, and Windows Server 2008 R2 or later. However, NAS does not support Windows Vista, or Windows Server 2008 or earlier. Compared with SMB 2.1 or later, SMB 1.0 has performance and functionality defects due to design issues. Furthermore, the Windows products that support SMB 1.0 or earlier are no longer available.

## Unsupported NFS features {#section_s8b_wum_mfb .section}

Alibaba Cloud NAS does not support the following NFS features.

-   NFSv4.0 does not support the following attributes: FATTR4\_MIMETYPE, FATTR4\_QUOTA\_AVAIL\_HARD, FATTR4\_QUOTA\_AVAIL\_SOFT, FATTR4\_QUOTA\_USED, FATTR4\_TIME\_BACKUP, and FATTR4\_TIME\_CREATE. If one or more of these attributes are specified, an NFS4ERR\_ATTRNOTSUPP error occurs in the /var/log/messages file.
-   NFSv4.1 does not support the following attributes: FATTR4\_DIR\_NOTIF\_DELAY, FATTR4\_DIRENT\_NOTIF\_DELAY, FATTR4\_DACL, FATTR4\_SACL, FATTR4\_CHANGE\_POLICY, FATTR4\_FS\_STATUS, FATTR4\_LAYOUT\_HINT, FATTR4\_LAYOUT\_TYPES, FATTR4\_LAYOUT\_ALIGNMENT, FATTR4\_FS\_LOCATIONS\_INFO, FATTR4\_MDSTHRESHOLD, FATTR4\_RETENTION\_GET, FATTR4\_RETENTION\_SET, FATTR4\_RETENTEVT\_GET, FATTR4\_RETENTEVT\_SET, FATTR4\_RETENTION\_HOLD, FATTR4\_MODE\_SET\_MASKED, and FATTR4\_FS\_CHARSET\_CAP. If one or more of these attributes are specified, an NFS4ERR\_ATTRNOTSUPP error is displayed in the /var/log/messages file.
-   NFSv4 does not support the following operations: OP\_DELEGPURGE, OP\_DELEGRETURN, and NFS4\_OP\_OPENATTR. If one or more of these operations are applied, an NFS4ERR\_ATTRNOTSUPP error is displayed in the /var/log/messages file.
-   NFSv4 does not support delegations.

## Unsupported SMB features {#section_ag9_ikx_0ku .section}

Alibaba Cloud NAS does not support the following SMB features:

-   Extended file attributes and client-side caching based on leases.
-   Input/output control \(IOCTL\) or file system control \(FSCTL\) operations, such as creating sparse files, compressing files, retrieving NIC status, and creating reparse points.
-   Alternate data streams.
-   Identity authentication provided by Active Directory \(AD\) or Lightweight Directory Access Protocol \(LDAP\).
-   Several features provided by SMB 3.0 or later, such as SMB Direct, SMB Multichannel, SMB Directory Leasing, and Persistent File Handle.
-   Access control lists \(ACLs\) on files or directories

