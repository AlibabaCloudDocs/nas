# Unmount a file system from an ECS instance that runs Windows {#task_khy_jhy_zfb .task}

This section describes how to unmount a NAS file system whose protocol type is SMB from an ECS instance that runs Windows.

1.  Open the command prompt, enter the NET USE command to view all of the available network connections 

    Example:

    ```
    
    Status                 Local       Remote            Network
    --------------------------------------------------------------------------------
    OK                                 \\name\IPC$       Microsoft Windows Network
    OK                                 \\name2\folder    Microsoft Windows Network
    ```

2.  You can use the net use \\\\name /delete command or the net use \\\\name2\\folder /delete command to unmount a specific file system. 

    **Note:** 

    -   You can use the net use \* /delete command to manually unmount all of the available file systems in Windows.
    -   You can use the Net use \*/delete/y command to automatically unmount all of the file systems in Windows.
3.  Open the command prompt, enter the NET USE command to verify that all of the available file systems are unmounted. 

