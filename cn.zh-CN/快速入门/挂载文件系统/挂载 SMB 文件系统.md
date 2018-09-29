# 挂载 SMB 文件系统 {#concept_zb5_1rh_cfb .concept}

您可以在 Windows 系统中将 NAS 的 SMB 文件系统挂载至 ECS 实例。

## 前提条件 {#section_zlq_3j1_dfb .section}

将 SMB 文件系统挂载至 ECS 实例前，需要确保 Windows 系统服务中的以下两项服务均已启动：

-   Workstation
-   TCP/IP NetBIOS Helper

## 挂载命令 {#section_pgk_srh_cfb .section}

您可以运行以下格式的命令，挂载 SMB 文件系统：

```
net use <挂载目标盘符> \\<挂载点域名>\myshare
```

## 参数说明 {#section_skz_dsh_cfb .section}

-   挂载目标盘符： 在当前 Windows 机器上要挂载的目标盘符。在盘符和 use 以及\\\\间需要加空格。
-   挂载点域名：指创建文件系统的挂载点时，自动生成的挂载点域名。
-   myshare：固定的 SMB share 名称，不能改变。

## 命令示例 {#section_dyj_bsh_cfb .section}

如果您需要将 SMB 文件系统挂载到盘符 Z，可以运行以下命令：

```
C:\> net use z: \\file-system-id-xxxx.region.nas.aliyuncs.com\myshare

```

## 查看挂载信息 {#section_ypf_4sh_cfb .section}

挂载完成后，您可以在 Windows 命令行工具中运行以下命令查看已挂载的文件系统：

```
net use
```

