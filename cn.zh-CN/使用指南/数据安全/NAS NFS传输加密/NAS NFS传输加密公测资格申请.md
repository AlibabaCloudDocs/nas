# NAS NFS传输加密公测资格申请 {#task_tmm_4ln_mfb .task}

NAS NFSv4 的传输加密功能已在华北1区的容量型 NAS 产品中开始公测。您可以在 NAS 控制台申请公测资格。

在申请公测资格并使用前，您需要了解以下内容：

-   与非传输加密版本相比，NAS NFS 传输加密版本的延迟及IOPS会有约10%的损耗。
-   NFS 传输加密会在客户端使用 stunnel 进行 TLS 加密代理。对于吞吐型应用，stunnel 会消耗大量 CPU 资源用于加密与解密。在较为极端的场景下，单个挂载点可能会消耗 100% 的 CPU 资源。这种情况下，应用的吞吐也会受到限制。

1.  登录[文件存储控制台](https://nas.console.aliyun.com/)。 
2.   选择区域**华北1**，然后在 NAS NFS 传输加密公测信息右侧单击**申请**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23837/153976409113824_zh-CN.png)

 
3.   在提交申请对话框中，输入**联系方式**、**邮箱地址**、**公司名称**和**使用场景**，然后单击**提交**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23837/153976409113825_zh-CN.png)

 
4.   在控制台首页的 NAS NFS 传输加密公测信息右侧，单击**查询申请状态**。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23837/153976409113826_zh-CN.png)

 
5.  在查询申请状态对话框中查看申请审核是否通过。 如显示如下信息，表示审核已经通过，您可以开始试用 NAS NFS 传输加密功能。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23837/153976409113827_zh-CN.png)


