# SMB协议限制说明 {#concept_67161_zh .concept}

NAS 支持 SMB 协议，但目前还不支持少部分 SMB 的功能。

## 简介 {#section_kyd_wcb_hfb .section}

SMB 全称 Server Message Block，又称 CIFS（Common Internet File System，主要指SMB2之前的SMB协议），是一种用来访问网络中文件、打印机和其他共享网络资源的应用层通信协议。在阿里云 NAS 文档中，SMB 指代 NAS 支持的 SMB 2.0 及以上的各个 SMB 协议版本。

与NFS相比，SMB文件系统访问协议更加适用于Windows客户端。各个版本的Windows对SMB协议的支持更加完善，绝大多数Windows应用程序不经修改即可通过SMB协议访问阿里云文件存储服务。阿里云建议应用程序集中运行在Windows客户端的用户优先考虑使用SMB文件系统。

## 主要特性 {#section_ogq_xcb_hfb .section}

SMB主要特性如下：

-   支持SMB 2.0及以上的SMB协议版本，支持Windows Vista / Windows Server 2008及以上的各Windows版本，不支持Windows XP / Windows Server 2003及以下的各Windows版本。做出这一选择的主要原因是与SMB 2.0 及以后的版本相比，SMB 1.0由于协议设计的巨大差异导致在性能和功能上有严重的不足，并且只支持SMB1.0或更早协议版本的Windows产品已经完全退出微软支持的生命周期。

-   文件系统容量和性能线性扩展，单一命名空间；单文件系统最大容量达PB级别，最大文件个数10亿。

-   支持VPC和经典网络环境中的安全访问控制，保障用户数据的私密性。提供挂载点权限组，控制台访问（管控API）支持RAM。

-   访问方式：每个挂载点只提供一个share, 统一命名为 myshare。用户用`\\mount_point\myshare`来访问这个SMB share。用户的多个虚拟机可以在阿里云的经典网络或VPC网络中同时访问同一个SMB文件系统。

-   与NFS文件系统基于同一个分布式高可用的底层文件系统，提供一致的SLA保证。文件数量和长度的支持限制也与NFS一致。


## 功能限制 {#section_wfn_1db_hfb .section}

由于客户端的多样性和复杂性，在现阶段不支持少部分SMB功能。这些不支持的功能对大多数应用的运行没有影响。目前不支持的功能如下：

-   不支持Linux客户端访问。

-   不支持用户用NFS和SMB访问同一个文件系统，不支持通过广域网直接访问SMB文件系统。

-   只提供在文件系统级别的读写权限控制，不提供文件/目录级别的ACL权限控制。

-   不支持文件扩展属性（Extended attributes）以及基于Oplocks和Lease的客户端缓存。

-   不支持Sparse files、文件压缩、网卡状态查询、重解析点（Reparse Point）等IOCTL/FSCTL操作。

-   不支持交换数据流（Alternate Data Streams）。

-   不支持SMB Direct、SMB Multichannel、SMB Directory Leasing、Persistent File Handle等SMB 3.0及以上版本的一些协议功能。


