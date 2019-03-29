# 跨账户挂载阿里云文件存储 NAS {#concept_tkk_hdn_xgb .concept}

本文主要介绍如何跨账户挂载阿里云文件存储 NAS。

默认情况下，阿里云 NAS 只支持挂载到同账户下的 ECS。如果一个企业用户下有多个 UID 账户，且不同账户下的 ECS 和 NAS 之间需进行数据互访，只需 ECS 与 NAS 之间的 VPC 网络互通。您可以通过云企业网的跨账户功能来实现 VPC 网络互通。

## 配置 VPC 互通 {#section_crp_jgn_xgb .section}

阿里云企业网产品可以帮助用户实现不同账号下的 VPC 互通，VPC 互通后就可以跨账号实现 NAS 的挂载访问。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/155382877939653_zh-CN.png)

1.  创建 A 账号云企业网实例
    1.  登录[云企业网管理控制台](https://cen.console.aliyun.com/)。
    2.  在云企业网实例页面，单击**创建云企业网实例**。
    3.  配置云企业网实例。

        如图所示：

        ![](images/39616_zh-CN_source.png)

        配置说明如下：

        |配置|说明|
        |--|--|
        |名称| 输入云企业网实例的名称。

 名称在 2-128 个字符之间，以英文字母或中文开头，可包含数字，连字符（-）和下划线（\_）。

 |
        |描述| 输入云企业网实例的描述。

 描述在 2-256 个字符之间，不能以`http://`和 `https://` 开头。

 |
        |加载网络实例| 您可以将位于本账号下或其他账号下的网络实例加载到云企业网实例中，详情请参见[网络实例](https://www.alibabacloud.com/help/zh/doc-detail/66001.htm)。

 |

    4.  获取已创建的云企业网实例 ID。

        本操作的云企业网实例 ID 为 cbn-xxxxxxxxxx4l7。

2.  账号 B 授权账号 A 加载其网络实例

    跨账号加载网络实例，需要在加载的 VPC 详情页面进行授权。步骤如下：

    1. 使用账号 B 登录[VPC 管理控制台](https://vpcnext.console.aliyun.com/)。

    2. 在左侧导航栏，单击**专有网络**。

    3. 单击目标 VPC 的实例 ID。

    4. 在云企业网跨账号授权信息区域，单击**云企业网跨账号授权**。

    在弹出的对话框中，输入对方账号 ID 和对方云企业网实例 ID，然后单击**确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/155382877939688_zh-CN.png)

3.  账号 A 加载网络实例

    完成授权后可以进行跨账号网络实例加载：

    1.  使用账号A登录[云企业网管理控制台](https://cen.console.aliyun.com/)。
    2.  在云企业网实例页面，单击已创建云企业网实例操作列的**管理**。
    3.  在加载网络实例页面，单击**加载网络实例**，配置网络实例：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132369/155382877939689_zh-CN.png)

        配置说明如下：

        |配置|说明|
        |--|--|
        |账号|选择**跨账号**。|
        |对方账号|输入对方账号 ID，本操作输入账号 B 的账号ID。|
        |实例类型|选择要互通的实例，支持加载专有网络和边界路由器实例。本操作选择专有网络实例。|
        |地域|选择所选实例的地域。本操作选择华北1。|
        |实例|选择要加载的实例。本操作选择一个 VPC 实例。|

4.  NAS 挂载验证

    登录 ECS 实例进行挂载验证。

    ```
    [root@ ~]#sudo mount -t nfs -o vers=4.0,vpc2挂载点域名:/ /mnt
    [root@iZbp18jc3nwxdiy5e1vkkaZ ~]# df -h
    Filesystem                                       Size  Used Avail Use% Mounted on
    /dev/vda1                                         40G  1.8G   36G   5% /
    devtmpfs                                         1.9G     0  1.9G   0% /dev
    tmpfs                                            1.9G     0  1.9G   0% /dev/shm
    tmpfs                                            1.9G  472K  1.9G   1% /run
    tmpfs                                            1.9G     0  1.9G   0% /sys/fs/cgroup
    tmpfs                                            379M     0  379M   0% /run/user/0
    082e54b989-ciq13.cn-hangzhou.nas.aliyuncs.com:/  1.0P     0  1.0P   0% /mnt
    ```


