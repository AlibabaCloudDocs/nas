# Apsara File Storage NAS Performance {#concept_61136_zh .concept}

This topic describes the features, specifications, and scenarios of Apsara File Storage NAS Performance. You can select the storage type based on your business requirements.

Apsara File Storage NAS Performance is backed by solid-state drives \(SSDs\), providing high throughput, high IOPS, and low latency performances for workloads. It is a shared file storage service that is applicable to scenarios that require high throughput, elasticity, and low latency of read operations. You can use this solution if you have frequent read/write operations and high requirements over system response performance.

## Features {#section_qaj_omr_lnj .section}

-   Scalable capacity and a throughput \(up to 20 GB/s\) that enjoys linear scaling along with capacity.
-   A maximum throughput of 600 MB/s for a single TB and milliseconds of latency.
-   Improved performance, applicable to businesses that require large capacity and high throughput.

## Specifications {#section_cqq_o70_yd4 .section}

-   Capacity: 1 PB
-   Latency: A latency of milliseconds
-   IOPS: up to 30,000 \(4,000 random read/write\)
-   Throughput: linear scaling along with capacity, applicable to computing businesses that require large capacity, high throughput, and low latency

## Scenarios {#section_gao_gen_dow .section}

Random I/O access, data-intensive, and latency-sensitive businesses, such as enterprise applications, websites, and containers.

## Throughput calculation {#section_vso_u96_m1b .section}

The maximum throughput of an Apsara File Storage NAS Performance file system \(MB/s\) = 0.6 MB/s × storage space of the file system \(GB\) + 600 MB/s \(initial bandwidth\). The maximum throughput is 20 GB/s.

