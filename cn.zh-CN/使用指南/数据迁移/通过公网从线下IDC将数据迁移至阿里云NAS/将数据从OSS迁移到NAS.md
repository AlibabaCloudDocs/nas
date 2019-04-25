# 将数据从OSS迁移到NAS {#task_lxz_n1k_kfb .task}

将线下 IDC 文件系统数据迁移至 OSS 后，您可以使用 FileSync 服务将文件系统数据从 OSS 迁移至 NAS。

迁移操作方法如下，更多详情请参见[OSS 迁移至 NAS 教程](https://help.aliyun.com/document_detail/116067.html)。

1.  登录[文件存储控制台](https://nas.console.aliyun.com/)，单击**文件同步**。![](images/13483_zh-CN_source.png)


2.  在数据迁移服务页面，单击**数据地址**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22771/155616118445379_zh-CN.png)


3.  在**管理数据地址**页面中，单击**创建数据地址**，在**创建数据地址**对话框中，**数据类型**选择**OSS**，将 OSS 的地址配置为源数据地址。![](images/13494_zh-CN_source.png)


4.  在**管理数据地址**页面中，单击**创建数据地址**，在**创建数据地址**对话框中，**数据类型**选择**NAS**，**NAS来源**选择**阿里云**，将 NAS 地址配置为目的 NAS 数据地址。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22754/155616118413486_zh-CN.png)


5.  关闭**管理数据地址**页面，单击**迁移任务****创建迁移任务**。
6.  在**创建迁移任务**对话框中，在**源地址**中选择 OSS 地址，在**目的地址**中选择 NAS 地址，单击**确定**。![](images/13495_zh-CN_source.png)


7.  在迁移任务列表页面中查看迁移任务的状态。![](images/13488_zh-CN_source.png)



