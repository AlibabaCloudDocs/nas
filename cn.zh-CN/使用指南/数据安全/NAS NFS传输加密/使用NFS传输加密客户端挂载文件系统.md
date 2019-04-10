# 使用NFS传输加密客户端挂载文件系统 {#task_smf_p34_mfb .task}

下载安装 NFS 传输加密客户端后，您可以使用该客户端加密挂载 NAS 文件系统。

NFS 传输加密客户端能够通过 TLS 方式挂载文件系统，并在挂载时使用阿里云 NAS 推荐的挂载选项。同时，该客户端还提供了日志功能，便于在挂载出错时定位错误原因。

NFS 传输加密客户端定义了一个新的网络文件类型：alinas。该文件类型能够与标准的 `mount` 命令无缝兼容。客户端还支持在系统启动时自动挂载文件系统，您可以在/etc/fstab文件中添加相关参数完成。使用NFS 传输加密客户端进行 TLS 挂载时，工具会启动一个 stunnel 进程和一个监控进程 aliyun-alinas-mount-watchdog. stunnel 进程会对应用与 NAS 间的读写进行 TLS 加密并转发给 NAS 服务器。

1.  登录[文件存储控制台](https://nas.console.aliyun.com/)。 
2.  创建一个新的挂载点，详细步骤请参阅[添加挂载点](../../../../../cn.zh-CN/快速配置指南/添加挂载点.md#)。 

    **说明：** 文件系统中原有的挂载点不支持通过 TLS 方式挂载文件系统，因此必须要创建一个新的挂载点。

3.  运行以下命令，检查新建的挂载点是否支持传输加密。 

    ```
    telnet 6e1854xxxx-xxxx.cn-qingdao.nas.aliyuncs.com 12049
    ```

    如果出现以下界面，则表示挂载点支持传输加密。其中`6e1854xxxx-xxxx.cn-qingdao.nas.aliyuncs.com`为新建的挂载点的名称。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23840/155488568913835_zh-CN.png)

4.  运行以下命令，挂载文件系统。 

    ```
    sudo mount -t alinas -o tls file-system-mountpoint alinas-mount-point/
    ```

    示例：`sudo mount –t alinas –o tls 606294xxxx-xxxx.cn-qingdao.nas.aliyuncs.com /mnt`

5.  运行以下命令，添加其他挂载参数。 

    ```
    sudo mount –t alinas –o tls,noresvport 606294xxxx-xxxx.cn-qingdao.nas.aliyuncs.com /mnt
    ```

    **说明：** NFS 传输加密工具默认使用以下选项挂载文件系统：

    -   vers=4.0
    -   rsize=1048576
    -   wsize=1048576
    -   hard
    -   timeo=600
    -   retrans=2
6.  在/etc/fstab中添加以下 entry，开启自动挂载： 

    ```
    file-system-mountpoint local-mount-point alinas _netdev,tls 0 0
    ```

    示例：`606294xxxx-xxxx.cn-qingdao.nas.aliyuncs.com /mnt alinas _netdev,tls 0 0`


