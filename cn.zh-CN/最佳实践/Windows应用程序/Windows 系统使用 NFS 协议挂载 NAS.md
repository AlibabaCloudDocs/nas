# Windows 系统使用 NFS 协议挂载 NAS {#concept_67165_zh .task}

本文主要介绍如何在 Windows 系统环境下使用 NFS 协议挂载 NAS。

挂载 NAS 文件系统前，请先完成以下工作。

1.  已开通NAS服务。

    首次登录[NAS控制台](https://nas.console.aliyun.com/)时，根据页面提示开通NAS服务。

2.  在需要创建文件系统的地域，已有可用的专有网络 VPC。

    如果没有，请创建专有网络 VPC，详情请参见[创建专有网络和交换机](创建专有网络和交换机../../SP_22/DNVPC11885991/ZH-CN_TP_2434.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb)。

3.  在需要创建文件系统的地域，已有可用的云服务器 ECS，并将此云服务器 ECS 归属到已创建的专有网络VPC下。

    如果没有，请购买云服务器 ECS，详情请参见[创建ECS实例](../../../../cn.zh-CN/个人版快速入门/创建ECS实例.md#)。

    **说明：** 如果要创建专有网络类型的挂载点，还需在创建文件系统的地域上创建专有网络 VPC，并将已创建的云服务器 ECS 归属到此专有网络 VPC 下，详情请参见[创建专有网络和交换机](创建专有网络和交换机../../SP_22/DNVPC11885991/ZH-CN_TP_2434_V13.dita#concept_isl_ghv_rdb/section_ufw_rhv_rdb) 。

4.  已创建文件系统。

    如果没有，请创建文件系统，详情请参见[创建文件系统](../../../../cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。

5.  已为文件系统添加挂载点。

    如果没有，请添加挂载点，详情请参见[添加挂载点](../../../../cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。


如果您需要使用分布式文件系统，且在多台 ECS 实例上共享存储，推荐您使用 NAS 服务。NAS 服务的地域信息，请以 NAS 控制台上显示的信息为准。

本文以 Windows Server 2012 R2 系统为例，在 VPC 网络下的 Windows ECS 实例上挂载阿里云 NFS 文件系统。其他版本的 Windows 系统操作方式类似。

## 挂载文件系统 {#section_m3p_e5t_ip9 .section}

1.  在本地客户端上连接 Windows 实例，详情请参见[在本地客户端上连接Windows实例](../../../../cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)。
2.  安装 NFS 客户端。 
    1.  打开**服务器管理**
    2.  选择**管理** \> **添加角色和功能**。
    3.  根据**添加角色和功能向导**指示安装NFS客户端。 

        在**服务器角色**选项卡下，选择**NFS服务器**。

        在**功能**选项卡下，选择**NFS客户端**。

    4.  重启实例。
    5.  启动**命令提示符**，运行命令 `mount`。 如果返回以下信息，说明NFS客户端安装成功。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566213175_zh-CN.png)

3.  运行以下命令挂载 NAS 文件系统。 

    ``` {#codeblock_5l4_qjb_m6i}
    mount -o nolock -o mtype=hard -o timeout=60 \\035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\! h:                   
    ```

    `035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\` 是新挂载点的挂载地址。

4.  执行`mount`检查挂载结果。 

    挂载完成后，回显信息必须包括mount=hard、locking=no以及timeout参数\>=10，否则说明挂载有问题。

    ![检查UID和GID](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566213180_zh-CN.png)

5.  在**这台电脑**界面查看新的共享文件系统。 

    在共享文件系统里新建文件夹和文件，检查是否能正常操作该文件系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566213177_zh-CN.png)


## 常见问题 {#section_2u4_3qx_r09 .section}

如果在操作时系统报错 `file handle error`，您需要确认以下注册表信息：

**说明：** 如果找不到 Locking、AnonymousGID、AnonymousUID 这三个注册表项，则按照 Windows 的字段格式要求进行创建。

**HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**，其中 Locking 值必须为 1。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566313178_zh-CN.png)

创建以下注册表项设置 GID 和 UID：

1.  进入 **Default** 注册表项目录：**HKEY\_LOCAL\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **Default**。
2.  右击空白处，选择**新建** \> **DWORD\(32位\)值**，并创建以下两个注册表项。 
    -   AnonymousGID，值为0。
    -   AnonymousUID，值为0。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566313179_zh-CN.png)

3.  重启实例。
4.  运行以下命令挂载 NAS 文件系统。 

    ``` {#codeblock_bcu_68e_don}
    mount -o nolock -o mtype=hard -o timeout=60 \\035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\! h:                   
    ```

    `035XXXXXXX3.cn-hangzhou.nas.aliyuncs.com\` 是新挂载点的挂载地址。

5.  运行 `mount` 检查新的 UID 和 GID。 

    挂载完成后，回显信息必须包括mount=hard、locking=no以及timeout参数\>=10，否则说明挂载有问题。

    ![检查UID和GID](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18709/156775566213180_zh-CN.png)


