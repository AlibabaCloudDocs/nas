# Features not supported by NFS {#concept_rnt_v53_wfb .concept}

This section describes the features that are not supported by NFS.

NFS file systems do not support the following features:

-   NFSv4.0 does not support the following attributes: FATTR4\_MIMETYPE, FATTR4\_QUOTA\_AVAIL\_HARD, FATTR4\_QUOTA\_AVAIL\_SOFT, FATTR4\_QUOTA\_USED, FATTR4\_TIME\_BACKUP, and FATTR4\_TIME\_CREATE. An attempt to set these attributes results in an NFS4ERR\_ATTRNOTSUPP error that is sent back to the client.
-   NFSv4.1 does not support the following attributes: FATTR4\_DIR\_NOTIF\_DELAY, FATTR4\_DIR\_NOTIF\_DELAY, FATTR4\_DACL, FATTR4\_CHANGE\_POLICY, FATTR4\_FS\_STATUS, FATTR4\_LAYOUT\_HINT, FATTR4\_LAYOUT\_TYPES, FATTR4\_LAYOUT\_ALIGNMENT, FATTR4\_FS\_LOCATIONS\_INFO, FATTR4\_MDSTHRESHOLD, FATTR4\_RETENTION\_GET, FATTR4\_RETENTION\_SET, FATTR4\_RETENTEVT\_GET, FATTR4\_RETENTEVT\_SET, FATTR4\_RETENTION\_HOLD, FATTR4\_MODE\_SET\_MASKED, FATTR4\_FS\_CHARSET\_CAP. An attempt to set these attributes results in an NFS4ERR\_ATTRNOTSUPP error that is sent back to the client.
-   NFSv4 does not support the following operations: OP\_DELEGPURGE, OP\_DELEGRETURN, and NFS4\_OP\_OPENATTR. An attempt to perform these operations results in an NFS4ERR\_NOTSUPP error that is sent back to the client.
-   Currently, NFSv4 does not support delegation.

