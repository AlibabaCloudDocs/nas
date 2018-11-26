# Pre-mount considerations {#concept_o3z_wfk_bfb .concept}

After adding a mount point, you can compute the resource to the file system by the mount point.

## Prerequisites {#section_r35_tyk_bfb .section}

ECS has the following restrictions when mounting a file system:

-   - If the mount point is for a VPC, only the ECS instances within the same VPC can be mounted, and the authorized address in a rule for the permission group bound to the mount point matches the VPC IP address of the ECS instance.
-   - If the mount point is for a classic network, only the ECS instances under the same account can be mounted, and the authorized address in a rule for the permission group bound to the mount point matches the intranet IP address of the ECS instance.

## Mount Mode {#section_ulh_wyk_bfb .section}

NAS is currently available in both generic and NAS Plus smart cache types. The two storage types are mounted differently.

-   NAS generic: NAS generic storage supports NFS and SMB file systems, for how these two file systems are mounted, see[Mounting NFS file systems on Windows systems](reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mounting NFS file systems on Windows systems.md#), [Mounting NFS file systems on Windows systems](reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mounting NFS file systems on Windows systems.md#)and [Mounting SMB File Systems](reseller.en-US/Quick Start/Mount a file system/Mounting SMB File Systems.md#).
-   NAS Plus smart cache type: About how NAs Plus smart cache-based storage is mounted, see intelligent cached client usage documentation.

    **Note:** The NAS Plus smart cache file system must use a dedicated client. At the same time, private clients can only be used on NAS Plus smart cache file systems, cannot be used on NAS generic \(performance/capacity.


