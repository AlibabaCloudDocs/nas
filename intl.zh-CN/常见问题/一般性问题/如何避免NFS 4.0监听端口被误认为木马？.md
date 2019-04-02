# 如何避免NFS 4.0监听端口被误认为木马？ {#concept_65281_zh .concept}

## 问题现象 {#section_x2t_3bh_hfb .section}

使用NFS 4.0挂载NAS文件系统后，有一个0.0.0.0的随机端口被监听，并且无法通过netstat定位该监听端口的进程。

由于端口不固定，并且无法确定监听的程序，很容易被误判为受到木马攻击。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18748/153959009113103_zh-CN.jpg)

## 问题原因 { .section}

此随机端口是NFS 4.0为了支持callback而监听的。因为内核参数fs.nfs.nfs\_callback\_tcpport默认是0，所以NFS 4.0 client会随机挑选一个端口进行监听，而随机端口本身并不会带来安全风险。

不过为了更方便地管理端口，用户可以选择使用以下方法固定该callback端口。

## 解决方案 { .section}

在挂载文件系统之前，用户可以通过配置参数fs.nfs.nfs\_callback\_tcpport到一个非零的确定值，以固定该端口。

```
sudo sysctl fs.nfs.nfs_callback_tcpport=<port>

```

在以下示例中，在用户将fs.nfs.nfs\_callback\_tcpport手动配置到端口45450，并使用NFS 4.0挂载文件系统之后，netstat显示被监听的端口就是手动配置的45450。

\(请注意以下实例中使用的是root用户，所以不需要使用sudo执行sysctl命令。\)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18748/153959009113104_zh-CN.jpg)

