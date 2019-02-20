# 本地IDC NAT网络访问阿里云文件存储 {#concept_57628_zh .concept}

阿里云文件存储服务在使用时有一个限制：对于一个地域（比如华东1）内创建的文件系统（NFS或者SMB），只支持同一地域内的ECS挂载，用户在其他地域（比如华北1）内的ECS，或者用户自己IDC机房的服务器，是没法直接挂载的；只有通过建立不同VPC间或者IDC和VPC间的高速通道才能实现跨地域或者从IDC服务器挂载文件系统，而部署高速通道带来的高成本将是很多用户面临的一个非常现实的问题。

之前对于已经在自己机房部署了VPN服务的用户，我们推荐使用阿里云的VPN网关来实现用户办公环境或者IDC到阿里云NAS的互通，具体过程可以参考[本地IDC VPN网络访问阿里云文件存储](cn.zh-CN/最佳实践/远程访问文件系统/本地IDC VPN网络访问阿里云文件存储.md#)。

但是，VPN的部署非常繁琐，而且阿里云VPN目前是按月收费的（每月收费从几百到几千不等），对于一些用户，他们在业务上云过程中，仅仅是想把少量的线下数据上传到阿里云NAS，那么对于这部分用户来说，是不是有更好的方案呢？接下来我们就来介绍一个更简单（而且花费更少）的方案：使用NAT网关实现从公网访问阿里云NAS。

使用NAT网关从公网访问阿里云NAS的网络架构如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669013110_zh-CN.png)

用户需要做的是：

1.  创建NAS文件系统。
2.  为文件系统添加挂载点。
3.  创建NAT网关。
4.  为NAT网关添加带宽包，获得公网IP（EIP）。
5.  为NAT网关添加DNAT转发条目。

通过这五步，用户就可以在任何一台可以连接公网的PC（Windows或Linux）挂载NAS，实现文件的上传和下载。

我们接着来演示一下各步骤：

1.  在NAS控制台创建文件系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669013111_zh-CN.png)

2.  为文件系统添加挂载点，注意需要创建VPC挂载点（NAT只支持VPC）

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669013112_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669013113_zh-CN.png)

3.  获得挂载点的IP（可以在用户的ECS中ping一下挂载点地址获得IP）

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113114_zh-CN.png)

4.  在NAT控制台创建NAT网关 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113115_zh-CN.png)

5.  为NAT网关添加带宽包。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113116_zh-CN.png)

6.  创建DNAT，公网IP会出现第五步中创建的EIP，私网IP填写需要访问的挂载点的IP，端口设置最简单的方式是选择“所有端口”。（也可以安装NFS和SMB协议需要选择相应的端口。）

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113117_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113118_zh-CN.png)

7.  验证挂载NFS，将NAT映射配置到一个NFS的挂载点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113119_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113120_zh-CN.png)

8.  验证挂载SMB，删除原来的NAT映射，添加一条映射配置到一个SMB的挂载点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113121_zh-CN.png)

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18706/155065669113122_zh-CN.png)


到这里可以看出，使用NAT的方案，从配置来说要比使用VPN的方案要简单很多，但使用NAT也有其缺点：

-   安全性方面，由于打通了EIP和VPC，任何获得了EIP的人都可以挂载EIP对应的挂载点。
-   每个EIP+端口只能映射到一个挂载点，用户需要同时访问多个挂载点时需要创建多个EIP。

最后，总结一下两种方案的对比。

| |NAT网关方案|VPN网关方案|
|--|-------|-------|
|配置|简单，完全在阿里云控制台完成|复杂，需要在阿里云控制台配置VPN网关，还需要在IDC或者Office配置用户侧VPN网关。|
|价格|Small规格：12元/天，EIP带宽包：3.36元/Mbps/天|5Mbps VPN 网关：375元/月|
|安全性|差|好|
|灵活性|受限，一个EIP只能映射到一个NAS挂载点|好，可以同时访问所有的NAS挂载点|
|适合场景|临时，少量数据上传下载|用户线下环境和阿里云NAS长期的连通|

