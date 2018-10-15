# Mount NAS on Windows {#concept_67165_zh .concept}

NAS is a storage service that offers you a distributed file system and shared storage across multiple ECS instances. This topic describes the process of mounting an NAS file system on Windows Server 2012 R2.

## Prerequisites {#section_jmj_yl3_hfb .section}

Before you can mount a NAS file system to a Windows instance, you must complete the following actions:

-   Follow [Step 2. Create an instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) to create a Windows ECS instance. In this example:

    -   The **region** is EU Central 1 \(Frankfurt\).
    -   The **image** is Windows 2012 R2 Data Centre Edition.
    -   The **network type** must be VPC.
-   Create a file system and add a mount point.

    1.  Activate the NAS service.

    2.  Log on to the [NAS console](partners-intl.console.aliyun.com/#/nas).

    3.  Buy a storage package. Follow these steps:

        1.  In the left-side navigation pane, click **Storage Package**.

        2.  Click **Buy Storage Package**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213170_en-US.png)

        3.  On the **NAS Storage Package** page, select the **Region** \(EU Central 1 is selected in this example\), **Capacity**, and the duration of the package.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213171_en-US.png)

    4.  Create a file system. Follow these steps:

        1.  In the NAS console, from the left-side navigation pane, click **File System List**.
        2.  Select the **EU Central 1 \(Frankfurt\)** region.
        3.  Click **Create File System**.
        4.  Specify the specifications of the file system and bind the storage package to it.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213172_en-US.png)

        5.  Click **OK**.
    5.  Add a mount point.

        In this example, select **VPC** as the mount point type.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213173_en-US.png)

    6.  In the file system list, click the file system ID, and view the **Mount Address** of the new mount point. You will use the mount address to mount the file system on the Windows instance. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213174_en-US.png) 

## Procedure { .section}

You can now mount the mount point on a server with Windows 2012 R2 Data Centre Edition. This solution works for most versions of Windows with NFS Client installed.

1.  [Connect to a Windows instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).

2.  Install the NFS Client on the instance.

    1.  Click the **Server Manager** icon.

    2.  From the upper menu, select **Manage** \> **Add Roles and Features**.

    3.  Follow the **Add Roles and Features Wizard** to finish the installation.

        -   Under the **Server Roles** tab, select **Server For NFS**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895213175_en-US.png)

        -   Under the **Features** tab, select **Client for NFS**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895313176_en-US.png)

    4.  Restart the server within the guest operating system.

    5.  Start **Command Prompt** and run `mount`. If the following result is returned, the Client for NFS has been installed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895313177_en-US.png)

3.  Run the following command to mount the NFS mount point as a drive.

    ```
    mount -o nolock \\11xxxxxxxx9-wxx88.eu-central-1.nas.aliyuncs.com\! h:
    
    ```

    Where `11xxxxxxxx9-wxx88.eu-central-1.nas.aliyuncs.com` is the mount address that we have created.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895313178_en-US.png)

4.  Check the shared drive from the **This PC** of the instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895313179_en-US.png)

5.  Test creation of a folder and a text file inside the newly created folder.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895313180_en-US.png)


## Troubleshooting { .section}

If you get a `file handle error`, check the Registry entries in **HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**. The value of Locking must be 1.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895413752_en-US.png)

You can also set GID and UID by creating the Registry entries:

1.  Go to **HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **Default**.

2.  Right-click a blank area, and then select **New** \> **DWORD\(32bit\)** to add the following Registry entries.

    -   AnonymousGID: Set the value to 0.
    -   AnonymousUID: Set the value to 0.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895413753_en-US.png)

3.  Start **Command Prompt** and run `mount` to check the UID and GID.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153960895413754_en-US.png)


