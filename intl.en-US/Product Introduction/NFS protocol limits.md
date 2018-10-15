# NFS protocol limits {#concept_27535_zh .concept}

Network Attached Storage \(NAS\) supports the NFSv3 and NFSv4 protocols. However, you must pay attention to the following limits:

-   Attributes not supported by NFSv4.0 include: FATTR4\_MIMETYPE, FATTR4\_QUOTA\_AVAIL\_HARD, FATTR4\_QUOTA\_AVAIL\_SOFT, FATTR4\_QUOTA\_USED, FATTR4\_TIME\_BACKUP, and FATTR4\_TIME\_CREATE. If these attributes are attempted, an NFS4ERR\_ATTRNOTSUPP error is returned to the client.

-   Attributes not supported by NFSv4.1 include: FATTR4\_DIR\_NOTIF\_DELAY, FATTR4\_DIRENT\_NOTIF\_DELAY, FATTR4\_DACL, FATTR4\_SACL, FATTR4\_CHANGE\_POLICY, FATTR4\_FS\_STATUS, FATTR4\_LAYOUT\_HINT, FATTR4\_LAYOUT\_TYPES, FATTR4\_LAYOUT\_ALIGNMENT, FATTR4\_FS\_LOCATIONS\_INFO, FATTR4\_MDSTHRESHOLD, FATTR4\_RETENTION\_GET, FATTR4\_RETENTION\_SET, FATTR4\_RETENTEVT\_GET, FATTR4\_RETENTEVT\_SET, FATTR4\_RETENTION\_HOLD, FATTR4\_MODE\_SET\_MASKED, and FATTR4\_FS\_CHARSET\_CAP. If these attributes are attempted, an NFS4ERR\_ATTRNOTSUPP error is returned to the client.

-   OPs not supported by NFSv4.1 include: OP\_DELEGPURGE, OP\_DELEGRETURN, and NFS4\_OP\_OPENATTR. If these OPs are attempted, an NFS4ERR\_NOTSUPP error is returned to the client.

-   NFSv4 currently does not support Delegation.

-   Issues concerning UID and GID

    -   For the NFSv3 protocol, if the file’s UID or GID exists in a Linux local account, then the corresponding user name or group name is displayed based on the mapping relations of the local UID and GID; if the file’s UID or GID does not exist in the local account, then the UID or GID is displayed directly.

    -   For the NFSv4 protocol, if the version of the local Linux kernel is earlier than 3.0, the UID and GID of all files is displayed as nobody; if the version is later than 3.0, then the display rule is the same as that of NFSv3 protocol.

        **Note:** If you use NFSv4 protocol to mount a file system, and the version of your Linux kernel is earlier than 3.0, we recommend that you do not change owner or group of the file or directory. Otherwise, the UID and GID of the file or directory is changed to nobody.

-   A single file system can be simultaneously mounted and accessed by up to 10,000 computing nodes.

