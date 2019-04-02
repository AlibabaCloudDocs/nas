# Introduction to CPFS {#concept_66278_zh .concept}

Cloud Paralleled File System \(CPFS\) is a parallel file system. CPFS stores data across multiple data nodes in a cluster and allows the data to be simultaneously accessed by multiple clients. Therefore, it can provide data storage services with high IOPS, high throughput, and low latency for large-scale, high-performance computer clusters.

With the large-scale commercial use of high-performance parallel computing, traditional parallel file systems face many challenges. For example, the steep growth of storage resources results in high costs and complex operation and maintenance. Also, the stability and other performance indicators of large-scale storage systems cannot expand linearly with the increasing system scale. CPFS is introduced to address the above issues.

## Features {#section_my5_fcb_hfb .section}

-   Ultra-high throughput and IOPS

    CPFS provides an IOPS of 100,000,000 and a throughput of 1 Tbit/s.

    CPFS evenly distributes data strips across the entire storage cluster. Clients can access the data in parallel. The throughput and IOPS linearly increase with the number of storage nodes, enabling the storage cluster to provide ultra-high aggregated bandwidth and IOPS. Additionally, CPFS uses the RDMA over Converged Ethernet \(RoCE\) protocol, which reduces I/O latency and further increases I/O speed.

-   Ultra-high data reliability

    The maximum capacity of a single CPFS file system is 100 PB.

    Based on the architecture of Alibaba Cloud distributed storage system, CPFS persistent storage stores multiple data copies and provides data reliability of 99.99999999%. The reliability is far higher than that of the RAID disk arrays provided by traditional storage vendors.

-   Well-optimized availability

    Traditional parallel file systems provide two-node high-availability \(HA\) mode which must be configured before you deploy a file system. Additionally, manual recovery is required when the two nodes fail at the same time \(reduces file system reliability\). CPFS uses the arbitration and scheduling mechanism based on Paxox Ring. This mechanism can automatically detect abnormal service nodes and switch over the services to other nodes, providing availability of 99.9%.

-   Security

    CPFS provides various security features, such as Access Control List \(ACL\), network isolation, and authorization from the primary account to sub-accounts, to ensure the security isolation of user data.

-   Global namespace

    The cluster uses a unique global namespace, ensuring seamless data access between multiple clients.

-   Data lifecycle management

    Based on business scenarios, user data can be transferred between different Alibaba Cloud storage products, including CPFS, NAS, and OSS.

-   Standard POSIX and MPI data access APIs

    CPFS provides standard POSIX and MPI data access APIs, which allow you to migrate your applications to Alibaba Cloud without any modification. You can use a dedicated leased line together with the APIs to construct a cost-effective hybrid cloud parallel computing environment that locally generates data and remotely processes data in the cloud.

-   On-demand expansion and pay-by-capacity

    The cloud-based scalability of CPFS allows you to expand storage nodes as needed and only pay for the capacity you use. By this means, CPFS can efficiently meet sudden changes in service requirements while reducing TCO.


## Scenarios {#section_ydm_pfx_dhb .section}

CPFS provides numerous benefits, such as high performance, availability, reliability, and scalability. Additionally, CPFS is applicable to various high-performance computational scenarios.

-   Such scenarios include: colleges and universities, scientific research, and medicine.
-   This also applies to traditional large-scale manufacturing: automotive and aviation industries.
-   Other complex computational scenarios include: DNA, big data, and the Internet of Things \(IoT\).

