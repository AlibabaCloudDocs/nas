# Apsara File Storage NAS Capacity {#concept_1012851 .concept}

This topic describes the features, specifications, and scenarios of Apsara File Storage NAS Capacity. You can select the storage type based on your business requirements.

Apsara File Storage NAS Capacity is backed by SATA hard disk drives \(SATA HDDs\), providing high-performance storage at relatively low costs. It is a shared file storage service that is applicable to cost-sensitive scenarios that require high throughput and elasticity. You can adopt this cost-efficient solution if you have infrequent read/write operations and moderate latency requirements over your storage resources.

## Features {#section_iyl_1y5_bj7 .section}

-   Scalable capacity and a throughput \(up to 10 GB/s\) that enjoys linear scaling along with capacity.
-   A maximum throughput of 150 MB/s for a single TB and maximum latency of 10 ms.
-   Improved performance, applicable to businesses that require large capacity and high throughput.

## Specifications {#section_rce_ktv_808 .section}

-   Capacity: 10 PB
-   Latency: 10 ms
-   IOPS: up to 15,000 \(4,000 random read/write\)
-   Throughput: linear scaling along with capacity, applicable to computing businesses that require large capacity and high throughput but moderate latency requirements

## Scenarios {#section_kyg_ar8_qh3 .section}

Scalable capacity and cost-sensitive applications, such as big data analysis, file sharing, and data backup.

## Throughput calculation {#section_y60_ioh_l2h .section}

The maximum throughput of an Apsara File Storage NAS Capacity file system \(MB/s\) = 0.15 MB/s × storage space of the file system \(GB\) + 150 MB/s \(initial bandwidth\). The maximum throughput is 10 GB/s.

