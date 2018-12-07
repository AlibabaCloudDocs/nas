# Add a mount point {#concept_60431_zh .concept}

After creating a file system, you must add a mount point for the file system before you can mount the file system on computing nodes \(such as ECS instance, E-HPC, and Container Service\).

NAS supports two types of mount points: VPC and Classic Network.

## Add a mount point in a VPC {#section_ncq_3wx_gfb .section}

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Click **Add Mount Point** on the right of the file system to which you want to add a mount point.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/154417343121063_en-US.png)

3.  In the **Add Mount Point** dialog box, select **VPC** for **Mount Point Type**.
4.  Select the corresponding **VPC**, **VSwitch**, and **Permission Group**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/154417343121066_en-US.png)

    **Note:** You can select **VPC default permission group \(allow all\)** to allow all IP addresses in the same VPC to access the file system through the mount point.

5.  Click **OK**.

## Add a mount point in a classic network { .section}

1.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).
2.  Click **Add Mount Point** on the right of the file system to which you want to add a mount point .
3.  In the **Add Mount Point** dialog box, select **Classic network** for **Mount Point Type**, and select the permission group in the **Permission Group** drop-down box.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/154417343121073_en-US.png)

    **Note:** 

    -   Currently, only ECS instances can use mount points in classic networks.
    -   For a classic network mount point, no default permission group is provided. When using this for the first time, you must go to the Permission Group page to create a permission group in a classic network, and add rules for the permission group. For more information, see [Use permission groups](../../../../reseller.en-US/User Guide/Use permission groups.md#).
    -   When adding a mount point in a classic network for the first time, you are requested to authorize NAS through RAM to access the query interface of your ECS instance. Follow the instructions to complete the authorization, then try creating the mount point in the classic network again. For more information, see [Why do I need RAM permissions to create a mount point in a classic network](../../../../reseller.en-US/FAQ/Why do I need RAM permissions to create a mount point in a classic network.md#).
4.  Click **OK**.

After adding a VPC or classic network mount point for a file system, hover your mouse over the mount address of the file system to view the mount command.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18691/154417343121075_en-US.jpg)

