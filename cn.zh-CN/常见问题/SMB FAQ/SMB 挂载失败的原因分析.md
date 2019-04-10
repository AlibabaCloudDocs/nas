# SMB 挂载失败的原因分析 {#concept_fpq_xwf_2hb .concept}

Windows 系统挂载 SMB 失败时的解决步骤如下。

1.  确认挂载命令是否正确，是否是有多余的 `/` 、缺少`\`或者缺少空格，另外注意不要遗漏myshare。挂载 SMB 文件系统的正确命令格式应该为：

    ```
    net  use  <挂载目标盘符>  \\<挂载点域名>\myshare
    ```

2.  确认 Windows 系统版本。目前我们只支持 Windows 2008 R2 及以上版本， 不支持 Windows 2008。

    **说明：** Windows 2016 以后版本请参见[SMB 挂载常见问题](cn.zh-CN/常见问题/SMB FAQ/SMB 挂载常见问题.md#)。

3.  确认文件系统类型是 SMB，目前不能通过 SMB 协议挂载 NFS 文件系统。如图：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/155486034441401_zh-CN.png)

4.  确认文件系统挂载点权限组是否包含该机器的内网 IP / VPC IP。
5.  经典网络挂载时，确认 ECS 和 NAS 属于同一阿里云 UID 。
6.  确认阿里云 UID 是否处于欠费状态。
7.  ping 挂载地址检查是否能通，延时是否正常。
8.  如果可以 ping 通，测试`telnet <挂载点域名> 445`是否可以连通。
9.  确认机器上 TCP/IP netBIOS 以及 workstation 服务是否都已经打开。

