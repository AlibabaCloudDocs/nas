# Purchase a storage package {#concept_27524_zh .task}

Network Attached Storage \(NAS\) supports the subscription billing method. You can either create a file system and then attach a storage package or create a file system while you purchase a storage package.

## Purchase a storage package {#section_5al_h93_03c .section}

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Choose **NAS** \> **File System List** and click **Buy Storage Package**.
3.  Complete the required configurations and click **Buy Now**. 

    After the payment is complete, click the target file system ID or name on the File System List page and the **File System Details** page is displayed.

    **Note:** You must attach a storage package to a file system. A file system can only have one storage package attached. You can select the ID of an existing file system or click **Create new FS and bind package** to create a new file system.


## FAQ {#section_5xx_fqq_u9o .section}

-   When will a storage package take effect?

    A storage package takes immediate effect after it is purchased.

-   Can I refund a storage package?

    You can only refund a storage package that has never been consumed. For more information about refunds, submit a ticket to Alibaba Cloud Customer Services.

-   What will happen after a storage package expires?

    If you fail to renew a storage package after the storage package expires, you are charged for the used space by using the pay-as-you-go billing method.

-   What will happen if the used space of a file system exceeds the maximum capacity of a storage package?

    You are only charged for the space that exceeds the maximum capacity of the storage package. The excess space is charged by using the pay-as-you-go billing method.

    For example, you purchase a storage package of 100 GB. However, the actual used space exceeds the specified maximum capacity. The space that exceeds 100 GB is charged by using the pay-as-you-go billing method.

-   Can I purchase multiple storage packages for a file system?

    No. You can only attach one storage package to a file system. If you want a storage package with a higher specification or longer duration, you can [upgrade a storage package](upgrade a storage packageEN-US_TP_18688.dita#concept_53974_zh).

-   Is the storage capacity of a file system limited by the capacity of a storage package?

    No. The storage capacity of a file system is not affected by the capacity of a storage package. You are charged for the space that exceeds the maximum capacity of a storage package by using the pay-as-you-go billing method.

    For example, you create an NAS Performance file system with a maximum capacity of 10 PB and attach a storage package of 5 GB. The maximum capacity of the file system is still 10 PB.

-   How can I detach a storage package?

    After a storage package is attached to a file system, you must delete the file system before detaching the package.

-   How can I attach a storage package to another file system when it has already been attached to a file system?

    After a storage package is attached to a file system, you must delete the file system that has your storage package attached before detaching the package to another file system.


