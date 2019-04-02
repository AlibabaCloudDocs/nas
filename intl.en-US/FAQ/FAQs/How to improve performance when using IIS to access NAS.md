# How to improve performance when using IIS to access NAS {#concept_65228_zh .concept}

## Problem description {#section_mjy_qfh_hfb .section}

When IIS accesses a file by using a NAS share, the backend of IIS will frequently access NAS. Unlike accessing a local file system, you must interact with networks when accessing NAS. Even if it takes a short time for each interaction, the total amount of time increases with an increasing number of clients.

## Solutions { .section}

For more information, see [SMB2 Client Redirector Caches Explained](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200(v=ws.10)).

You can increase the values of the following registry keys. For example, you can change the values to 600 or above.

The path of the registry key is HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\LanmanWorkstation\\Parameters.

The registry keys are listed as follows:

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

**Note:** 

-   When none of the preceding keys exists, troubleshoot the issue as follows:
    1.  Ensure that SMB is used rather than NFS.
    2.  Ensure that the current version of Windows supports these registry keys. When the current version of Windows supports these registry keys but they do not exist, you can manually create these registry keys. For more information, see [Performance tuning for file servers](https://docs.microsoft.com/en-us/windows-server/administration/performance-tuning/role/file-server/).
-   For web files that are frequently accessed by IIS, such as js and css scripts, we recommend that you move these files to a local PC.

