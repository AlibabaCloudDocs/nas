# Introduction {#concept_qpg_wrt_1fb .concept}

Alibaba Cloud Network Attached Storage \(NAS\) provides file storage services for compute nodes, such as ECS instances, Elastic High Performance Computing \(E-HPC\) clusters, and Container Service clusters.

## Overview {#section_alc_yth_1hb .section}

NAS is a distributed file system that provides shared access, scalability, high availability, and high performance. Dependent on POSIX-based file APIs, NAS provides several benefits, such as compatibility with operating systems, shared access, data consistency, and exclusive locks.

NAS provides easy-to-use and scalable file storage that can work with ECS. A NAS file system can provide simultaneous access to multiple ECS instances. The storage capacity of a file system scales up or down with the number of files. NAS provides a common data source for multiple instances or running applications.

NAS provides multiple storage types, such as NAS Capacity, NAS Performance, and NAS Extreme. For more information, see [Storage types](reseller.en-US/Product Introduction/Storage types.md#).

NAS provides a wide variety of scenarios. For more information, see [Scenarios](reseller.en-US/Product Introduction/Scenarios.md#).

## Benefits {#section_zkc_4f5_2fb .section}

NAS provides a number of benefits, such as being high-performance, cost-effective, secure, reliable, and easy-to-use.

-   Costs
    -   A NAS file system can be mounted on multiple compute nodes at the same time while still allowing access to these nodes. This reduces a large number of data copies and synchronization costs.
    -   The performance of a NAS file system increases with expanding storage capacity. Without the need for further investment in high-end file storage devices, you can reduce a large number of hardware costs.
    -   With NAS, you only pay for the size of storage space that you use. In addition, no minimum consumption or extra configuration costs exist. For more information, see [Pricing](../../../../reseller.en-US/Pricing/Pricing.md#).
    -   With high reliability, NAS reduces data security risks and maintenance costs.
-   Easy-to-use

    You can easily create file systems without the extra need to deploy and maintain these file systems.

-   Security

    RAM-based access control VPC networks are used to isolate user access, and encrypt data both in transit and at rest to prevent the interception and tampering of critical data.

-   High reliability

    With data reliability of 99.999999999%, NAS reduces a large number of data security risks.

-   High performance

    NAS is a distributed file system that provides linear performance with increasing capacity and ultra-high performance over traditional data stores.

-   Compatibility
    -   NAS is compatible with multiple standard protocols, such as NFS and SMB. Compatible with POSIX-based file APIs, NAS provides data consistency and exclusive locks.
    -   You can view the result in real time after the content of a file stored in a NAS file system is changed.

## Features {#section_rvx_5g5_2fb .section}

NAS provides the following features:

|Scenarios|Features|Reference|
|---------|--------|---------|
|Create file systems|Before using NAS, you must create a file system.|[Create file systems](../../../../reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5)|
|Manage file systems|You can view the details of a file system or delete a file system.|[Manage file systems](../../../../reseller.en-US/Console User Guide/Manage file systems.md#)|
|Add mount points|You must add a mount point to a file system before mounting the file system.|[Create a mount point](../../../../reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq)|
|Manage mount points|You can disable, enable, or delete a mount point, or modify the permission group of a mount point.|[Manage mount points](../../../../reseller.en-US/Console User Guide/Manage mount points.md#)|
|Mount file systems|You must mount a file system on a computational node before using the file system.|[Mount a file system](../../../../reseller.en-US/Console User Guide/Mount a file system/Precautions.md#)|
|Manage user access|You can authorize a RAM user to operate NAS or control user access by using permission groups.| -   [Access control for RAM users](../../../../reseller.en-US/Console User Guide/Manage permissions/Access control for RAM users.md#)
-   [Create a custom policy](../../../../reseller.en-US/Console User Guide/Manage permissions/Create a custom policy.md#)
-   [Manage permission groups](../../../../reseller.en-US/Console User Guide/Manage permissions/Manage permission groups.md#)

 |
|Use NAS APIs|NAS provides various API interfaces that allow you to perform various operations on a file system.|[API overview](../../../../reseller.en-US/API reference/API overview.md#)|

## Billing methods {#section_x23_1gg_1hb .section}

For more information about NAS billing methods, see NAS pricing.

