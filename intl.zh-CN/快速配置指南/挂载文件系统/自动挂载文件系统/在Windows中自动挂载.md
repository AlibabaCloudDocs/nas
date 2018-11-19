# 在Windows中自动挂载 {#task_bmh_dkk_2fb .task}

您可以在 Windows 系统中创建挂载脚本，通过创建计划任务的方式自动挂载 NAS 文件系统。

1.  在 Windows 系统中创建名为nas\_auto.bat的脚本文件，在文件中添加以下挂载命令，并保存到对应的磁盘路径下。 
    -   如需挂载 SMB 文件系统，添加的命令如下：

        ```
        net use Z: \\fid-xxxx.cn-shanghai.nas.aliyuncs.com\myshare 
        ```

        **说明：** 

        操作时需要将命令中的盘符（Z:）和挂载点域名（fid-xxxx.cn-shanghai.nas.aliyuncs.com）替换为实际环境中的盘符和域名。

        有关挂载命令，请参阅[挂载 SMB 文件系统](intl.zh-CN/快速配置指南/挂载文件系统/挂载 SMB 文件系统.md#)。

2.  在 Windows 的控制面板中选择**管理工具**，打开**任务计划程序**。 
3.  选择**操作** \> **创建任务**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212128_zh-CN.png)

 
4.  选择**常规**页签，输入计划任务的**名称**，选择**不管用户是否登录都要运行**和**使用最高权限运行**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212129_zh-CN.png)

 
5.  选择**触发器**页签，单击**新建**，在**开始任务**中选择**登录时**，在**高级设置**中选择**已启用**，单击**确定**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212130_zh-CN.png)

 
6.  选择**操作**页签，单击**新建**，在**操作**中选择**启动程序**，在**程序或脚本**中选择创建好的nas\_auto.bat文件，单击**确定**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212131_zh-CN.png)

 
7.  选择**条件**页签，选择**只有在以下网络连接可用时才启动**，选择**任何连接**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212132_zh-CN.png)

 
8.  选择**设置**页签，选择**如果请求后任务还在运行，强行将其停止**，在**如果此任务已经运行，以下规则适用**中选择**请勿启动新实例**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212133_zh-CN.png)

 
9.  单击**确定**。 
10. 重启服务器，验证创建结果。 如系统显示如下信息，表示计划任务可以正常执行：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21507/154259057212134_zh-CN.png)


