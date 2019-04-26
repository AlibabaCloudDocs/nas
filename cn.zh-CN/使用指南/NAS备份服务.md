# NAS备份服务 {#concept_73045_zh .concept}

文件存储 NAS 无法直接进行备份，需要通过混合云备份（HBR）中的 ECS 文件备份来实现。

您可以在[混合云备份管理控制台](https://hbr.console.aliyun.com/)进行[NAS 备份](https://yq.aliyun.com/articles/696633)。

备份流程如图所示。

![](images/13198_zh-CN_source.png)

## 准备工作 {#section_ohp_0iu_zrd .section}

1.  创建挂载点，详情请参见[添加挂载点](../../../../cn.zh-CN/快速配置指南/添加挂载点.md#)。
2.  在 NAS 挂载点同一 VPC 中创建 ECS 实例。
3.  挂载 NAS 文件系统。
    -   Linux 系统挂载 NFS 文件系统，请先[安装 NFS 客户端](../../../../cn.zh-CN/快速配置指南/挂载文件系统/挂载 NFS 文件系统/在Linux系统中安装NFS客户端.md#)然后[挂载 NFS 文件系统](../../../../cn.zh-CN/快速配置指南/挂载文件系统/挂载 NFS 文件系统/在 Linux 系统中挂载 NFS 文件系统.md#)。
    -   [Windows 系统挂载 SMB 文件系统](../../../../cn.zh-CN/快速配置指南/挂载文件系统/挂载 SMB 文件系统.md#)。

## HBR ECS 文件备份 {#section_j5q_h3n_75f .section}

1.  创建 ECS 文件备份客户端。

    1.  登录[混合云备份控制台](https://hbr.console.aliyun.com)。
    2.  在左侧导航栏，选择**ECS备份** \> **ECS文件备份**，单击**添加ECS实例**。

        ![](images/13199_zh-CN_source.png)

    3.  在添加ECS实例页面，配置备份仓库名称。在下拉框中选择您之前已经创建过备份仓库，如您之前没有创建过备份仓库，单击**新建仓库**，然后输入**仓库名称**和**描述**即可创建一个新仓库。仓库名称不得超过32个字节。

        ![](images/13200_zh-CN_source.png)

    4.  添加需要备份的 ECS，单击**创建**，完成 ECS 实例在 HBR 的注册。

        ![](images/13201_zh-CN_source.png)

    更多操作详情请参见[准备工作](https://help.aliyun.com/document_detail/100942.html)。

2.  定制备份计划

    1.  在注册好的 ECS 实例操作栏，单击**备份**。

        ![](images/13202_zh-CN_source.png)

    2.  在备份页面，备份路径请填写挂载路径，请根据实际需求修改备份计划名称备份保留时间、备份起始时间以及备份执行间隔。

        ![](images/13203_zh-CN_source.png)

    3.  创建后，在备份计划和任务页签查看创建后的计划。

        ![](images/13204_zh-CN_source.png)

    **说明：** 更多操作详情请参见[备份ECS文件](https://help.aliyun.com/document_detail/100945.html)和[恢复ECS文件](https://help.aliyun.com/document_detail/95243.html)。


