# How to unmount a file system from an ECS instance that runs Windows {#task_khy_jhy_zfb .task}

This section describes how to unmount a NAS file system whose protocol type is SMB from an ECS instance that runs Windows.

1.  Open the command prompt, and enter the NET USE command to view available network connections. 

    Example:

    ```
    
    Status                 Local       Remote            Network
    --------------------------------------------------------------------------------
    OK                                 \\name\IPC$       Microsoft Windows Network
    OK                                 \\name2\folder    Microsoft Windows Network
    ```

2.  You can use the net use \\\\name /delete command or the net use \\\\name2\\folder /delete command to unmount a specific file system. You can enter the net use \* /delete command to manually unmount all of the available file systems in Windows. You can also enter the net use \* /delete /y command to automatically unmount all of the available file systems in Windows.
3.  You can enter the NET USE command to verify that all of the available file systems are unmounted in Step 2. 

