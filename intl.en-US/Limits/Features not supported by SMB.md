# Features not supported by SMB {#concept_hql_pnj_wfb .concept}

This section describes features that are not supported by SMB file systems.

SMB file systems do not support the following features:

-   Access from Linux clients.
-   Access to the same file system using both NFS and SMB protocols or access to the SMB file system using a wide area network.
-   Extended file attributes and client-side caching based on oplocks or leases.
-   IOCTL/FSCTL operations such as sparse files, file compression, NIC status queries, and reparse points.
-   Alternate data streams.

