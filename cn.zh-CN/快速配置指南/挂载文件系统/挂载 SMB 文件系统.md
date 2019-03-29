# 挂载 SMB 文件系统 {#concept_zb5_1rh_cfb .concept}

您可以在 Windows 系统中将 NAS 的 SMB 文件系统挂载至 ECS 实例。

## 前提条件 {#section_zlq_3j1_dfb .section}

将 SMB 文件系统挂载至 ECS 实例前，需要确保 Windows 系统服务中的以下两项服务均已启动：

-   Workstation

    Workstation 服务默认为启动状态。查看方式如图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/155385277842055_zh-CN.png)

    选择**所有程序** \> **附件** \> **运行**或使用快捷键`Win+R`，输入`services.msc`进入本地服务。在服务中找到 Workstation，双击查看运行状态。

-   TCP/IP NetBIOS Helper

    开启 TCP/IP NetBIOS Helper 服务步骤如下：

    1.  打开**网络与共享中心**，单击主机所连网络。
    2.  打开网络属性，双击 **Internet 协议版本 4**进入属性框，单击**高级**。
    3.  在高级 TCP IP 对话框中，选择 **WINS** \> **启用 TCP/IP 上的 NetBIOS**。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/155385277942056_zh-CN.png)


## 挂载命令 {#section_pgk_srh_cfb .section}

您可以运行以下格式的命令，挂载 SMB 文件系统：

```
net use <挂载目标盘符> \\<挂载点域名>\myshare
```

-   挂载目标盘符： 在当前 Windows 机器上要挂载的目标盘符。在盘符和 use 以及 \\\\ 间需要加空格。

    **说明：** 目标盘符不要和本地盘符重名。

-   挂载点域名：指创建文件系统的挂载点时，自动生成的挂载点域名。

    更多挂载点详情请参见[添加挂载点](cn.zh-CN/快速配置指南/添加挂载点.md#)。

-   myshare：固定的 SMB share 名称，不允许变更。

**说明：** 网络互通时，可以将 NAS 的 SMB 文件系统挂载至本地 Windows 主机，详情请参见[挂载前注意事项](cn.zh-CN/快速配置指南/挂载文件系统/挂载前注意事项.md#)。

## 命令示例 {#section_dyj_bsh_cfb .section}

如果您需要将 SMB 文件系统挂载到盘符 Z，可以运行以下命令：

```
 net use z: \\file-system-id-xxxx.region.nas.aliyuncs.com\myshare

```

## 查看挂载信息 {#section_ypf_4sh_cfb .section}

挂载完成后，您可以在 Windows 命令行工具中运行以下命令查看已挂载的文件系统：

```
net use
```

