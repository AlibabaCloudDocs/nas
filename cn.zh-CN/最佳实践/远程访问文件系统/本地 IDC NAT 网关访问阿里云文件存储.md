# 本地 IDC NAT 网关访问阿里云文件存储 {#concept_57628_zh .concept}

本文主要介绍本地 IDC 通过 NAT 进行跨地域挂载文件系统。

阿里云文件存储服务只支持同一地域内的 ECS 挂载，本地 IDC 或跨地域ECS 无法直接挂载 。无法直接挂载时，需要通过建立高速通道进行挂载，但成本往往很高。

对于之前已经在自己机房部署了 VPN 服务的用户，我们推荐使用阿里云的 VPN 网关来实现办公环境或者 IDC 到阿里云 NAS 的互通，具体操作方法请参见[本地IDC VPN网络访问阿里云文件存储](cn.zh-CN/最佳实践/远程访问文件系统/本地IDC VPN网络访问阿里云文件存储.md#)。

由于部署 VPN 较为繁琐，而且阿里云 VPN 目前是按月收费的（每月收费从几百到几千不等）。将少量的线下数据上传到阿里云文件存储 NAS 时，使用 VPN 会有很大的浪费？接下来我们就来介绍一个更简单（而且花费更少）的方案：使用 NAT 网关实现从公网访问阿里云 NAS。

使用 NAT 网关从公网访问阿里云 NAS 的网络架构如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613110_zh-CN.png)

操作步骤如下：

1.  创建 NAS 文件系统。
2.  为文件系统添加挂载点。
3.  创建 NAT 网关。
4.  为 NAT 网关添加带宽包，获得公网 IP（EIP）。
5.  为 NAT 网关添加 DNAT 转发条目。

通过以上五步，可以在任何一台连接公网的 PC（Windows 或 Linux）挂载 NAS，实现文件的上传和下载。

操作步骤示例如下：

1.  在 NAS 控制台创建文件系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613111_zh-CN.png)

2.  为文件系统添加挂载点，且需要创建 VPC 挂载点（NAT 只支持 VPC）

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613112_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613113_zh-CN.png)

3.  获得挂载点的 IP

    可以在 ECS 中 ping 挂载点地址获得 IP。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613114_zh-CN.png)

4.  在 NAT 控制台创建 NAT 网关 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613115_zh-CN.png)

5.  为 NAT 网关添加带宽包。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613116_zh-CN.png)

6.  创建 DNAT

    -   公网 IP：创建 EIP 时，产生公网 IP。
    -   私网 IP：填写需要访问的挂载点的 IP。
    -   端口：推荐选择**所有端口**，可以选择安装 NFS 或 SMB 时相应的端口。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613117_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984613118_zh-CN.png)

7.  验证挂载 NFS，将 NAT 映射配置到一个 NFS 的挂载点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984813119_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984813120_zh-CN.png)

8.  验证挂载 SMB，删除原来的 NAT 映射，添加一条映射配置到一个 SMB 的挂载点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984813121_zh-CN.png)

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155488984813122_zh-CN.png)


NAT 的优点为配置简单。

NAT 的缺点为：

-   安全性方面，由于打通了 EIP 和 VPC，任何获得了 EIP 的人都可以挂载 EIP 对应的挂载点。
-   每个 EIP+PORT 只能映射到一个挂载点，同时访问多个挂载点时需要创建多个EIP。

使用 NAT 与 使用 VPN 的优缺点对比如下：

| |NAT网关方案|VPN网关方案|
|--|-------|-------|
|配置|简单，完全在阿里云控制台完成|复杂，需要在阿里云控制台配置 VPN 网关，还需要在 IDC 或者 Office 配置用户侧 VPN 网关。|
|价格|Small 规格：12元/天，EIP带宽包：3.36元/Mbps/天|5Mbps VPN 网关：375元/月|
|安全性|差|好|
|灵活性|受限，一个 EIP 只能映射到一个 NAS 挂载点。|好，可以同时访问所有的 NAS 挂载点。|
|适合场景|临时，少量数据上传下载。|用户线下环境和阿里云NAS长期的连通。|

