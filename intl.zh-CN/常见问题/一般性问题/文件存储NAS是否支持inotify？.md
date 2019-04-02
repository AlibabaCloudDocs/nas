# 文件存储NAS是否支持inotify？ {#concept_48118_zh .concept}

使用 inotifywait 配合 rsync 是一种常见的准实时数据备份/同步方案，但在NAS文件系统上 inotifywait 无法正常工作，这是由于 inotify 本身的实现机制导致的。

## inotifywait 原理简介 {#section_rhv_ngh_hfb .section}

inotifywait 是Linux 内核子模块 inotify 的用户态接口实现，inotify 实现在 VFS 层，当文件操作到达 VFS 层时，inotify 模块会将操作类型（创建/删除/属性改变等）和操作对象（文件名）反馈给用户态，用户态的 inotifywait 即可将本次操作信息输出给用户。

## NAS 上使用 inotifywait 存在的问题 {#section_q5f_qgh_hfb .section}

由于 inotify 是在 kernel 的 VFS 层实现的，因此在 NFS 文件系统上，远程客户端对 NFS 文件系统的操作无法被本地 kernel 所感知，inotify 也就无法感知远程客户端的文件修改操作。

因此，在 NAS 上使用 inotifywait 会出现以下现象：

-   在客户端 A 和 B 同时挂载一个 NAS 文件系统，在客户端 A 启动 inotifywait 监听挂载目录。
-   在客户端 A 上操作挂载目录中的文件，可以被 inotifywait 感知。
-   在客户端 B 上操作挂载目录中的文件，inotifywait 无法感知任何文件操作。

## 替代方案 {#section_mgy_dhh_hfb .section}

一个可行的替代方案是使用 [FAM](http://oss.sgi.com/projects/fam/doc.html)， FAM 是一个用来监听文件或目录的库，全部在用户态实现，原理是在后台运行一个 daemon，定时扫描目录，获取文件变化情况。

但是使用 FAM 存在以下几个缺陷：

-   需要自己写程序调用 FAM 接口实现功能。
-   对于文件数目很多的场景，使用该方案性能会较差，可能消耗大量资源，无法做到很好的实时性。

