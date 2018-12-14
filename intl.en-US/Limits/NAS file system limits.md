# NAS file system limits {#concept_fwy_lbk_5fb .concept}

NAS file systems have the following limits:

-   The maximum length of the name of a file system is 255 bytes.
-   The maximum length of a symbolic link is 4080 bytes.
-   The maximum size of a single file is 32 TB.
-   NAS does not support mounting file systems across regions.
-   The storage capacity of a file system is 1 PB \(performance type\) and 10 PB \(capacity type\).
-   Each account can create up to 10 file systems.
-   Each file system can create up to 2 mount points.
-   Currently, mount points in Classic networks only allow access from ECS instances that are in the same account with them. These mount points do not support default permission groups. You can only add single IP addresses instead of CIDR blocks when creating security group rules for these mount points.
-   A file system can be simultaneously mounted on and accessed by up to 10,000 computing nodes.
-   For the NFSv3 protocol, if the file UID or GID exists in a Linux local account, then the corresponding username or group name is displayed based on the mapping relation of the local UID and GID. If the file UID or GID does not exist in the local account, then the UID or GID is displayed.
-   For the NFSv4 protocol, if the version of the local Linux kernel is earlier than 3.0, the UID and GID of all files are displayed as nobody. If the version is later than 3.0, then the display rule is the same as that of the NFSv3 protocol.
-   If you use the NFSv4 protocol to mount a file system, and the version of your Linux kernel is earlier than 3.0, we recommend that you do not run the chown or chgrp command on a file or directory. Otherwise, the UID and GID of the file or directory are changed to nobody.

