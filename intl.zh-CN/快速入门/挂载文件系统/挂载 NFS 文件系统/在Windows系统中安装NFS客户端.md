# 在Windows系统中安装NFS客户端 {#concept_o2f_dyg_cfb .concept}

要在 Windows 系统中将 NAS 的 NFS 文件系统挂载至 ECS 实例，您需要安装 NFS 客户端。

NFS 客户端在不同 Windows 系统中的安装和配置方式不同，本文分别介绍在 Windows 7、Windows Server 2008 及 Windows Server 2012 中安装和配置 NFS 客户端的方法。

## 在 Windows 7 系统中安装和配置 NFS 客户端 {#section_skw_l1h_cfb .section}

1.  在 Windows 系统中，打开控制面板，选择**程序与功能** \> **打开或关闭 Windows 功能**，勾选**NFS 服务**及其下的**NFS 客户端**和**管理工具**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501511651_zh-CN.png)

2.  在控制面板中，选择**管理工具** \> **Network File System 服务\(NFS\)**，右键单击**NFS 客户端**，选择**属性**，将**传输协议**修改为**TCP**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501511652_zh-CN.png)

3.  在 Windows 的 cmd 中运行 regedit.exe，选择**HKEY\_CURRENT\_USER** \> **Software** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **MountUtility** \> **Mount**，在右侧内容区中将**Locking**的值设为**1**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501511653_zh-CN.png)

    。

    **说明：** NFS 客户端默认使用 NFSv3 协议且支持 Lock 挂载。而 NAS 目前不支持 Lock，因此为了正常使用，需要按照上述步骤禁用 Lock。


## 在 Windows Server 2008 系统中安装和配置 NFS 客户端 {#section_tjl_wch_cfb .section}

1.  进入**服务器管理器**，选择**功能** \> **添加功能**，然后选择**远程服务器管理工具** \> **角色管理工具** \> **文件服务工具** \> **网络文件系统服务工具**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501511654_zh-CN.png)

2.  在**服务器管理器**，选择**角色** \> **添加角色**，勾选**文件服务**，单击**下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611655_zh-CN.png)

3.  勾选**文件服务器**和**网络文件系统服务**，单击**下一步**，按照引导完成角色添加。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611656_zh-CN.png)

4.  在开始菜单中选择**管理工具** \> **Network File System服务 \(NFS\)**，右键单击**NFS 客户端**，选择**属性**，将**传输协议**修改为**TCP**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611658_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611657_zh-CN.png)

5.  在 Windows 的 cmd 中运行 regedit.exe，选择**HKEY\_CURRENT\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**，在右侧内容区中单击右键，选择**新建** \> **DWORD \(32-位\)值**， 将新建的 key 名称设为**Locking**， 将其值设为**1**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611659_zh-CN.png)

    **说明：** NFS 客户端默认使用 NFSv3 协议且支持 Lock 挂载。而 NAS 目前不支持 Lock，因此为了正常使用，需要按照上述步骤禁用 Lock。


## 在 Windows Server 2012 系统中安装和配置 NFS 客户端 {#section_f3w_kgh_cfb .section}

1.  进入**服务器管理器**，选择**添加角色和功能**，在**服务器角色**步骤中勾选**NFS 服务器**，单击**下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611660_zh-CN.png)

2.  在**功能**步骤中勾选**NFS 客户端**，单击**下一步**，按照引导完成角色添加。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611661_zh-CN.png)

3.  在开始菜单中选择**管理工具** \> **Network File System服务 \(NFS\)**，右键单击**NFS 客户端**，选择**属性**，将**传输协议**修改为**TCP**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611662_zh-CN.png)

4.  在 Windows 的 cmd 中运行 regedit.exe，选择**HKEY\_CURRENT\_MACHINE** \> **SOFTWARE** \> **Microsoft** \> **ClientForNFS** \> **CurrentVersion** \> **User** \> **Default** \> **Mount**，在右侧内容区中单击右键，选择**新建** \> **DWORD \(32-位\)值**， 将新建的 key 名称设为**Locking**， 将其值设为**1**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21204/153805501611659_zh-CN.png)

    **说明：** NFS 客户端默认使用 NFSv3 协议且支持 Lock 挂载。而 NAS 目前不支持 Lock，因此为了正常使用，需要按照上述步骤禁用 Lock。


