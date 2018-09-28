# 在Windows实例上挂载NAS文件系统 {#concept_67165_zh .concept}

如果您想要使用分布式文件系统，并在多台ECS实例上共享存储，您可以使用NAS服务。NAS服务的地域信息，请以NAS控制台上显示的信息为准。

本文以Windows Server 2012 R2系统为例，描述了如何在一台Windows ECS实例上挂载一个阿里云NAS文件系统。您可以使用类似的方法在其他版本的Windows系统上操作。

**说明：** 如果您要在一台Linux实例上挂载一个NAS文件系统，请参考[挂载文件系统](../../../../intl.zh-CN/快速入门/挂载文件系统/简介.md#)。

## 前提条件 {#section_jmj_yl3_hfb .section}

在将NAS文件系统挂载到Windows ECS实例上前，您必须先完成以下工作：

-   参考 [步骤 2：创建ECS实例](../../../../intl.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#)创建ECS示例。在本示例中，

    -   **地域**选择华东1。
    -   **镜像**选择Windows 2012 R2数据中心版本。
    -   **网络类型**选择VPC（专有网络）。
-   准备NAS文件系统及挂载点：

    1.   [开通NAS服务](https://common-buy.aliyun.com/?spm=5176.59209.972905.price1.20fa3f62xXZGAx&commodityCode=naspost#/open)。

    2.  登录[NAS控制台](https://nas.console.aliyun.com/)。

    3.  按以下步骤购买一个存储包：

        1.  在左侧导航栏中，单击**存储包**。

        2.  在**存储包管理**页面，单击**购买存储包**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313170_zh-CN.png)

        3.  在**NAS存储包**页面，选择**区域**（在本示例中，选择华东1）、**容量**和**购买时长**，单击**立即购买**，并按页面提示完成操作。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313171_zh-CN.png)

    4.  按以下步骤创建文件系统：

        1.  在NAS控制台的左侧导航栏中，单击**文件系统列表**。
        2.  选择地域（在本示例中，选择华东1） 。
        3.  单击**创建文件系统**。
        4.  在**创建文件系统**对话框中，指定文件系统的配置，并绑定已创建的存储包。
        5.  单击**确定**。
    5.   [添加挂载点](../../../../intl.zh-CN/快速入门/添加挂载点.md#)。

        挂载点是云服务器访问文件系统的入口，当前支持专有网络和经典网络挂载点，每个挂载点必须与一个权限组绑定。本示例中选择**专有网络**并选择需要的交换机。

    6.  在文件系统列表中，单击文件系统ID进入**文件系统详情**页，查看新挂载点的**挂载地址**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313172_zh-CN.png)


## 挂载文件系统 { .section}

本部分描述如何在Windows ECS实例上挂载一个NAS文件系统。本文描述的步骤适用于大部分安装了NFS客户端的Windows ECS实例。

1.   [使用软件连接Windows实例](../../../../intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#)。

2.  安装NFS客户端。

    1.  打开**服务器管理**。

    2.  选择**管理** \> **添加角色和功能**。

    3.  按**添加角色和功能向导**指示安装NFS客户端，注意以下配置：

        -   在**服务器角色**选项卡下，选择**NFS服务器**。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313173_zh-CN.png) 

        -   在**功能**选项卡下，选择**NFS客户端**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313174_zh-CN.png)

    4.  在实例内部重启。

    5.  启动**命令提示符**，运行命令 `mount`。 如果返回以下信息，说明NFS客户端安装成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313175_zh-CN.png)

3.  运行以下命令挂载NAS文件系统。

    ```
    mount -o nolock \\035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\! h:
    
    ```

    其中，`035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\` 是新挂载点的挂载地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313176_zh-CN.png)

4.  在**这台电脑**里查看新的共享文件系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362313177_zh-CN.png)

5.  在共享文件系统里新建文件夹和文件，检查是否能正常操作这个文件系统。


## 常见问题 { .section}

如果在操作时系统报错 `file handle error`，您需要确认以下注册表信息：

 **HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**，其中Locking值必须为 1。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362413178_zh-CN.png)

您也能创建以下注册表项设置GID和UID：

1.  进入**Default**注册表项目录：**HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **Default**。

2.  右击空白处，选择**新建** \> **DWORD\(32位\)值**，并创建以下两个注册表项：

    -   AnonymousGID，值为0。
    -   AnonymousUID，值为0。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362413179_zh-CN.png)

3.  运行 `mount` 检查新的UID和GID。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/153814362413180_zh-CN.png)


