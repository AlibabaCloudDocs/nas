# 在Windows系统中挂载NFS文件系统 {#concept_vq1_s4h_cfb .concept}

在 Windows 系统中安装并配置 NFS 客户端后，即可以挂载 NFS 文件系统。

您可以运行以下格式的命令，挂载 NFS 文件系统：

```
mount -o nolock \\fid-xxxx.cn-hangzhou.nas.aliyuncs.com\! F:
```

**说明：** 运行命令时，您需要注意以下内容：

-   命令中的感叹号不能省略，`F:`为本地任一空闲盘符。
-   不建议在 Windows 下挂载文件系统的非根目录，否则在进行 rename 等操作会发生 invalid device 错误。
-   在Linux系统创建的文件，如果需要Windows系统读写权限，需要对文件和文件夹做相应的设置。
-   在 Windows 系统中挂载文件系统时，默认为匿名用户访问，Windows 上创建的文件在 Linux 上看到的权限默认为 0755。该默认权限可以按照以下步骤修改：在网络文件服务系统窗口中，右键单击**NFS 客户端**，选择**属性**，在**文件权限**页签中修改。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21208/153665315311663_zh-CN.png)


