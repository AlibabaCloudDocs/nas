# SMB 文件系统不支持特性 {#concept_hql_pnj_wfb .concept}

本文档介绍 SMB 文件系统的一些不支持特性。

SMB 文件系统不支持的特性如下：

-   不支持 Linux 客户端访问。
-   不支持使用 NFS 和 SMB 访问同一个文件系统，不支持通过广域网直接访问 SMB 文件系统。
-   不支持文件扩展属性（Extended attributes）以及基于 Oplocks 和 Lease 的客户端缓存。
-   不支持 Sparse files、文件压缩、网卡状态查询、重解析点（Reparse Point）等 IOCTL/FSCTL 操作。
-   不支持交换数据流（Alternate Data Streams）。

