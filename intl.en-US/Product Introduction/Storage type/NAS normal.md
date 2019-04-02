# NAS normal {#concept_71454_zh .concept}

NAS normal is the most common storage type in NAS. NAS normal can be easily used without a local client and can meet the file storage requirements in daily business.

## Introduction {#section_yhk_zm5_2fb .section}

NAS normal provides two product types: capacity type and SSD performance type. The two types use different storage media and are different in performance, protocol compatibility, and billing. The differences between the two types are described as follows:

-   The NAS SSD performance type focuses on performance and aims to provide storage with higher throughput \(four times that of the capacity type\), higher IOPS, and lower latency \(two to four times lower than the capacity type\) for workloads.
-   The NAS capacity type focuses on the cost and aims to provide efficient and reliable storage with a lower cost for workloads.

## Application scenarios {#section_kh2_dn5_2fb .section}

NAS normal can meet the file storage requirements of daily business in various file storage scenarios:

-   File sharing in business systems
-   Log storage and analysis in business systems
-   Development and test data storage in business systems
-   Enterprise database backup and storage
-   Back-end file storage in Office Automation \(OA\) systems
-   Website data storage and distribution

You can select NAS capacity type or NAS SSD performance type based on your application scenarios.

-   In scenarios where high throughput or low latency is required, for example, scenarios where file operations are frequently performed or file modifications must take effect immediately, you can use the NAS SSD performance type to ensure storage performance.
-   In scenarios where large storage capacity is required without high performance requirements, for example, the static backup of a large number of files, you can use the NAS capacity type to reduce storage costs.

## Specification comparison {#section_dtd_hn5_2fb .section}

The following table compares the performance indicators, supported protocols, and billing methods of the NAS capacity type and NAS SSD performance type. You can use this table as a reference when selecting the product types.

|Item|NAS SSD performance type|NAS capacity type|
|----|------------------------|-----------------|
|Storage medium|SSD|SSD + SATA HDD|
|Maximum throughput \(MB/s\)|0.58 MB/s x File system storage capacity \(GB\) + 600 MB/s \(20 GB/s in maximum\)|0.14 MB/s x File system storage capacity \(GB\) + 150 MB/s \(10 GB/s in maximum\)|
|Maximum IOPS|50,000|15,000|
|Supported protocols|NFS \(v3.0/v4.0\), SMB \(v2.0/v2.1/v3.0\)|NFS \(v3.0/v4.0\), SMB \(v2.0/v2.1/v3.0\)|
|Billing method|Pay-As-You-Go and storage packages are supported. You can choose whether to bind a storage package when creating a file system.|You must bind a storage package to use the NAS capacity type. If the actual storage capacity exceeds the package capacity, the exceeded part is billed using Pay-As-You-Go.|

## Billing method { .section}

For detailed billing methods for NAS, see NAS pricing.

