# Unmount a file system from an ECS instance running Linux {#task_f5r_3kk_2fb .task}

This topic describes how to unmount a file system from an ECS instance running Linux.

1.  Log on to the [ECS console](partners-intl.console.aliyun.com/#/ecs).
2.  Run the `umount /mnt` command to unmount an NFS file system. 

    Replace the /mnt directory with a directory specific to your environment.

    The format of the unmount command is `umount /<the directory of a mount point\>`.

    **Note:** 

    We recommend that you do not specify any other umount parameters and avoid changing the default values of these parameters.

    When unmounting a file system, an error indicating that the device is busy may occur. Use the kill command to terminate the processes that are accessing the file system.

    1.  Install fuser.
        -   fuser is preinstalled in CentOS, RHEL, and Aliyun Linux. You do not need to reinstall fuser on these systems.
        -   For Ubuntu or Debian, run the `apt install -y fuser` command to install the tool.
    2.  Run the `fuser -mv <the directory of a mount point>` command to view the process ID of each process that is accessing the NAS file system.
    3.  Run the `kill <pid>` command to terminate a process.
3.  Run the `mount -l` command to verify the unmount results. 

    If a NAS file system is not displayed in the unmount result, it indicates that the file system is unmounted.


