# Windows 系统使用 NFS 协议挂载 NAS {#concept_67165_zh .concept}

本文主要介绍如何在 Windows 系统环境下使用 NFS 协议挂载 NAS。

如果您需要使用分布式文件系统，且在多台 ECS 实例上共享存储，推荐您使用 NAS 服务。NAS 服务的地域信息，请以 NAS 控制台上显示的信息为准。

本文以 Windows Server 2012 R2 系统为例，在 Windows ECS 实例上挂载阿里云 NAS 文件系统。其他版本的 Windows 系统操作方式类似。

**说明：** Linux 系统挂载 NAS 文件系统，请参见[挂载文件系统](../../../../cn.zh-CN/控制台用户指南/挂载文件系统/挂载说明.md#)。

## 前提条件 {#section_jmj_yl3_hfb .section}

挂载 NAS 文件系统前，请先完成以下工作。

-   参见 [创建ECS实例](../../../../cn.zh-CN/个人版快速入门/创建ECS实例.md#)创建 ECS 示例。

    示例：

    -   **地域**：华东1。
    -   **镜像**：Windows 2012 R2 数据中心版本。
    -   **网络类型**：VPC（专有网络）。
-   准备 NAS 文件系统及挂载点
    1.  [开通 NAS 服务](https://common-buy.aliyun.com/?spm=5176.59209.972905.price1.20fa3f62xXZGAx&commodityCode=naspost#/open)。

    2.  登录[NAS 控制台](https://nas.console.aliyun.com/)。

    3.  购买存储包
        1.  在左侧导航栏中，单击**存储包**。
        2.  在存储包管理页面，单击**购买存储包**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706380613170_zh-CN.png)

        3.  在NAS 存储包页面，选择**区域**（本示例选择华东1）、**容量**和**购买时长**，单击**立即购买**，并按页面提示完成操作。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706380813171_zh-CN.png)

    4.  创建文件系统
        1.  在NAS控制台的左侧导航栏中，单击**文件系统列表**。
        2.  选择**地域**（在本示例中，选择华东1） 。
        3.  单击**创建文件系统**。
        4.  在创建文件系统对话框中，指定文件系统的配置，并绑定已创建的存储包。
        5.  单击**确定**。
    5.  [../../../../dita-oss-bucket/SP\_111/DNnas1858274/ZH-CN\_TP\_18691.md\#](../../../../cn.zh-CN/快速入门/容量型__性能型NAS/Windows系统.md#) 

        挂载点是云服务器访问文件系统的入口，当前支持专有网络和经典网络挂载，每个挂载点必须与一个权限组绑定。本示例选择**专有网络**并选择需要的交换机。

    6.  查看挂载地址

        在文件系统列表中，单击文件系统 ID 进入文件系统详情页面，查看新挂载点的**挂载地址**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381013172_zh-CN.png)


## 挂载文件系统 { .section}

挂载文件系统操作步骤如下：

1.  [../../../../dita-oss-bucket/SP\_2/DNA0011894323/ZH-CN\_TP\_9622.md\#](../../../../cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)。
2.  安装NFS客户端。
    1.  打开**服务器管理**。
    2.  选择**管理** \> **添加角色和功能**。
    3.  按**添加角色和功能向导**指示安装NFS客户端。
        1.  在**服务器角色**选项卡下，选择**NFS服务器**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381013173_zh-CN.png)

        2.  在**功能**选项卡下，选择**NFS客户端**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381213174_zh-CN.png)

    4.  重启实例。
    5.  启动**命令提示符**，运行命令 `mount`。 如果返回以下信息，说明NFS客户端安装成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381513175_zh-CN.png)

3.  运行以下命令挂载 NAS 文件系统。

    ```
    mount -o nolock \\035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\! h:
    					
    ```

    `035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\` 是新挂载点的挂载地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381513176_zh-CN.png)

4.  在**这台电脑**界面查看新的共享文件系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381513177_zh-CN.png)

5.  在共享文件系统里新建文件夹和文件，检查是否能正常操作该文件系统。

## 常见问题 { .section}

如果在操作时系统报错 `file handle error`，您需要确认以下注册表信息：

**说明：** 如果找不到 Locking、AnonymousGID、AnonymousUID 这三个注册表项，则按照 Windows 的字段格式要求进行创建。

**HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**，其中 Locking 值必须为 1。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706381713178_zh-CN.png)

创建以下注册表项设置 GID 和 UID：

1.  进入 **Default** 注册表项目录：**HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **Default**。
2.  右击空白处，选择**新建** \> **DWORD\(32位\)值**，并创建以下两个注册表项。
    -   AnonymousGID，值为0。
    -   AnonymousUID，值为0。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706382013179_zh-CN.png)

3.  运行 `mount` 检查新的 UID 和 GID。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156706382813180_zh-CN.png)


