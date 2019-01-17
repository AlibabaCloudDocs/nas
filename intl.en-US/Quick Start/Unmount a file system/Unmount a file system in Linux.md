# Unmount a file system in Linux {#task_f5r_3kk_2fb .task}

To delete a file system, you must unmount it from all ECS instances that have the file system mounted.

1.  Run the following command in each of the ECS instances: 

    ```
    umount <directory where the file system is mounted>
    ```

    **Note:** 

    We recommend that you do not specify any other umount options or modify their default value.

2.  Run the df command in the ECS instance to check whether the NAS file system is successfully unmounted. 

    The df command is used to query the storage usage of and statistical information about a file system mounted to the current ECS instance. If the information about a NAS file system that you unmount is not displayed in the command output, the file system is successfully unmounted.


-   View the mounting status of a NAS file system

    ```
    $ df -T
    Filesystem Type 1K-blocks Used Available Use% Mounted on
    /dev/vda1 ext4 41151808 5658860 33379516 15% /
    devtmpfs devtmpfs 8122760 0 8122760 0% /dev
    tmpfs tmpfs 8133492 0 8133492 0% /dev/shm
    tmpfs tmpfs 8133492 552 8132940 1% /run
    tmpfs tmpfs 8133492 0 8133492 0% /sys/fs/cgroup
    fid-xxxx.cn-hangzhou.nas.aliyuncs.com:/ nfs4 1099511627776 2498679808 1097012947968 1% /mnt
    
    ```

-   Unmount the file system

    ```
    $ umount /mnt 
    ```


