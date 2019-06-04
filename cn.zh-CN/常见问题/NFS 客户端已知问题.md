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

## 网络抖动导致文件系统无响应 {#section_i3z_hje_dhq .section}

当系统内核版本为以下两种情况时，NFS 客户端遇到网络抖动、服务端故障切换等情况，可能会触发 TCP 连接异常，导致 NFS 连接中断。

**说明：** 您可以通过uname-a命令查看内核版本。

-   内核版本低于 2.6.32-696.16.1（不包括 2.6.32-696.16.1 版本）。
-   内核版本高于 2.6.32-696.16.1（包括 2.6.32-696.16.1 版本），但是 NFS 挂载没有使用 noresvport 选项。

当发生连接异常后，需要在 ECS 实例上重新执行挂载操作。挂载操作请参见[在 Linux 系统中挂载 NFS 文件系统](../../../../intl.zh-CN/快速配置指南/挂载文件系统/挂载 NFS 文件系统/在 Linux 系统中挂载 NFS 文件系统.md#)，使用推荐的参数进行挂载。

使用 noresvport选项进行挂载后，请执行`ss -ant| grep 2049`命令检查端口号，如下图框选部分所示，端口号大于1024，说明挂载生效。反之，请先卸载所有已挂载的文件系统（执行`mount | grep nas`命令确保已不存在挂载），再进行重新挂载。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/156759/155963278546656_zh-CN.png)

**注意：** 请避开使用 2.6.32-696 ~ 2.6.32-696.10.1 版本的内核，该版本发生文件系统无响应的概率高于其他内核版本，详情请参见[RHEL6.9: NFSv4 TCP transport stuck in FIN\_WAIT\_2 forever](https://access.redhat.com/solutions/3053801)。

## 内核缺陷导致文件系统无响应 {#section_g0k_uvc_9ei .section}

当系统的内核版本为以下几个版本时，NFS 服务端故障转移，可能造成 NFS 客户端的打开/读/写操作出现死锁情况，从而导致文件系统持续无响应。

-   Redhat 6/CentOS 6 2.6.32-696.3.1.el6。
-   Redhat 7/CentOS 7 3.10.0-229.11.1.el7 之前的所有内核版本。
-   Ubuntu 15.10 Linux 4.2.0-18-generic。

当操作无响应时，请重启 ECS 实例，详情请参见[RHEL7: NFSv4 client loops with WRITE / NFS4ERR\_STALE\_STATEID - if NFS server restarts multiple times within the grace period](https://access.redhat.com/solutions/1427473)。

## 不支持 chown 命令和系统调用 {#section_78h_hzk_1vs .section}

系统的内核版本为 2.6.32 时，不支持NFS客户端执行 chown 命令和系统调用。

## ls 操作无法终止 {#section_2iz_ytx_alx .section}

当系统的内核版本为 2.6.32-696.1.1.el6 及之前版本时，在系统中执行 ls 操作的同时还在进行添加、删除文件/子目录操作，将导致 ls 操作永远无法终止。

请升级内核版本，避免此问题。

