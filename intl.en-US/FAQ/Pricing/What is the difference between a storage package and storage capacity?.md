# What is the difference between a storage package and storage capacity? {#concept_1375303 .task}

This topic describes the concepts of a storage package and storage capacity. It also provides details about the procedure to view the storage capacity of a file system.

## Storage packages {#section_6oe_m4x_nxf .section}

The billing method for a storage package is subscription.

Assume that you create a NAS Capacity file system and link a storage package with a size of 500 GB to the file system. During a period from 7:00 to 8:00 on June 1, 2019, the maximum used capacity of the file system is 550 GB. When you are charged, 500 GB of the total 550 GB is covered by the storage package, while the remaining 50 GB is charged by using the pay-as-you-go billing method.

**Note:** 

The maximum storage capacity has no relation to the size of a storage package.

If you require more storage capacity as your business expands, you can upgrade the existing storage package to a higher specification. For more information, see [Upgrade a storage package](../../../../reseller.en-US/Pricing/Subscription/Upgrade a storage package.md#).

## Storage capacity {#section_qmr_rp1_4lp .section}

Storage capacity indicates the available size for a file system that you can use to store data.

-   Maximum capacity of NAS Extreme is 1 PB.
-   Maximum capacity of NAS Capacity is 10 PB.

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Choose **NAS** \> **File System List**.
3.  Find the target file system, and click **Manage** to view the capacity of the file system on the File System Details page.

    **Note:** 

    On the File System Details page, the value of the File System Usage field indicates the maximum amount of used space for a file system over the last hour.

    In Linux, you can run the `df -h` command to view the remaining capacity of a file system.

    If the used space for a file system is zero, it indicates that no data is stored in the file system.

    ![Used space of a file system](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1095538/156698684354043_en-US.png)


