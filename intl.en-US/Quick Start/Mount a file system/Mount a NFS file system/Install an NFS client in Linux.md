# Install an NFS client in Linux {#task_all_hsg_cfb .task}

To mount a NAS NFS file system to an ECS instance in Linux, you must install an NFS client.

1.  Log on to the ECS instance with the public DNS name and the user name of the ECS instance. 
2.  Run either of the following commands to install an NFS client: 
    -   If you use the CentOS system, run the following command:

        ```
        sudo yum install nfs-utils
        ```

    -   If you use the Ubuntu or Debian system, run the following command:

        ```
        sudo apt-get install nfs-common
        ```

3.  Run the following command to view the number of NFS requests that are initiated simultaneously: 

    ```
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```

    **Note:** 

    The number of NFS requests that are initiated simultaneously is controlled by the NFS client in Linux. If the parameter is set to a small value, the I/O performance of the system reduces. The maximum value of the parameter is 256 in the default kernel. For better I/O performance, you can run the following commands as the root user to set the parameter to a larger value:

    ```
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    sysctl -w sunrpc.tcp_slot_table_entries=128
    ```

    After modifying the parameter, restart the system.


