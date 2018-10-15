# Back up data from ECS to NAS by using Windows Server Backup {#concept_63080_zh .concept}

This topic describes how to back up important data from a folder or the full disk on a Windows ECS instance to Alibaba Cloud NAS in a common method — the Windows Server Backup feature.

Windows Server Backup supports one-time manual data backup and scheduled backup. When necessary, you can conveniently restore data from the backup file.

## Background {#section_i4c_333_hfb .section}

Alibaba Cloud NAS helps you design a separated compute and storage architecture that backs up persistent data to NAS while retaining computing tasks and memory states on your ECS instance. This way, even if your ECS instance goes down, your business can be quickly fail over to a new ECS instance, which seamlessly and continuously accesses the data stored on NAS. NAS is the best choice for separation of compute and storage with the support for data sharing among multiple ECS instances.

In addition to data sharing, you can choose to regularly or occasionally synchronize data from your ECS instance to storage media besides cloud disks. This allows you not only to back up data, but also to recover data in the case of disasters like accidental deletion of the ECS instance and cloud disks. NAS allows you to back up important data as needed. Compared to cloud disk snapshots, which backs up data for the full disk, NAS provides more backup options. For example, you can choose to back up only certain directories rather than the full cloud disk.

## Windows Server Backup { .section}

Windows Server Backup is a native feature of Windows that backs up and restores data for a full disk, folders, or files. According to [Microsoft - Overview of Windows Server Backup](https://technet.microsoft.com/zh-cn/library/cc732091), Windows Server Backup is a feature for your day-to-day backup and recovery needs.

You can use Windows Server Backup to back up a full server \(all volumes\), selected volumes, system state, or specific files or folders to another device \(including other hard disks, tape libraries, or remote shared folders\) and to recover the data from the storage media when necessary.

## Install Windows Server Backup { .section}

Follow these steps to install Windows Server Backup in an Alibaba Cloud Windows image:

1.  Click **Start** \> **Administrative Tools** \> **Server Manager**.
2.  In Server Manager, click **Features**, and then click **Add Features**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413151_en-US.png)
3.  Select **Windows Server Backup Features**, and then click **Next**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413152_en-US.png)
4.  Click **Install**.

After the installation is completed, you can click **Start** \> **Administrative Tools** \> **Windows Server Backup** to start the feature.

## Use Windows Server Backup to back up data { .section}

Before using Windows Server Backup to back up data to NAS, you must create an SMB file system instance and mount it to your ECS instance.

Windows Server Backup supports **Backup Once** and the creation of **Backup Schedule** for scheduled backups.

## Backup Once { .section}

With **Backup Once**, you can manually back up data \(on a full disk or in selected folders\) to NAS as needed.

1.  Start **Windows Server Backup**, and click **Backup Once**.

    The **Backup Once Wizard** window is displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413153_en-US.png)

2.  Click **Next**.
3.  On the **Select Backup Configuration** page, select **Full Server** or **Custom** \(volumes or files\).

    If you select **Custom**, you must click **Advanced Settings** to set backup types and excluded files in the folders.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413154_en-US.png)

4.  On the **Specify Destination Type** page, select **Remote shared folder**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413155_en-US.png)

5.  On the **Specify Remote Folder** page, specify a location under the NAS SMB mount point, such as the **backup** folder.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413156_en-US.png)

6.  On the **Confirmation** page, click **Backup** to start backup and wait for the backup process to be completed.


After backup is completed, you can go to the NAS **backup** folder and view the backed up content.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413157_en-US.png)

## Backup Schedule { .section}

On the **Backup Schedule** page, you can configure automatic and regular **Backup Once**. This process is similar to that of **Backup Once**, expect that you must specify the backup time.\(ui\)

**Note:** In the following procedure, steps that are the same as those in the **Backup Once** procedure are not described in details. Details for these steps can be found in the Backup Once section.

1.  Start **Windows Server Backup**, and click **Backup Schedule**.

    The **Backup Schedule Wizard** window is displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413158_en-US.png)

2.  On the **Specify Backup Time** page, set the backup frequency and running time.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413159_en-US.png)

3.  On the **Specify Destination Type** page, select **Back up to a shared network folder**.

    **Note:** When you use a remote shared folder as the storage destination for a backup schedule, each backup overwrites the preceding one, so only the latest backup is retained.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413160_en-US.png)

4.  Start the backup schedule. A backup task automatically runs within the time you specified.

## Use Windows Server Backup to recover data { .section}

If your data is deleted or a file is overwritten, you can recover files previously backed up to NAS.

1.  Start **Windows Server Backup**, and click **Recover**.
2.  On the **Getting Started** page, select **A backup stored on another location**, and type the path of the backup folder configured previously.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413161_en-US.png)

3.  On the **Specify Items to Recover** page, select one or more files or folders to recover.
4.  On the **Specify Recovery Options** page, type the location on your local device to save the recovered data.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153960892413162_en-US.png)
5.  On the **Confirmation** page, click **Recover** to start data recovery and wait for the process to be completed.

