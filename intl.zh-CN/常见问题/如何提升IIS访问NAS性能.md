# 如何提升IIS访问NAS性能 {#concept_65228_zh .concept}

## 问题现象 {#section_mjy_qfh_hfb .section}

对于IIS使用NAS share的方式，访问一个文件时，IIS后台会有很多次访问NAS操作。不同于访问本地文件系统，访问NAS每次至少要有一次网络交互，因此虽然每次访问的时间不长，但是多次的叠加可能会造成客户端总时间比较长。

## 解决方案 { .section}

改进的方式请参见以下链接：[https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200\(v=ws.10\)?spm=a2c4g.11186623.2.12.3f0e4f0bYtWYjJ&file=ff686200\(v=ws.10\)](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200(v=ws.10)?spm=a2c4g.11186623.2.12.3f0e4f0bYtWYjJ&file=ff686200(v=ws.10)) 。

您可以将文章中提到的三个注册表项都调大，例如调为600或以上。

需要注意的是这些注册表项都在注册表HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\LanmanWorkstation\\Parameters之下，名称分别为：

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

另外，建议把js/css等网页程序相关的内容放在本地，因为IIS会非常频繁访问。

