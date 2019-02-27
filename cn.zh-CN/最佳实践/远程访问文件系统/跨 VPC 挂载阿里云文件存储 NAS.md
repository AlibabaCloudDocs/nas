# 跨 VPC 挂载阿里云文件存储 NAS {#concept_bnk_22m_xgb .concept}

本文主要介绍如何跨 VPC 进行挂载阿里云文件存储 NAS。

默认场景下，阿里云 ECS 挂载 NAS 需要确保 ECS 和 NAS 在同一 VPC 网络环境下。但很多时候由于历史配置部署原因，ECS 的 VPC 和 NAS 挂载点的 VPC 并不一致。因此我们可以通过云企业网同账户功能来实现 VPC 的互通。

## 配置 VPC 互通 {#section_kmv_trm_xgb .section}

阿里云云企业网产品可以帮助用户实现同 Region 下的不同 VPC 互通。网络打通后VPC1 里的 ECS 可以直接 ping 通 VPC2 内的 ECS 和 NAS 挂载点。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155125194139613_zh-CN.png)

1.  创建云企业网示例
    1.  登录[云企业网管理控制台](https://cen.console.aliyun.com/)。
    2.  在云企业网实例页面，单击**创建云企业网实例**。
    3.  配置云企业网实例：

        如图所示：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155125194139616_zh-CN.png)

        配置说明如下：

        |配置|说明|
        |--|--|
        |名称| 输入云企业网实例的名称。

 名称在 2-128 个字符之间，以英文字母或中文开头，可包含数字、连字符（-）和下划线（\_）。

 |
        |描述| 输入云企业网实例的描述。

 描述在2-256个字符之间，不能以`http://`和 `https://` 开头。

 |
        |加载网络实例|您可以将位于本账号下或其他账号下的网络实例加载到云企业网实例中，详情请参见[网络实例](https://help.aliyun.com/document_detail/66001.html#concept-gbk-1mh-tdb)。|

2.  加载网络示例
    1.  在云企业网实例页面，单击已创建实例操作列中的**管理**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155125194139619_zh-CN.png)

    2.  在加载网络实例页面，单击**加载网络实例**，配置网络实例。

        如图所示：

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/132139/155125194139622_zh-CN.png)

        配置说明如下：

        |配置|说明|
        |--|--|
        |账号|选择**同账号**。|
        |实例类型|选择要互通的实例，支持加载专有网络和边界路由器实例。本操作选择专有网络实例。|
        |地域|选择所选实例的地域。本操作选择华北1。|
        |实例|选择要加载的实例。本操作选择一个 VPC 实例。|

        请重复以上操作，将两个 VPC 网络实例加载到同一个云企业网实例内，两个 VPC 网络完成互通配置。

3.  NAS 挂载验证

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


