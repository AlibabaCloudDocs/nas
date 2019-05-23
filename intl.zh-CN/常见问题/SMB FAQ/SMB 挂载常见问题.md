# SMB 挂载常见问题 {#concept_dnz_nsy_bhb .concept}

## Windows 2016 以后的版本不支持挂载 NAS SMB {#section_fmv_wsy_bhb .section}

-   问题现象

    命令及错误提示：

    ```
    C:\Users\Administrator>net use z: \\xxxxx-xxxx.xxxxx.nas.aliyuncs.com\myshare
    System error 1272 has occurred.
    You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.
    ```

-   解决方案：

    造成以上问题的原因是 windows server 的这个版本的安全特性默认不支持guest 用户访问远程共享目录。

    解决方法如下：

    -   修改注册表：

        ```
        [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
        "AllowInsecureGuestAuth"=dword:0
        ```

        修改为：

        ```
        [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
        "AllowInsecureGuestAuth"=dword:1
        ```

    -   切换到 Powershell 键入以下命令：

        ```
        New-ItemProperty -Path $registryPath -Name $name -Value $value -PropertyType DWORD -Force
        ```

    具体解决方案请参见[Guest access in SMB2 disabled by default in Windows 10, Windows Server 2016 version 1709, and Windows Server 2019](https://support.microsoft.com/en-us/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)。


## Linux如何挂载SMB {#section_idm_frz_bhb .section}

NAS 目前并不支持 Linux 挂载 SMB。

如果要挂载，一般 linux 系统挂载命令如下：

```
mount -t cifs [MOUNT POINT] [LOCAL DIRECTORY] -o username=guest,vers=3.0
```

**说明：** Linux 版本不同挂载命令会有所区别。

较新的 Linux 系统使用`-o username=guest`选项需要输入密码，可以改用以下命令：

```
mount -t cifs [MOUNT POINT] [LOCAL DIRECTORY] -o guest,vers=3.0
```

## SMB 挂载有时候连接不上 {#section_zs4_mkz_bhb .section}

问题现象：

有时候用户会混用 NFS 和 SMB 文件系统，导致第一次通过 net use 挂载 NFS 文件系统连接失败后，挂载正确的 SMB 文件系统也会出现问题。

解决方案：

检查确保挂载正确的文件系统后，暂时停止挂载，5分钟后再次挂载。如果还失败，请发工单。

## Administrator 能看见挂载的 SMB 目录，其他用户看不到 {#section_xw4_zkz_bhb .section}

造成以上原因是由于 windows 下的用户账户隔离机制引起的。

要实现多用户的共享，需要创建一个目录链接。比如 C 盘下创建一个 myshare，命令如下：

```
mklink /D C:\myshare \\xxxxxxx-xxxx.cn-beijing.nas.aliyuncs.com\myshare\
```

## Windows Server 2016 的 IIS 无法加载 SMB volume 文件的问题 {#section_yw4_zkz_bhb .section}

如果遇到 Windows Server 2016 的 IIS 无法加载 SMB 文件卷文件的问题， 请参见云栖文章：[安装和配置 AD 域](https://yq.aliyun.com/articles/692463)。

## IIS 服务在阿里云 NAS 上的最佳实践 {#section_zw4_zkz_bhb .section}

如果遇到 Windows 2016 挂载 SMB 失败，HTTP错误500.19，错误码0x8007003a。请参见云栖文章：[IIS 服务在阿里云 NAS 上的最佳实践](https://yq.aliyun.com/articles/692462)。

## 是否支持 NFS 和SMB 同时挂载一个文件系统 {#section_k2w_b2z_bhb .section}

不能以 NFS 和 SMB 同时挂载同一个文件系统。

我们建议不要使用 Linux 作为客户端访问 SMB，因为存在一些操作上的问题。比如支持的字符集、文件名的长度（Windows 支持255宽字符，Linux 支持255 UTF8 字节）等等。

但用户如果确实需要的话，可以在支持 SMB2 及以上的 kernel 上挂载。

挂载命令：`mount -t cifs -o vers=2.0 \\挂载点\myshare /mnt`或者`mount -t cifs -o vers=2.0 //挂载点/myshare /mnt`。如果弹出需要密码，直接回车就可以。

确认 kernel 是否支持 CIFS 挂载：在/boot下，检查CONFIG\_CIFS的配置，y 或 m 表示支持。

如图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/137459/155857575640796_zh-CN.png)

**说明：** 

-   执行以上命令前需要安装 cifs-utils 。以 CentOS系统为例，安装命令如下：

    ```
    yum install samba-client samba-common cifs-utils
    ```

-   如果遇到一些 Linux 系统对 cifs 支持方面的问题，建议升级 kernel 到 3.10.0-514 及以上版本。

