# Functions and features {#concept_60367_zh .concept}

Alibaba Cloud NAS supports NFSv3 and NFSv4 protocols and uses standard file system syntax for data access. Mainstream apps and work loads can be integrated for seamless use without any modifications required.

## Shared access { .section}

Multiple computing nodes can visit the same file system instance at the same time, which is suitable for use cases where apps are deployed across multiple ECS, HPC or Docker instances and need to visit the same data source.

## Auto scaling { .section}

A single file system has a capacity ceiling of 1 petabyte and is charged by actual usage, fully meeting the requirements for elastic scalability.

## Security control { .section}

Multiple security mechanisms are in place including network isolation \(VPC\)/user isolation \(classic network\), file system standard permission control, permission group access control and RAM master account and sub-account authorization to ensure data security in the file system.

## Linear expansion performance { .section}

Alibaba Cloud NAS is able to provide high-throughput, high-IOPS and low-latency storage for app work loads. Meanwhile, the linear relationship between performance and capacity can meet capacity and storage performance requirements arising from business growth.

## Strong consistency { .section}

Support for strong consistency, after any modification to the file has been successfully returned, other subsequent visits will see the final result immediately.

