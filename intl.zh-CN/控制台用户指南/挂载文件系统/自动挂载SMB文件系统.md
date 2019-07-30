# 自动挂载SMB文件系统 {#task_bmh_dkk_2fb .task}

本文档介绍如何在Windows系统中创建挂载脚本及计划任务，使其重启时自动挂载SMB文件系统。

## 前提条件 {#section_qxx_g4r_16u .section}

1.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
2.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。
3.  确保Windows系统服务中的以下两项服务均已启动。
    -   Workstation

        1.  选择**所有程序** \> **附件** \> **运行**或使用快捷键`Win+R`，输入`services.msc`进入本地服务。
        2.  在服务中找到 Workstation，确认运行状态为**已启动**。

            正常情况下，Workstation 服务默认为启动状态。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156447384142055_zh-CN.png)

    -   TCP/IP NetBIOS Helper

        开启 TCP/IP NetBIOS Helper 服务步骤如下所示：

        1.  打开**网络与共享中心**，单击主机所连网络。
        2.  单击**属性**，双击 **Internet 协议版本 4** 进入属性框，单击**高级**。
        3.  在高级TCP IP设置对话框中，选择 **WINS** \> **启用 TCP/IP 上的 NetBIOS**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156447384142056_zh-CN.png)


## 操作步骤 {#section_asn_ci4_x0r .section}

1.  登录[云服务器 ECS](https://ecs.console.aliyun.com/)。
2.  创建名为nas\_auto.bat的脚本文件，在文件中添加以下挂载命令。

    ``` {#codeblock_ad0_f5r_ff5}
    net use D: \\file-system-id.region.nas.aliyuncs.com\myshare 
    ```

    挂载命令格式：`net use <挂载目标盘符> \\<挂载点域名>\myshare`。

    -   挂载目标盘符：指当前Windows系统上要挂载的目标盘符，请根据实际值替换。
    -   挂载点域名：指创建文件系统挂载点时，自动生成的挂载点域名，请根据实际值替换。挂载点详情请参见[添加挂载点](cn.zh-CN/快速入门/容量型__性能型NAS/Windows系统.md#)。
    -   myshare： SMB的share名称，不允许变更。
    **说明：** 

    目标盘符不能和本地盘符重名。

3.  创建计划任务。
    1.  打开控制面板，选择**管理工具** \> **任务话程序**。
    2.  在任务计划程序页面，选择**操作** \> **创建任务**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384212128_zh-CN.png)

    3.  选择**常规**页签，输入计划任务的**名称**，勾选**不管用户是否登录都要运行**和**使用最高权限运行**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384212129_zh-CN.png)

    4.  选择**触发器**页签，单击**新建**，在**开始任务**中选择**登录时**，在**高级设置**中选择**已启用**，单击**确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384212130_zh-CN.png)

    5.  选择**操作**页签，单击**新建**，在**操作**中选择**启动程序**，在**程序或脚本**中选择创建好的nas\_auto.bat文件，单击**确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384212131_zh-CN.png)

    6.  选择**条件**页签，选择**只有在以下网络连接可用时才启动**。在**只有在以下网络连接可用时才启动**中选择**任何连接**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384312132_zh-CN.png)

    7.  选择**设置**页签，选择**如果请求后任务还在运行，强行将其停止**，在**如果此任务已经运行，以下规则适用**中选择**请勿启动新实例**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384312133_zh-CN.png)

    8.  单击**确定**。
    9.  重启服务器，验证创建结果。

        如果系统显示如下信息，表示计划任务正常执行。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/156447384312134_zh-CN.png)

4.  打开命令行窗口，执行`net use`命令，检查挂载结果。

    如果回显包含如下类似信息，说明挂载成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21209/156447384349545_zh-CN.png)


