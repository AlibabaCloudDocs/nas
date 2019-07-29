# Precautions {#concept_o3z_wfk_bfb .concept}

Before mounting a file system, we recommend that you familiarize yourself with the following precautions.

**Note:** You can only create mount points with the VPC type and mount NFS file systems in NAS Extreme.

-   If the type of a mount point is VPC, you can only mount a linked file system on an ECS instance in the VPC where the mount point is located. The specified authorization address of a rule included in the permission group that is linked to the mount point must match the IP range of the VPC that hosts the ECS instance.
-   If the type of a mount point is classic network, you can only mount a file system on an ECS instance owned by the same account as that of the mount point. The specified authorization address of a rule included in the permission group that is linked to the mount point must match the IP range of the VPC that hosts the ECS instance.
-   You can manually mount a file system or enable an automatic mount at startup.
    -   For more information about how to manually mount a file system on an ECS instance running Linux, see [Mount an NFS file system](intl.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#).
    -   For more information about how to manually mount a file system on an ECS instance running Linux, see [Mount an SMB file system](intl.en-US/Console User Guide/Mount a file system/Mount an SMB file system.md#).
    -   For more information about how to enable an automatic mount on an ECS instance running Linux, see [Enable an automatic mount at startup for an NFS file system](intl.en-US/Console User Guide/Mount a file system/Enable an automatic mount at startup for an NFS file system.md#).
    -   For more information about how to enable an automatic mount on an ECS instance running Windows, see [Enable an automatic mount at startup for an SMB file system](intl.en-US/Console User Guide/Mount a file system/Enable an automatic mount at startup for an SMB file system.md#).
-   For more information about how to use Cloud Enterprise Network \(CEN\) to enable a cross-region mount, see [Enable a cross-VPC mount for a file system](intl.en-US/Console User Guide/Mount a file system/Enable a cross-VPC mount for a file system.md#).
-   For more information about how to use CEN to enable a cross-account mount, see [Enable a cross-account mount for a file system](intl.en-US/Console User Guide/Mount a file system/Enable a cross-account mount for a file system.md#).

