# 在Linux系统中安装NFS客户端 {#task_all_hsg_cfb .task}

要在 Linux 系统中将 NAS 的 NFS 文件系统挂载至 ECS 实例，您需要安装 NFS 客户端。

1.  使用 ECS 实例的公有 DNS 名称和用户名进行登录，连接至 ECS 实例。 
2.  运行以下命令，安装 NFS 客户端。 
    -   如果您使用 CentOS 操作系统，运行以下命令：

        ```
        sudo yum install nfs-utils
        ```

    -   如果您使用 Ubuntu 或 Debian 操作系统，运行以下命令：

        ```
        sudo apt-get install nfs-common
        ```

3.  运行以下命令，查看同时发起的NFS请求数量。 

    ```
    cat /proc/sys/sunrpc/tcp_slot_table_entries
    ```

    **说明：** 

    Linux NFS 客户端对于同时发起的NFS请求数量进行了控制，若该参数配置较小，会降低 IO 性能。默认编译的内核中该参数最大值为256。您可以使用root用户执行以下命令来提高该参数的值，取得较好的性能。

    ```
    echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
    echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
    sysctl -w sunrpc.tcp_slot_table_entries=128
    ```

    参数修改完成后，请重启系统。


