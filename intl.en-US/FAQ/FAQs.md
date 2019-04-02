# FAQs {#concept_b32_qx2_2hb .concept}

## What is CPFS? {#section_uqj_rx2_2hb .section}

Alibaba Cloud CPFS is an expandable parallel file system that meets the requirements for high-performance computational scenarios. CPFS provides a unified namespace that enables concurrent access from hundreds of thousands of clients. The performance of a CPFS file system can reach a throughput of hundreds of Gbit/s, an IOPS of millions, and sub-millisecond level latency.

## What are the most applicable scenarios for CPFS? {#section_sgp_cy2_2hb .section}

CPFS can meet the file storage requirements for computing-intensive scenarios, such as machine learning, big data analysis, media processing, and high-performance computational \(HPC\) scenarios including DNA sequencing, hydrocarbon exploration, and meteorological reanalysis.

## How can I activate CPFS and create a CPFS file system? {#section_fdr_py2_2hb .section}

If you have signed in Alibaba Cloud, after activating Network Attached Storage \(NAS\), you can log on to the [NAS console](https://nas.console.aliyun.com/) to activate CPFS. If you need to use CPFS, you must first subscribe to a CPFS package to create a CPFS file system. In general, it takes several minutes to create a file system. After the file system is created, you can use computational instances to access and use the file system.

## How can I access a CPFS file system by using computational instances? {#section_cqh_gz2_2hb .section}

You must download and install a [CPFS client](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/108096/cn_zh/1553564531232/cpfs-client-1.2.1-centos.x86_64.rpm) on a computational instance, and then mount a CPFS file system on the instance.

## How can I access and process Object Storage Service \(OSS\) files in a CPFS system? {#section_uhl_fdb_fhb .section}

You can download OSS files to a CPFS file system for processing by using the ossutil tool.

## Is CPFS compatible with the Portable Operating System Interface \(POSIX\)? {#section_b34_vz2_2hb .section}

Yes, CPFS is compatible with POSIX.

## How can I purchase CPFS? Which specifications are available? {#section_vdz_21f_2hb .section}

You must subscribe to a CPFS package to create a file system with a certain specification. You can select a file system specification of 50 TB, 100 TB, or 150 TB. Each specification has a duration of one month, six months, or one year, respectively.

