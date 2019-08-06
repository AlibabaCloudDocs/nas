# 手动挂载SMB文件系统 {#concept_zb5_1rh_cfb .task}

本文档介绍如何在Windows系统中手动挂载SMB文件系统。

## 前提条件 {#section_zlq_3j1_dfb .section}

1.  已创建文件系统，详情请参见[创建文件系统](intl.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
2.  已添加挂载点，详情请参见[添加挂载点](intl.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。
3.  确保Windows系统服务中的以下两项服务均已启动。
    -   Workstation
        1.  选择**所有程序** \> **附件** \> **运行**或使用快捷键`Win+R`，输入`services.msc`进入本地服务。
        2.  在服务中找到 Workstation，确认运行状态为**已启动**，启动类型为**自动**。

            正常情况下，Workstation 服务默认为启动状态。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507786642055_zh-CN.png)

    -   TCP/IP NetBIOS Helper

        开启 TCP/IP NetBIOS Helper 服务步骤如下所示：

        1.  打开**网络与共享中心**，单击主机所连网络。
        2.  单击**属性**，双击 **Internet 协议版本 4** 进入属性框，单击**高级**。
        3.  在高级TCP IP设置对话框中，选择 **WINS** \> **启用 TCP/IP 上的 NetBIOS**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507786642056_zh-CN.png)

        4.  选择**所有程序** \> **附件** \> **运行**或使用快捷键`Win+R`，输入`services.msc`进入本地服务。
        5.  在服务中找到 TCP/IP NetBIOS Helper，确认运行状态为**已启动**，启动类型为**自动**。

            正常情况下，TCP/IP NetBIOS Helper 服务默认为启动状态。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507786654417_zh-CN.png)


## 操作步骤 {#section_pgk_srh_cfb .section}

执行以下步骤挂载SMB文件系统。

1.  登录[云服务器 ECS](https://ecs.console.aliyun.com/)。
2.  打开命令行窗口，执行以下命令挂载文件系统。

    ``` {#codeblock_qt9_gik_x61}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare
    ```

    挂载命令格式：`net use <挂载目标盘符> \\<挂载点域名>\myshare`。

    -   挂载目标盘符：指当前Windows系统上要挂载的目标盘符，请根据实际值替换。
    -   挂载点域名：指创建文件系统挂载点时，自动生成的挂载点域名，请根据实际值替换。挂载点详情请参见[添加挂载点](intl.zh-CN/快速入门/容量型__性能型NAS/Windows系统.md#)。
    -   myshare： SMB的share名称，不允许变更。
    **说明：** 

    目标盘符不能和本地盘符重名。

    如果执行挂载命令报错，可参见[SMB 挂载失败的原因分析](../intl.zh-CN/常见问题/SMB FAQ/SMB 挂载失败的原因分析.md#)进行排查。

3.  执行`net use`命令，检查挂载结果。

    如果回显包含如下类似信息，说明挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156507786649545_zh-CN.png)

4.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。

