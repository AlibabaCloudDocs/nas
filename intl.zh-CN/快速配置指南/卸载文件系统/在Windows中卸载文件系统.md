# 在Windows中卸载文件系统 {#task_khy_jhy_zfb .task}

本文档介绍如何在 Windows 系统中卸载 NAS 的 SMB 文件系统。

1.  打开 CMD，输入命令NET USE查看所有的网络连接。 

    示例如下：

    ```
    
    Status                 Local       Remote            Network
    --------------------------------------------------------------------------------
    OK                                 \\name\IPC$       Microsoft Windows Network
    OK                                 \\name2\folder    Microsoft Windows Network
    ```

2.  您可以输入命令net use \\\\name /delete或者net use \\\\name2\\folder /delete卸载指定的文件系统。 您可以输入命令net use \* /delete，手动卸载 Windows 下所有已挂载的文件系统。您还可以输入命令net use \* /delete /y，自动卸载 Windows 下所有已挂载的文件系统。
3.  您可以输入命令NET USE，验证是否已成功卸载步骤 2 中指定的或者所有已挂载的文件系统。 

