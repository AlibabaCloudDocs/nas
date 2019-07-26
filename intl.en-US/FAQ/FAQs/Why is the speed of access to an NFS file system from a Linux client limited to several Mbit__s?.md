# Why is the speed of access to an NFS file system from a Linux client limited to several Mbit/s? {#concept_53839_zh .concept}

This topic describes why the speed of access to an NFS file system from an NFS client that runs Linux is limited to several Mbit/s and how you remove the limit.

The maximum number of concurrent NFS requests from an NFS client running Linux is limited to 2 by default, which reduces NFS performance.

After an NFS client is installed, you can modify the maximum number of concurrent NFS requests to improve NFS performance. For more information, see [How can I modify the maximum number of concurrent NFS requests?](reseller.en-US/FAQ/FAQs/How can I modify the maximum number of concurrent NFS requests?.md#).

