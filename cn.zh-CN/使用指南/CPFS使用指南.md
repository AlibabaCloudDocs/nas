# CPFS使用指南 {#concept_cyg_wng_4gb .concept}

CPFS是阿里云新上线的并行文件存储服务，专注于提供高性能的文件存储和访问能力。

使用 CPFS 的操作步骤如下：

1.  创建文件系统
    1.  登录[阿里云文件存储控制台](https://nas.console.aliyun.com/)，在左侧边栏选择CPFS，如下图所示：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/154832404638078_zh-CN.png)

    2.  单击右上角**创建文件系统**按钮，进入购买页面。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/154832404638079_zh-CN.png)

    3.  请根据您自身需求进行基本配置、网络配置和购买量的选择。

        -   基本配置需要选定地域、可用区和文件系统的容量。
        -   网络配置需要选定指定地域内的专有网络和虚拟交换机。若您还未创建，请先前往[阿里云专有网络控制台](https://vpc.console.aliyun.com/)进行相关配置。
        -   购买量的选择需要选定文件系统实例数量和服务时长。

        CPFS服务目前采用预付费模式（即包年包月），服务期间您可以根据自身业务增长情况选择升级存储量，服务到期您可以选择续费。

2.  管理文件系统

    购买成功后，回到阿里云文件存储控制台，即可看到您的CPFS实例正在创建中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/154832404638080_zh-CN.png)

    CPFS实例创建过程大约需要10分钟，创建成功后，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/119749/154832404638081_zh-CN.png)

    您可以选择单击**管理**按钮，查看实例详情；单击**升级**按钮进行容量升级；单击**续费**按钮进行服务续费。

3.  使用文件系统

    CPFS文件系统创建完成后，在客户端ECS上进行挂载即可使用。

    1.  下载并安装客户端软件包
    2.  配置文件统挂载点

        使用控制台展示的文件系统挂载点进行挂载配置。

    3.  挂载CPFS文件系统
    4.  使用CPFS文件系统

        CPFS文件系统兼容POSIX语义，可以使用Linux的常见操作命令（如`ls`等）进行访问和操作文件系统。


