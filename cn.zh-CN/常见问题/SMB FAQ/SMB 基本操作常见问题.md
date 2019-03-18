# SMB 基本操作常见问题 {#concept_ufh_bbz_bhb .concept}

## 为什么用 net use 会看到 mount 点处于已断开状态 {#section_ltg_dbz_bhb .section}

如果15分钟内在文件系统上没有操作，连接会自动断开。只要有操作，连接自动重连。

## CIFS/SMB文件系统的容量和性能如何？ {#section_is4_wbz_bhb .section}

现在 SMB 文件系统是部署在容量型 NAS 集群上的，所以单文件系统的容量上限和带宽上限与容量型 NAS 是一样。 其他属性，比如对单一命名空间，VPC、经典网络的支持等，都和 NFS 是一样的。

详情请参见[文件 NAS](https://www.aliyun.com/price/product#/nas/detail)。

## SMB 文件系统支持的协议和操作系统 {#section_g5j_bdz_bhb .section}

SMB 文件系统支持的协议和 ECS OS的详情请参见[SMB 协议限制说明](../../../../../cn.zh-CN/使用限制/SMB 文件系统限制.md#)。

SMB 文件系统不支持的特性请参见[SMB 文件系统不支持特性](../../../../../cn.zh-CN/使用限制/SMB 文件系统不支持特性.md#)。

## 访问 SMB 文件系统的一些限制 {#section_ecq_5dz_bhb .section}

同 NFS 文件系统一样，不能跨 region 访问，不能直接通过公网访问，需要专线连到 VPC。

如果需要在有文件系统挂载点的VPC之外访问，请参见：

-   [本地IDC VPN网络访问阿里云文件存储](../../../../../cn.zh-CN/最佳实践/远程访问文件系统/本地IDC VPN网络访问阿里云文件存储.md#)
-   [本地IDC NAT网络访问阿里云文件存储](../../../../../cn.zh-CN/最佳实践/远程访问文件系统/本地IDC NAT网络访问阿里云文件存储.md#)
-   [跨 VPC 挂载阿里云文件存储 NAS](../../../../../cn.zh-CN/最佳实践/远程访问文件系统/跨 VPC 挂载阿里云文件存储 NAS.md#)
-   [跨账户挂载阿里云文件存储NAS](../../../../../cn.zh-CN/最佳实践/远程访问文件系统/跨账户挂载阿里云文件存储 NAS.md#)

