# Mount a file system on an ECS instance running Windows {#task_944060 .task}

This topic describes how to create a file system and mount the file system on an ECS instance that runs Windows.

1.  You have registered an Alibaba Cloud account and completed real-name authentication.

    If you do not have an Alibaba Cloud account, you need to create an account. For more information, see [Create an Alibaba Cloud account](https://www.alibabacloud.com/help/zh/doc-detail/50482.html).

2.  Activate the NAS service.

    When you log on to the [NAS console](https://nas.console.aliyun.com/) for the first time, follow the instructions to active the NAS service.

3.  An ECS instance must be available in the same region where you need to create a file system.

    If no available ECS instance exists, we recommend that you purchase an ECS instance. For more information, see [Step 2. Create an instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

4.  Ensure that the Workstation and TCP/IP NetBIOS Helper services are started on the Windows system. For more information, see [../../../../dita-oss-bucket/SP\_111/DNnas1882233/EN-US\_TP\_21209.md\#](../../../../intl.en-US/Console User Guide/Mount a file system/Mount an SMB file system.md#).

    **Note:** 

    1.  For more information about how to manage NAS by using a RAM user account, see [Access control for RAM users](../../../../intl.en-US/Console User Guide/Manage permissions/Access control for RAM users.md#).
    2.  After you activate the NAS service, the default billing method is pay-as-you-go. If you want to use NAS with extra discount, you can purchase a storage package. For more information, see [Purchase](../../../../intl.en-US/Pricing/Storage package/Purchase.md#).
    3.  If you need to create a mount point in a VPC, you need to create a VPC in the same region where the new file system is located. Then, you need to attach the ECS instance that hosts the file system to the VPC. For more information, see [Create a VPC and VSwitch](Create a VPC and VSwitch../../SP_22/DNVPC11885991/EN-US_TP_2434.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb).

## Step 1: Create a file system {#section_ycr_jeb_8o0 .section}

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**, and click **Create File System**.
3.  In the Create File System dialog box, configure the required settings as described in the following table.

    |Name|Description|
    |----|-----------|
    |Region| Select a region where you need to create a file system.

**Note:** 

    -   When a file system and an ECS instance are located in different regions, you cannot mount the file system on the ECS instance.
    -   The supported storage types and protocol types of a file system change based on the region. For more information, see [Storage types and protocol types supported by NAS in different regions](../../../../intl.en-US/FAQ/FAQs/Regions and supported storage types and protocols.md#).
    -   You can create a maximum of 20 file systems in a region by using an Alibaba Cloud account.
 |
    |Storage Type| Valid values: **SSD performance-type** and **Capacity-type**.

**Note:** The maximum capacity of a NAS Performance file system is 1 PB. The maximum capacity of a NAS Capacity file system is 10 PB. The billing method is pay-as-you-go.

 |
    |Protocol|Select **SMB \(2.1 and later\)**. NFS is used to share files stored on an ECS instance that runs Linux. SMB is used to share files stored on an ECS instance that runs Windows.

 |
    |Zone| Each region has many isolated locations known as zones. The power supply and network of each zone are independent.

 Select a zone from the drop-down list. We recommend that you select the same zone where the target ECS instance is located.

**Note:** When a file system and an ECS instance are located in different zones in the same region, you can mount the file system on the ECS instance.

 |
    |Storage Package| Storage packages are an alternative billing method. It provides extra discount based on the pay-as-you-go billing method. If you do not purchase a storage package, the default billing method is pay-as-you-go. For more information, see [Pricing](../../../../intl.en-US/Pricing/Billing method.md#).

 |

4.  After the configuration is complete, click **OK**.

## Step 2: Create a mount point {#section_kkl_dpm_swq .section}

In NAS, you need to use a mount point to mount a file system on an ECS instance. NAS supports two types of mount points: VPC and classic network. You can create each type of mount point by performing a respective set of steps.

**Note:** You can create a maximum of two mount points for each file system.

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**.
3.  Locate the target file system, click **Add Mount Point**.
4.  In the **Add Mount Point** dialog box, configure the required settings.

    **Mount Point Type**: includes VPC and Classic network.

    -   If you need to create a mount point with the VPC type, configure the settings as described in the following table.

        |Name|Description|
        |----|-----------|
        |VPC| Select a VPC. If no VPC is available, create a VPC in the [Virtual Private Cloud console](https://vpc.console.aliyun.com/).

**Note:** The VPC and VSwitch you select must be the same as those of the ECS instance on which you mount a file system.

 |
        |VSwitch| Select a VSwitch that is created in the VPC.

 |
        |Permission Group| Select **VPC default permission group \(allow all\)** or an existing permission group.

**Note:** This VPC default permission group is generated for each Alibaba Cloud account, which allows access to the file system through the mount point from all IP addresses of the VPC. For more information about how to create a permission group, see [Manage permission groups](../../../../intl.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).

 |

    -   If you need to create a mount point in a classic network, configure the settings as described in the following table.

        |Name|Description|
        |----|-----------|
        |Permission group| Select a permission group. If no available permission group exists, create a permission group in the [NAS console](https://nas.console.aliyun.com/#/accessGroup/list).

**Note:** 

        -   You can only create a mount point with the classic network type in a region that is located in China.
        -   You can only attach a mount point with the classic network type to an ECS instance.
        -   For data security, NAS dos not provide a permission group for a mount point with the classic network type. Therefore, you need to create a permission group with the network type set as classic network before specifying the permission group for a mount point with the classic network type. Then, you need to add the required rules to the permission group. For more information about how to manage permission groups, see [Manage permission groups](../../../../intl.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).
        -   When creating a mount point in a classic network for the first time, you are required to use RAM to authorize NAS to access ECS instances hosted by the logon Alibaba Cloud account. We recommend that you follow the instructions to complete the authorization and create a mount point in a classic network. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../../../../intl.en-US/FAQ/FAQs/Why do I need RAM permissions to create a mount point in a classic network.md#).
 |

5.  Click **OK** to create the new mount point.

## Step 3: Mount a file system {#section_c6i_oxv_mra .section}

Perform the following steps to mount an SMB file system on an ECS instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Open the command prompt and run the following command to mount the file system.

    ``` {#codeblock_7b8_l26_nq2}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare
    ```

    The format of the command used to mount the file system is `net use <the drive of the mount target> \\<the domain name of a mount point>\myshare`.

    -   The drive of the mount target: the target drive on which you need to mount a file system.
    -   The domain name of a mount point: the domain name generated when you create the mount point for a file system. For more information, see [Manage mount points](../../../../intl.en-US/Console User Guide/Manage mount points.md#).
    -   myshare: indicates the name of an SMB share. You cannot change the name.
    **Note:** 

    Ensure that the name of the target mount drive is unique on the target ECS instance.

    For more information about how to troubleshoot the errors that occur while the the mount command is running, see [Causes and solutions of SMB mount failures](../../../../intl.en-US/FAQ/SMB FAQ/Causes and solutions of SMB mount failures.md#).

3.  Use the `net use` command to check mount results.

    An example of a successful mount is shown in the following figure.

    ![mount results](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/156410937653100_en-US.png)


