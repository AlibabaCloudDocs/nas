# 将数据从OSS迁移到NAS {#task_lxz_n1k_kfb .task}

将线下 IDC 文件系统数据迁移至 OSS 后，您可以使用 FileSync 服务将文件系统数据从 OSS 迁移至 NAS。

1.   登录[文件存储控制台](https://nas.console.aliyun.com/)，单击**文件同步**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22754/153916271413483_zh-CN.png)

 
2.   在**管理同步任务**页面中，单击**数据地址**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22754/153916271513484_zh-CN.png)

 
3.   在**管理数据地址**页面中，单击**创建数据地址**，在**创建数据地址**对话框中，**数据类型**选择**OSS**，将 OSS 的地址配置为源数据地址。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22771/153916271513494_zh-CN.png)

 
4.   在**管理数据地址**页面中，单击**创建数据地址**，在**创建数据地址**对话框中，**数据类型**选择**NAS**，**NAS来源**选择**阿里云**，将 NAS 地址配置为目的 NAS 数据地址。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22754/153916271513486_zh-CN.png)

 
5.  返回**管理同步任务**页面，单击**创建同步任务**。 
6.   在**创建同步任务**对话框中，在**源地址**中选择 OSS 地址，在**目的地址**中选择 NAS 地址，单击**确定**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22771/153916271513495_zh-CN.png)

 
7.   在**管理同步任务**页面中查看同步任务的状态。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22771/153916271513496_zh-CN.png)

 

