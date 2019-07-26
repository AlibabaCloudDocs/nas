# Manage file systems {#task_27530_zh .task}

This topic describes how to manage file systems in the Network Attached Storage \(NAS\) console. The management includes creating and deleting file systems. It also includes viewing a list of file systems and the details of each file system.

## Create file systems {#section_5jo_0kj_jn5 .section}

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Choose **NAS** \> **File System List** and click **Create File System**.
3.  In the Create File System dialog box, configure the required settings.

    ![create a file system](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18693/156410764552624_en-US.png)

    |Name|Description|
    |----|-----------|
    |Region| Select a region where you need to create a file system.

**Note:** 

    -   When a file system and an ECS instance are located in different regions, you cannot mount the file system on the ECS instance.
    -   The supported storage types and protocol types of a file system change based on the region. For more information, see [Storage types and protocol types supported by NAS in different regions](../reseller.en-US/FAQ/FAQs/Regions and supported storage types and protocols.md#).
    -   You can create a maximum of 20 file systems in a region by using an Alibaba Cloud account.
 |
    |Storage Type| Valid values: **SSD performance-type** and **Capacity-type**.

**Note:** The maximum capacity of a NAS Performance file system is 1 PB. The maximum capacity of a NAS Capacity file system is 10 PB. The billing method is pay-as-you-go.

 |
    |Protocol Type| Valid values: **NFS \(including NFSv3 and NFSv4\)** and **SMB \(2.1 and later\)**.

 NFS is used to share files stored on an ECS instance that runs Linux. SMB is used to share files stored on an ECS instance that runs Windows.

 |
    |Zone| Each region has many isolated locations known as zones. The power supply and network of each zone are independent.

 Select a zone from the drop-down list. We recommend that you select the same zone where the target ECS instance is located.

**Note:** When a file system and an ECS instance are located in different zones in the same region, you can mount the file system on the ECS instance.

 |
    |Storage Package| Storage packages are an alternative billing method. It provides extra discount based on the pay-as-you-go billing method. If you do not purchase a storage package, the default billing method is pay-as-you-go. For more information, see [Pricing](../reseller.en-US/Pricing/Billing method.md#).

 |

4.  Click **OK** to create the new file system.

## View the list of file systems {#section_hy3_chm_hfb .section}

On the **File System List** page, you can view the list of all file systems in a region. On the **File System List** page, locate the target file system and click Edit to modify the name of the file system.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18693/156410764531413_en-US.png)

## View the details of a file system {#section_fp5_zhm_hfb .section}

Locate the target file system, and click the file system ID or **Manage** to open the **File System Details** page. You can view basic information, storage packages, and mount points of the file system.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18693/156410764632295_en-US.png)

## Delete a file system {#section_qy1_m3m_hfb .section}

Locate the target file system, click **Delete** to delete the file system.

**Note:** 

-   Before deleting a file system, you must remove all mount points of the file system.
-   Use caution while deleting a file system. After a file system is deleted, the data on the file system cannot be restored.

