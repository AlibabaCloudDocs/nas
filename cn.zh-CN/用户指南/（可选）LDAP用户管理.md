# （可选）LDAP用户管理 {#concept_cxp_3w2_2hb .task}

文件存储CPFS支持配置企业自建的LDAP服务，来控制CPFS文件系统的用户访问。

LDAP为轻量目录访问协议（Lightweight Directory Access Protocol），用来提供目录服务。

**说明：** 

-   不接入LDAP时，CPFS只允许root用户访问文件系统，其他用户访问时将返回permission denied错误。
-   接入LDAP时，您需要提供LADP服务器并确保LDAP服务的连通性。
    1.  确保LDAP服务器与CPFS文件系统所在的VPC连通。
    2.  确保LDAP的服务端口（默认为389端口）可连通。

1.  登录[NAS控制台](https://nas.console.aliyun.com/)。
2.  选择**CPFS** \> **文件系统列表**。
3.  找到目标文件系统，单击**管理**。
4.  在文件系统详情页面，单击**添加LDAP**。 

    您需要提供**URI**、**Bind DN**和**Search Base**等信息。

    ![添加LADP](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/148019/156635016841332_zh-CN.png)


