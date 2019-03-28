# How to use Alibaba Cloud Network Attached Storage {#concept_n2t_lgf_xgb .concept}

This section describes Network Attached Storage \(NAS\) and how it is used.

## What is NAS? {#section_zlq_4gf_xgb .section}

In the domain of storage, NAS is the abbreviation for network attached storage, which is referred to as network-based storage. You can share access to a NAS file system by using Network File System \(NFS\) or Server Message Block \(SMB\) from multiple servers at the same time. Unlike traditional file storage, NAS is a cloud-based distributed file system that provides scalability, high reliability, high availability, and high performance. Dependent on POXIS-based file APIs, NAS provides numerous benefits, such as compatibility with operating systems, shared access, data consistency, exclusive locks, and linear performance with increasing capacity.

## A comparison with NAS, EBS, and OSS {#section_bl3_ngf_xgb .section}

Both NAS and Elastic Block Store \(EBS\) provide computational storage. To access a NAS or EBS file system, you must use POSIX-based APIs and link ECS instances with the file system. The difference between EBS and NAS is the location of each file system. The file system of EBS is integrated with an operating system. However, you can only access the file system of NAS over networks. OSS does not have a dedicated file system. You are only allowed to access OSS by using APIs over networks.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131419/155374582139576_en-US.png)

-   NAS: As NAS has regulated file systems on a storage system, computational nodes can access NAS in the same way they access a local file system by using POSIX-based APIs over networks. NAS supports scalable capacity. You do not need to preserve capacity in advance. Capacity can be scaled based on the amount of actually written data. The file lock mechanism of NAS natively supports shared access. Compared to EBS, NAS has high latency and low IOPS performance due to network issues. Therefore, NAS is mainly applied to shared access scenarios with multiple computational nodes and stateless clusters.
-   EBS: EBS is a type of bare disks, which cannot be directly accessed by an operating system. You must expose block storage as volumes by using RAID or LVM. Then, you can access these volumes by formatting the file system to ext3, ext4, and NTFS.

    EBS offers high performance and low latency. EBS is applicable to I/O-intensive, high-performance, and low-latency data stores, such as OLTP data stores and NoSQL data stores. As EBS capacity is not scalable, the maximum size of a single disk is 32 TB. Additionally, due to limited support for shared access, EBS must work with cluster management applications, such as Oracle RAC and WSFC Windows to enable shared access.

-   OSS: OSS is a new type of storage. Compared to the directory-based tree hierarchy of NAS, OSS uses a flat file hierarchy.

    OSS allows access by RESTful APIs and does not support random reading or writing of data. OSS is mainly applied to upload, download, and distribute large amounts of data over the Internet.


## NAS scenarios {#section_hgg_wjf_xgb .section}

-   Multiple ECS instances share access to NAS

    NAS supports shared access to file storage. Each ECS instance can access NAS in the same way it accesses a local file system and retrieves the same data. This allows data to be automatically synchronized between multiple ECS instances. NAS addresses the issue of data synchronization in clustering mode.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131419/155374582139577_en-US.png)

-   High-performance websites

    The most commonly used architecture for the application platform of a website is a clustering architecture. For each code update, you must deliver the latest version of the website to all clusters. Manually synchronization of code or applications brings low efficiency, high costs, and low fault-tolerance. However, you can quickly deliver and synchronize code by using the shared storage of NAS.

-   Web content management platform

    Content management platforms are mostly Web-based applications with a stateless clustering architecture. A content management platform that uses functions such as rsync to synchronize data, images, and files between servers. This allows an image uploaded from server A to be viewed on server B. However, data cannot be fully synchronized in real time. When a spike in business occurs, synchronized data may be inconsistent. NAS is introduced to easily resolve this issue. When cluster servers simultaneously access the same NAS file storage, data will be automatically shared and synchronized.

-   Shared storage for both developing and testing environments

    With NAS shared storage, you can easily share code between developing and testing environments. You only need to maintain one code base. Note that NAS promotes progress in a developing environment, compiling and uploading to CI for integration, and releasing code without the labor-intensive task of copying code. Therefore, NAS shared storage is flexible and quick to meet customer needs.

-   Container storage

    A container is an indispensable component of a micro-service. A container can be preconfigured, is portable, and provides thread isolation. Each time you start a container, you must ensure access to original data and enable a shared file system. In this situation, whichever instance a container runs, the container can connect to the file system. Many data applications require persistent and local storage of a container. Shared file storage is the best option for containers that have a steep growth in demand for persistent storage. NAS supports data sharing between multiple pods. You can switch between containers to ensure high availability. NAS features scalable capacity and can meet the container requirements for business flexibility.

-   High-performance computing

    NAS features high bandwidth and IOPS, which is mainly applied to high-performance computational scenarios.

    For example, NAS can be applied to concurrent computing with large-scale computational node-based scenarios, such as High-performance computing \(HPC\), artificial intelligence \(AI\) self-driving, simulation, and DNA sequencing. These scenarios require a unified name space and high-performance shared access to file storage.


## How to select the appropriate type of NAS {#section_azs_1lf_xgb .section}

NAS has multiple storage types. For various application models, we recommend that you select the most appropriate storage type to derive the best performance from NAS. The features and scenarios of various NAS types are described as follows.

|Type|Feature|Scenario|
|----|-------|--------|
|NAS Capacity| High capacity, low cost, and scalability.

 Latency: 3-10ms.

 |File sharing, content management, and backup.|
|NAS Performance| High capacity and scalability.

 Latency: 1-2ms.

 |File sharing, containers, and big data analysis.|

