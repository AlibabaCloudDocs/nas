# SMB 文件系统限制 {#concept_h2x_4t3_wfb .concept}

本文档介绍 SMB 文件系统的使用限制。

SMB 文件系统的使用限制如下：

-   支持 SMB 2.1 及以上的 SMB 协议版本，支持 Windows 7/ Windows Server 2008 R2 及以上的各 Windows 版本，不支持 Windows Vista / Windows Server 2008 及以下的各 Windows 版本。与 SMB 2.1 及以后的版本相比，SMB 1.0 由于协议设计的巨大差异导致在性能和功能上有严重的不足，并且只支持 SMB1.0 或更早协议版本的 Windows 产品已经完全退出微软支持的生命周期。
-   访问方式：每个挂载点只提供一个 share， 统一命名为 myshare，并使用 \\\\mount\_point\\myshare 来访问 SMB share。您的多个虚拟机可以在阿里云的经典网络或 VPC 网络中同时访问同一个 SMB 文件系统。
-   只对文件系统级别、而不对文件/目录级别提供 ACL 权限控制。

