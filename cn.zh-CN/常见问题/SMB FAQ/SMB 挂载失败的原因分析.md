# SMB 挂载失败的原因分析 {#concept_fpq_xwf_2hb .concept}

本文主要介绍在 Windows 系统中挂载 SMB 文件系统挂载失败时可能的原因及解决方案。

## 系统错误 53 {#section_kkp_c4t_s32 .section}

**错误描述**

找不到网络路径。

**主要原因**

网络未连通或TCP/IP NetBIOS Helper服务未启动。

**解决方法**

请根据如下步骤进行排查。

1.  使用ping 命令检查挂载点地址是否可连通，延时是否正常。

    ping <挂载点地址\>

    -   若网络 ping 通，则执行[步骤 2](#li_c2c_vh8_ugj)。
    -   若网络 ping 不通，请从以下方面排查。
        -   确认挂载命令正确，无多余或缺少 `/` 、`\`、空格及myshare等内容。

            正确挂载 SMB 文件系统的命令格式：

            ``` {#codeblock_at9_yzk_jn6}
            net use <挂载目标盘符> \\<挂载点地址>\myshare
            ```

            样例：

            ``` {#codeblock_asi_1za_86c}
            net use z: \\xxxx.cn-hangzhou.nas.aliyuncs.com\myshare 
            ```

        -   确认文件系统类型为 SMB。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/156507780641401_zh-CN.png)

        -   确认挂载点地址填写正确。
        -   确认客户端的 ECS 与挂载点在同一个 VPC 中。
        -   确认跨 VPC 或通过 VPN 连入的客户端，网络配置正确。
2.  使用 telnet命令检查 SMB 服务是否可用。

    telnet <挂载点地址\> 445

3.  确认是否已启动 TCP/IP NetBIOS Helper 服务，具体操作请参见[手动挂载SMB文件系统](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载SMB文件系统.md#)。

## 系统错误 58 {#section_hc3_y35_loh .section}

**错误描述**

指定的服务器无法运行请求的操作。

**主要原因**

客户端 SMB 协议版本支持不兼容。

**解决方法**

请确认 Windows 系统版本为Windows 2008 R2 及以上版本（不包括 Windows 2008）。

## 系统错误 64 {#section_3fa_9qy_l9f .section}

**错误描述**

指定的网络名不可用。

**主要原因**

-   NAS 权限组未允许目标 ECS 访问。
-   服务欠费。
-   选择经典网络进行挂载时， ECS 和 NAS 不属于同一阿里云 UID。
-   文件系统类型不是 SMB。

**解决方法**

无权访问 NAS 文件系统资源，请从以下方面进行排查。

1.  确认文件系统挂载点权限组已包含该机器的内网 IP/VPC IP。
2.  确认阿里云 UID 未欠费。
3.  确认经典网络挂载时， ECS 和 NAS 属于同一个阿里云UID。
4.  确认文件系统类型为 SMB。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/149028/156507780641401_zh-CN.png)


## 系统错误 67 {#section_2xt_2ks_so0 .section}

**错误描述**

找不到网络名。

**主要原因**

关键的网络服务未启动。

**解决方法**

启动如下服务，具体操作可参见[挂载SMB文件系统](../../../../intl.zh-CN/控制台用户指南/挂载文件系统/手动挂载SMB文件系统.md#section_zlq_3j1_dfb)。

1.  启用 Workstation 服务。
2.  启用 TCP/IP NetBIOS Helper 服务。

## 系统错误 85 {#section_dsx_7nn_yn0 .section}

**错误描述**

本地设备名已在使用中。

**主要原因**

目标盘符已被占用。

**解决方法**

请更换目标盘符重新挂载文件系统。

## 系统错误 1272 {#section_pwi_i6q_rqy .section}

**错误描述**

系统提示：“不能访问此共享文件夹，因为您组织的安全策略阻止未经身份验证的来宾访问。这些策略可帮助保护您的电脑免受网络上不安全设备或恶意设备的威胁。”

**主要原因**

Windows 系统因安全策略阻挡了以来宾访问权限（Guest Auth）访问SMB文件系统。

**解决方法**

若您的系统为 Windows Server 2016 之后版本（不包括 WindowsServer 2016），请修改以下注册表项允许来宾访问权限（Guest Auth）。

``` {#codeblock_ju0_36o_rzr}
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
"AllowInsecureGuestAuth"=dword:1
```

具体解决方案请参考[Guest access in SMB2 disabled by default in Windows](https://support.microsoft.com/en-us/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)。

