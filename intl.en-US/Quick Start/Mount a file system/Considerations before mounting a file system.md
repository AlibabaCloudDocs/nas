# Considerations before mounting a file system {#concept_o3z_wfk_bfb .concept}

After adding a mount point, you can mount a file system to computing resources through the mount point.

## Prerequisites {#section_r35_tyk_bfb .section}

When mounting a file system to an ECS instance through a mount point, you must note the following limits:

-   If the mount point type is VPC, you can mount a file system to an ECS instance only when the instance and the mount point are in the same VPC. In addition, the IP address authorized by a rule of the permission group bound to the mount point must match the VPC IP address of the ECS instance.
-   If the mount point type is Classic network, you can mount a file system to an ECS instance only when the instance and the mount point belong to the same account. In addition, the IP address authorized by a rule of the permission group bound to the mount point must match the intranet IP address of the ECS instance.

**Note:** A NAS file system can be mounted to an ECS instance in another region.Use Cloud Enterprise Network（CEN） to establish a network across regions before you mount the file system.

## Mounting methods {#section_ulh_wyk_bfb .section}

-   NAS supports NFS and SMB file systems. For the mounting methods of the two file systems, see [Mount an NFS file system in Linux](reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mount an NFS file system in Linux.md#) and [Mount an SMB file system](reseller.en-US/Quick Start/Mount a file system/Mount an SMB file system.md#).

