# 在Windows中卸载文件系统 {#task_khy_jhy_zfb .task}

本文档介绍如何在 Windows 系统中卸载 NAS 的 SMB 文件系统。

1.  打开 CMD，输入命令 NET USE 查看所有的网络连接。 

    示例如下：

    ```
    
    Status                 Local       Remote            Network
    --------------------------------------------------------------------------------
    OK                                 \\name\IPC$       Microsoft Windows Network
    OK                                 \\name2\folder    Microsoft Windows Network
    ```

2.  您可以输入命令 net use \\\\name /delete 或者 net use \\\\name2\\folder /delete 卸载指定的文件系统。 

    **说明：** 

    -   命令 net use \* /delete，手动卸载 Windows 系统中所有已挂载的文件系统。
    -   命令net use \* /delete /y，自动卸载 Windows 系统中所有已挂载的文件系统。
3.  在 CMD 中输入命令 NET USE，查看文件系统已成功卸载。 

