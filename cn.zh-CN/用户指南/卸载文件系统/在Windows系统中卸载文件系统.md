# 在Windows系统中卸载文件系统 {#task_khy_jhy_zfb .task}

本文档介绍如何在云服务器ECS（Windows 系统）中卸载SMB文件系统。

1.  登录[云服务器 ECS](https://ecs.console.aliyun.com/)。
2.  打开命令行窗口，执行以下命令卸载文件系统。 

    ``` {#codeblock_ult_4vw_cik}
    net use D: /delete
    ```

    挂载命令中的盘符（D:），请根据实际挂载盘符进行替换。您可执行`net use`命令，获取挂载盘符。

    **说明：** 

    -   执行 net use \* /delete命令，手动卸载 Windows 系统中所有已挂载的文件系统。
    -   执行net use \* /delete /y命令，自动卸载 Windows 系统中所有已挂载的文件系统。
3.  执行`net use`命令，查看卸载结果。 如果回显中未找到您挂载的SMB文件系统信息，表示该文件系统已卸载成功。

