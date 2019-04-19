# What is NAS {#concept_qpg_wrt_1fb .concept}

Alibaba Cloud Network Attached Storage \(NAS\) is a highly reliable and available file storage service. You can mount the file system to computing nodes \(such as Alibaba Cloud ECS, E-HPC, or Container Service\)

## Features {#section_lwx_nd5_2fb .section}

NAS has the following features:

-   Seamless integration

    Alibaba Cloud NAS supports the NFSv3, NFSv4, and SMB protocols, and provides standard file system access semantics. Your applications and workloads can work seamlessly with NAS.

-   Shared access

    Multiple computing nodes can access a NAS file system simultaneously, allowing applications relying on the same data source to be deployed across numerous Alibaba Cloud ECS, E-HPC, or Container Service instances.

-   Elastic scalability

    NAS is billed based on the actual usage, which can meet the requirement for elastic scalability. The capacity of each NAS storage type is as follows:

    -   NAS capacity type and NAS Plus: The maximum capacity of a file system instance is 10 PB.
    -   NAS performance type: The maximum capacity of a file system instance is 1 PB.
-   Security control

    Multiple security strategies are implemented to guarantee complete data security in NAS file system, including:

    -   Network isolation \(VPC\) and User isolation \(classic network\)
    -   Standard file system access control
    -   Permission group access control, see [Use permission groups](../../../../reseller.en-US/User Guide/Use permission groups.md#) for details.
    -   primary account/RAM account authorization, see [Use RAM to grant RAM users the NAS permission](../../../../reseller.en-US/User Guide/Use RAM to grant RAM users the NAS permission.md#) for details.
-   Performance scaling

    Alibaba Cloud NAS provides high-throughput, high-IOPS, and low-latency storage for application workloads. Performance and capacity requirements can be scaled based on business needs.

-   Strong consistency

    NAS provides a strong consistency data model. When a write, update, or delete action to cloud storage data is successful, all further accesses to that data in the cloud read the latest update.


## Advantages {#section_zkc_4f5_2fb .section}

NAS has its own advantages in cost, reliability, and ease of use.

-   Cost
    -   A NAS file system can be mounted on and accessed by multiple compute nodes, saving a large amount of copy and synchronization costs.
    -   The performance of an individual file system scales linearly with the storage capacity, substantially reducing costs compared to purchasing a high-end file storage device.
    -   NAS is billed based on the actual usage. Therefore, you can adjust system capacity as needed to save costs.
    -   With the high availability, NAS reduces data security risk and substantially saves maintenance cost.
-   Reliability

    With 99.999999999% data reliability, Alibaba Cloud NAS reduces data security risk in comparison to self-built file storage.

    The storage must be highly durable by default. All data within the file storage service must be synchronously replicated, so that a minimum of two copies of each file are stored within a logical data center. The two copies must be stored on different devices.

-   Ease of use
    -   Alibaba Cloud NAS supports the NFSv3, NFSv4, and SMB protocols. You can directly use apps with NAS without modification.
    -   Once you write, update, or delete any file stored in NAS, all further access to the file in the cloud can read the latest update.

## Functions {#section_rvx_5g5_2fb .section}

NAS provides the following functions:

|Scenarios|Function|Reference|
|---------|--------|---------|
|Create a file system|You must create a file system to use NAS.|[Create a file system](../../../../reseller.en-US/Quick Start/Create a file system.md#)|
|Manage a file system|You can check the detailed information about a file system or delete a file system.|[File system](../../../../reseller.en-US/User Guide/File system.md#)|
|Add a mount point|To mount a file system, you must add a mount point to the file system.|[Add a mount point](../../../../reseller.en-US/Quick Start/Add a mount point.md#)|
|Manage a mount point|You can disable, enable, or delete a mount point, or modify the permission group of a mount point.|[Mount point](../../../../reseller.en-US/User Guide/Mount point.md#)|
|Mount a file system|You must mount a file system to the compute node before use.| [Mount an NFS file system in Linux](../../../../reseller.en-US/Quick Start/Mount a file system/Mount a NFS file system/Mount an NFS file system in Linux.md#)

 [Mount an SMB file system](../../../../reseller.en-US/Quick Start/Mount a file system/Mount an SMB file system.md#)

 |
|Access control|You can use RAM to authorize sub-account to perform operations in NAS. You can also use use permission groups to control user access.| [Use RAM to grant RAM users the NAS permission](../../../../reseller.en-US/User Guide/Use RAM to grant RAM users the NAS permission.md#)

 [Use permission groups](../../../../reseller.en-US/User Guide/Use permission groups.md#)

 |
|Back up a file system|NAS backup service is released for public test. You can use the service to back up a NAS file system.| |
|Migrate data to NAS|When using NAS, You must migrate data from local or OSS to NAS.| |
|Use NAS APIs|NAS provides various API interfaces that allow you to perform various operations on a file system.|[API overview](../../../../reseller.en-US/API reference/API overview.md#)|

## Scenarios {#section_dsc_m35_2fb .section}

NAS applies to the following scenarios:

-   Shared storage and high availability for SLB

    If your Server Load Balancer is connected to multiple ECS instances, the applications on these ECS instances store the data on the shared NAS for data sharing and high availability of the load balancing servers.

-   File sharing

    If numerous individuals need access to the same files, your administrator can create a NAS file system for shared access to the data, and grant users or groups of users access to files or directories as needed.

-   Data backup

    Alibaba Cloud NAS allows you to back up your local offline data to the cloud while retaining file access interface compatibility between the two data points.

-   Server logs sharing

    Server logs of applications on multiple computing nodes are stored on the shared NAS to facilitate concentrated processing and analysis of logs in the future.


## Pricing {#section_dp3_kj5_2fb .section}

NAS is billed based on the actual usage in two methods: pay-as-you-go and subscription.

For detailed pricing information, see [Billing method](../../../../reseller.en-US/Pricing/Billing method.md#).

