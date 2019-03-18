# SMB file system limits {#concept_h2x_4t3_wfb .concept}

This section describes SMB file system limits.

SMB file systems have the following limits:

-   SMB file systems support SMB protocol version 2.1 and later, and Windows 7, Windows Server 2008 and later versions, but do not support Windows Vista, Windows Server 2003 and earlier versions. Compared with SMB 2.0 and later versions, SMB 1.0 has performance and function vulnerabilities, for example, Windows support for SMB 1.0 and earlier versions are no longer maintained by Microsoft.
-   Access method: Each mount point only provides one SMB share named myshare. You can use \\\\mount\_point\\myshare to access SMB shares. Multiple virtual hosts in an Alibaba Cloud Classic or VPC network can simultaneously access the same SMB file system.
-   Access control lists are available at file system level, but not at file or directory level.

