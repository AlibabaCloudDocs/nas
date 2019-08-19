# Mount a file system on an ECS instance running Linux {#concept_27526_zh .task}

This topic describes how to create a file system and mount the file system on an ECS instance running Linux.

1.  You have registered an Alibaba Cloud account and completed real-name authentication.

    If you do not have an Alibaba Cloud account, you need to create an account. For more information, see [Create an Alibaba Cloud account](https://www.alibabacloud.com/help/zh/doc-detail/50482.html).

2.  You have activated the Network Attached Storage \(NAS\) service.

    When you log on to the [NAS console](https://nas.console.aliyun.com/) for the first time, follow the instructions to activate the NAS service.

3.  At least one ECS instance is available in the region where you need to create a file system.

    If no ECS instance is available, you need to purchase an ECS instance. For more information, see [Step 2. Create an instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

    **Note:** 

    1.  For more information about how to manage NAS by using a RAM user account, see [Access control for RAM users](../../../../intl.en-US/Console User Guide/Manage permissions/Access control for RAM users.md#).
    2.  After you activate the NAS service, the default billing method is pay-as-you-go. If you want to use NAS with an extra discount, you can purchase a storage package. For more information, see [Purchase a storage package](../../../../intl.en-US/Pricing/Subscription/Purchase a storage package.md#).
    3.  If you need to create a mount point in a VPC, you need to create a VPC in the same region where the new file system resides. Then, you need to attach the ECS instance that hosts the file system to the VPC. For more information, see [Create a VPC and VSwitch](Create a VPC and VSwitch../../SP_22/DNVPC11885991/EN-US_TP_2434.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb).

## Step 1: Create a file system {#section_3x4_3v9_srh .section}

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**, and click **Create File System**.
3.  In the Create File System dialog box, configure the required settings. 

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
    |Protocol Type| Select **NFS \(including NFSv3 and NFSv4\)**.

 NFS is used to share files stored on an ECS instance that runs Linux. SMB is used to share files stored on an ECS instance that runs Windows.

 |
    |Zone| Each region has many isolated locations known as zones. The power supply and network of each zone are independent.

 Select a zone from the drop-down list. We recommend that you select the same zone where the target ECS instance resides.

**Note:** When a file system and an ECS instance are located in different zones in the same region, you can mount the file system on the ECS instance.

 |
    |Storage Package| Storage packages are an alternative billing method. It provides an extra discount over the pay-as-you-go billing method. If you do not purchase a storage package, the default billing method is pay-as-you-go. For more information, see [Pricing](../../../../intl.en-US/Pricing/Pricing.md#).

 |

4.  Click **OK** to create the new file system.

## Step 2: Create a mount point {#section_9q8_owp_z6n .section}

In NAS, you need to use a mount point to mount a file system on an ECS instance. NAS supports two types of mount points: VPC and classic network. You can create each type of mount point by performing a respective set of steps.

**Note:** You can create a maximum of two mount points for each file system.

1.  Log on to the [NAS console](https://nas.console.aliyun.com/).
2.  Choose **NAS** \> **File System List**.
3.  Find the target file system, and click **Add Mount Point**.
4.  In the **Add Mount Point** dialog box, configure the required settings. 

    **Mount Point Type**: includes VPC and Classic network.

    -   If you need to create a mount point with the VPC type, configure the settings as described in the following table.

        |Name|Descriptions|
        |----|------------|
        |VPC| Select a VPC. If no VPC is available, create a VPC in the [Virtual Private Cloud console](https://vpc.console.aliyun.com/).

**Note:** The VPC and VSwitch you select must be the same as those of the ECS instance on which you mount a file system.

 |
        |VSwitch| Select a VSwitch that is created in the VPC.

 |
        |Permission Group| Select **VPC default permission group \(allow all\)** or an existing permission group.

**Note:** This VPC default permission group is generated for each Alibaba Cloud account, which allows access to the file system through the mount point from all IP addresses of the VPC. For more information about how to create a permission group, see [Manage permission groups](../../../../intl.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).

 |

    -   If you need to create a mount point in a classic network, configure the settings as described in the following table.

        |Name|Descriptions|
        |----|------------|
        |Permission group| Select a permission group. If no available permission group exists, create a permission group in the [NAS console](https://nas.console.aliyun.com/#/accessGroup/list).

**Note:** 

        -   You can only create a mount point with the classic network type in a region that is located in Mainland China.
        -   You can only attach a mount point with the classic network type to an ECS instance.
        -   For data security, NAS dos not provide a permission group for a mount point with the classic network type. Therefore, you need to create a permission group of the classic network type before specifying the permission group for a mount point of the classic network type. Then, you need to add the required rules to the permission group. For more information about how to manage permission groups, see [Manage permission groups](../../../../intl.en-US/Console User Guide/Manage permissions/Manage permission groups.md#).
        -   When creating a mount point in a classic network for the first time, you are required to use RAM to authorize NAS to access ECS instances hosted by the logon Alibaba Cloud account. We recommend that you follow the instructions to complete the authorization and create a mount point in a classic network. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../../../../intl.en-US/FAQ/FAQs/Why do I need RAM permissions to create a mount point in a classic network.md#).
 |

5.  Click **OK** create a mount point.

## Step 3: Install an NFS client {#section_0q3_q5c_9sh .section}

Before mounting an NFS file system on an ECS instance running Linux, you must install an NFS client.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Use the following command to install the NFS client. 
    -   If CentOS, RHEL, or Aliyun Linux is running on the ECS instance, run the following command.

        ``` {#codeblock_dk2_0xl_805}
        sudo yum install nfs-utils
        ```

    -   If Ubuntu or Debian is running on the ECS instance, run the following commands.

        ``` {#codeblock_l6c_fnw_myw}
        sudo apt-get update
        ```

        ``` {#codeblock_bp8_tbd_bgl}
        sudo apt-get install nfs-common
        ```

3.  Change the maximum number of concurrent NFS requests. For more information, see [How can I modify the maximum number of concurrent NFS requests?](../../../../intl.en-US/FAQ/FAQs/How can I modify the maximum number of concurrent NFS requests?.md#). 

    The maximum number of concurrent requests from an NFS client is limited to 2 by default, which reduces NFS performance.


## Step 4: Mount a file system {#section_789_6w7_3jg .section}

You can use the domain name of a file system or the domain name of the mount target to mount the NFS file system on an ECS instance. The domain name of the file system is resolved to the IP address of the mount target in a zone where the ECS instance resides.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Mount the NFS file system. 

    -   Use the following command to mount an NFSv4 file system.

        ``` {#codeblock_ff5_sft_tfr}
        sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        								
        ```

        If you fail to mount the file system, run the following command.

        ``` {#codeblock_0s7_syr_553}
        sudo mount -t nfs4 -o rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        								
        ```

    -   If you need to mount an NFSv3-compliant system, run the following command.

        ``` {#codeblock_974_tkj_vn4}
        sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
        ```

    The following table lists the parameters used in the mount command and the description of each parameter.

    |Name|Description|
    |:---|:----------|
    |Mount point| Includes the domain name of a mount point and the mount directory. We recommend that you replace the value of this parameter with a value specific to your business requirements.

    -   The domain name of a mount point is generated when you create the mount point. You do not need to manually configure the name of a mount point.
    -   The path of a mount point indicates the target mount address. The path can be the root directory \(/\) or a subfolder such as /mnt in Linux.
 |
    |vers|The version of the file system. Only NFSv3 and NFSv4 are applicable.|
    |Mount options| When you mount a file system, multiple mount options are available. For more information, see the [Mount options](intl.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#table_2uc_odz_vk9) topic in [Mount an NFS file system](../../../../dita-oss-bucket/SP_111/DNnas1882233/intl.en-US/Console User Guide/Mount a file system/Mount an NFS file system.md#).

 |

3.  Use the `mount -l` command to view mount results. 

    The following figure shows an example of a successful mount.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156618374551149_en-US.png)

    After a file system is mounted, you can use the `df -h` command to view the capacity of the file system.

4.  After mounting a NAS file system, you can read and write data to the file system on an ECS instance. 

    You can access the file system by using the same method for a common directory. An example is shown as follows.

    ![read and write data to the file system](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156618374554347_en-US.png)


