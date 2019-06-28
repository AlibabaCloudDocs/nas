# NFS 客户端已知问题 {#concept_zzg_t32_jhb .concept}

NFS 客户端为内核的一部分，由于部分内核存在一些缺陷，会影响 NFS 的正常使用。为了获得更好的 NFS 稳定性体验，请使用阿里云推荐的内核版本。

## 推荐 Linux 系统版本 {#section_5ti_22q_ew2 .section}

推荐使用阿里云官方内核镜像，选择经过阿里云严格测试的内核版本，确保稳定性，如下所示。

-   CentOS 6.9 及以上
-   Redhat 6.9 及以上
-   Ubuntu 14.04 / 16.04 / 18.04
-   Debian 8 及以上
-   SUSE 11 及以上
-   OpenSUSE 42.3 及以上
-   AliyunLinux 17 及以上

## 内核网络栈缺陷导致文件系统无响应（优先级：高） {#section_i3z_hje_dhq .section}

当系统的内核版本为 2.6.32-696 ~ 2.6.32-696.10.1 时，NFS 服务端繁忙，内核请求重传，有概率触发内核网络栈缺陷，造成操作无响应。

当操作无响应时，请重启 ECS 实例，详情请参见 [RHEL6.9: NFSv4 TCP transport stuck in FIN\_WAIT\_2 forever](https://access.redhat.com/solutions/3053801)。

## 内核缺陷导致文件系统无响应（优先级：高） {#section_g0k_uvc_9ei .section}

当系统的内核版本为以下几个版本时，NFS 服务端故障转移，可能造成 NFS 客户端的打开/读/写操作出现死锁情况，从而导致文件系统持续无响应。

-   Redhat 6/CentOS 6 2.6.32-696.3.1.el6。
-   Redhat 7/CentOS 7 3.10.0-229.11.1.el7 之前的所有内核版本。
-   Ubuntu 15.10 Linux 4.2.0-18-generic。

当操作无响应时，请重启 ECS 实例，详情请参见[RHEL7: NFSv4 client loops with WRITE / NFS4ERR\_STALE\_STATEID - if NFS server restarts multiple times within the grace period](https://access.redhat.com/solutions/1427473)。

## 不支持 chown 命令和系统调用（优先级：低） {#section_78h_hzk_1vs .section}

系统的内核版本为 2.6.32 时，不支持NFS客户端执行 chown 命令和系统调用。

## ls 操作无法终止（优先级：低） {#section_2iz_ytx_alx .section}

当系统的内核版本为 2.6.32-696.1.1.el6 及之前版本时，在系统中执行 ls 操作的同时还在进行添加、删除文件/子目录操作，将导致 ls 操作永远无法终止。

请升级内核版本，避免此问题。

