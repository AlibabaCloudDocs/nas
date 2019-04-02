# 如何提升IIS访问NAS性能 {#concept_65228_zh .concept}

## 问题现象 {#section_mjy_qfh_hfb .section}

对于 IIS 使用 NAS share 的方式，访问一个文件时，IIS 后台会有很多次访问 NAS 操作。不同于访问本地文件系统，访问 NAS 每次至少要有一次网络交互，因此虽然每次访问的时间不长，但是多次的叠加可能会造成客户端总时间比较长。

## 解决方案 { .section}

改进方式请参见[SMB2 Client Redirector Caches Explained](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200(v=ws.10)) 。

您可以将文章中提到的三个注册表项都调大，例如调为600或以上。

注册表项所在路径为HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\LanmanWorkstation\\Parameters。

注册表名称分别为：

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

**说明：** 

-   三个注册表项都不存在：
    1.  先确认使用的是 SMB 而不是 NFS。
    2.  然后确认客户使用的 windows 版本支持这三个注册表项。如果 windows 版本支持而注册表项不存在，手动创建一下。详情请参见[Performance tuning for file servers](https://docs.microsoft.com/en-us/windows-server/administration/performance-tuning/role/file-server/)
-   建议把 IIS 频繁访问的 js/css 等网页程序相关的内容放在本地。

