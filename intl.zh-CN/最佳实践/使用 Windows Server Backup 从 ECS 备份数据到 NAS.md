# 使用 Windows Server Backup 从 ECS 备份数据到 NAS {#concept_63080_zh .concept}

## 背景 {#section_i4c_333_hfb .section}

本文介绍了一种从 Windows ECS 备份数据到 NAS 的常用方法，即使用 Windows 服务器系统自带的 Windows Server Backup 工具，将云盘上指定文件夹或者整盘的重要数据备份到阿里云 NAS。

Windows Server Backup 支持手动一次性备份数据，和制定备份计划周期性备份数据；在需要时，您可以方便地从备份中恢复数据。

阿里云 NAS 帮助您实现计算和存储分离的架构设计：您可以将计算任务以及内存态数据保留在 ECS 上， 而将需要持久化的数据保存到 NAS 上。这样，即使在 ECS 宕机时，您的业务也可以快速切换到其他 ECS 上，并且使用新的 ECS 无缝、持续地访问保存在 NAS 上的数据。NAS 是多 ECS 共享数据，以及实现计算存储分离的最佳工具。

除了数据共享外，您也可以选择把 ECS 上的数据定期或者不定期地同步到云盘之外的存储；这样不仅可以保留历史数据，而且当发生灾难性事件（比如误删除 ECS 及云盘）时，也可以用作数据恢复。NAS 能够帮助您灵活地保存重要数据：相比于云盘快照基于整盘来保存历史数据，备份历史数据到 NAS 提供更灵活的选择，比如您可以选择备份某一个或者几个目录，而不是整块云盘。

## Windows Server Backup { .section}

Windows Server Backup 是一个 Windows 原生的数据（整盘、文件夹或者文件）备份和恢复的工具。根据微软官网的介绍（[Windows Server Backup 概述](https://technet.microsoft.com/zh-cn/library/cc732091)），Windows Server Backup 是一个日常备份和恢复工具。 通过 Windows Server Backup 可以备份整个服务器（所有卷）、选定卷、系统状态或者特定的文件或文件夹，到其他设备（包括其他硬盘、磁带库或者远程共享文件夹），并且可以在需要的时候从其他硬盘、磁带库或者远程共享文件夹进行数据的恢复。

## 安装 Windows Server Backup { .section}

参照以下步骤，在阿里云的 Windows 镜像中安装运行 Windows Server Backup。

1.  打开**服务器管理器** \> **功能**，单击**添加功能**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713151_zh-CN.png)

2.  勾选**Windows Server Backup 功能**，并单击**安装**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713152_zh-CN.png)


安装完成之后，你可以在**管理工具**中单击**Windows Server Backup** 来启动它。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713153_zh-CN.png)

## 使用 Windows Server Backup 备份数据 { .section}

Windows Server Backup 支持**一次性备份**和创建**备份计划**进行周期性持续备份，以下分别对其进行介绍。

## 一次性备份 { .section}

使用一次性备份，您可以按需手动地将数据（整盘或者目录）备份到 NAS。

1.  打开Windows Server Backup，在其右侧操作栏单击**一次性备份** 启动**一次性备份向导**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713154_zh-CN.png)

2.  在**选择备份配置**中按需选择要备份的对象：**整个服务器**或**自定义**（卷或文件）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713155_zh-CN.png)

    -   当选择**自定义**时，需要进一步**选择要备份的项**，单击**添加项**来完成。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713156_zh-CN.png)

    -   在**选择要备份的项**中，打开**高级设置**，可以设置备份类型，以及备份中跳过目录中特定的文件等。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713157_zh-CN.png)

3.  在**指定目标类型**中选择存储位置，勾选**远程共享文件夹**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713158_zh-CN.png)

4.  在**指定远程文件夹**中，指定 NAS SMB 挂载点下的一个位置，比如 “backup” 目录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713159_zh-CN.png)

5.  启动备份，等待备份完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360713160_zh-CN.png)


备份完成后，您可以在 NAS 上 “backup” 目录下，查看已备份的内容。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813161_zh-CN.png)

## 备份计划 { .section}

 **备份计划**中可以配置定期自动进行一次性备份。其操作流程与 一次性备份类似，主要区别是需要制定备份的时间。

**说明：** 下述操作步骤中，与一次性备份类似的步骤不作赘述。

1.  打开**Windows Server Backup**，在其右侧操作栏单击**备份计划** 启动**备份计划向导**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813162_zh-CN.png)

2.  在**指定备份时间**中设置备份的频率和运行时间。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813163_zh-CN.png)

3.  在 **指定目标类型** 中，勾选 **备份到共享网络文件夹**。

    **说明：** 当将远程共享文件夹用作计划备份的存储目标时，各备份会擦除前面的备份，只保留最新的备份。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813164_zh-CN.png)

4.  启动备份计划，备份任务会在您指定的时间内自动运行。


## 使用 Windows Server Backup 恢复数据 { .section}

在发生误删除，或者文件被覆盖等情况，您可以从之前备份到 NAS 的数据中恢复文件。

1.  打开 **Windows Server Backup**，在其右侧操作栏单击 **恢复** 启动 **恢复向导**。

2.  在 **入门** 中，指定备份数据的来源。勾选 **在其他位置存储备份**，并配置之前用作备份的目录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813165_zh-CN.png)

3.  在 **选择要恢复的项目** 中，选择备份中的一个或者某几个文件或者子文件夹进行恢复。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813166_zh-CN.png)

4.  在 **指定恢复选项**中，指定恢复数据保存到本地的位置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18708/153814360813167_zh-CN.png)

5.  启动数据恢复，等待恢复完成。


