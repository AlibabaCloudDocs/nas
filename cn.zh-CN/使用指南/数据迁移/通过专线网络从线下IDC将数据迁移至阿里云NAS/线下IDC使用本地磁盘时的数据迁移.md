# 线下IDC使用本地磁盘时的数据迁移 {#task_cld_w5j_kfb .task}

如果线下 IDC 使用本地磁盘作为存储设备，您可以使用 nas\_tool 软件将文件系统数据从线下 IDC 迁移至阿里云 NAS。

进行迁移前，在计算节点的系统内安装 JAVA JDK 1.7 及以上版本。您可以在[Oracle官网](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)进行下载。

1.  在线下 IDC 客户的计算节点上下载 [nas\_tool](https://nasimport.oss-cn-shanghai.aliyuncs.com/nas_tool.zip) 软件。
2.  将nas\_tool.zip解压缩至工作目录。
3.  将阿里云 NAS 文件系统挂载到线下 IDC 客户的计算节点，具体方式请参见[本地IDC VPN网络访问阿里云文件存储](../../../../cn.zh-CN/最佳实践/远程访问文件系统/本地IDC VPN网络访问阿里云文件存储.md#)。
4.  执行迁移脚本，不同操作系统中的操作如下： 
    -   在 Windows 系统中，运行`cmd`，执行`cd`命令进入 nas\_tool 所在的目录，运行以下命令：

        ```
        copy.bat <src_dir> <dst_dir>
        ```

    -   在 Linux 系统中，打开 terminal， 执行`cd`命令进入 nas\_tool 所在的目录，运行以下命令：

        ```
        sh copy.sh <src_dir> <dst_dir>
        ```


