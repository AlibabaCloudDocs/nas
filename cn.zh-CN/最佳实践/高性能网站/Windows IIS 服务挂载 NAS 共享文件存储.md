# Windows IIS 服务挂载 NAS 共享文件存储 {#concept_54986_zh .concept}

本文介绍如何结合阿里云 NAS 的 SMB 协议支持 ECS Windows 虚拟机，使用 Windows 内置的互联网信息服务（IIS）来提供 Web 和 FTP 服务。

阿里云文件存储服务 NAS 主要面向阿里云 ECS 实例、E-HPC、容器服务、弹性 Web 和 BatchCompute 等计算节点提供文件存储服务。通过标准的文件访问协议 NFS 和 SMB，用户无需对现有应用做任何修改即可在云上使用。

## 背景和基本信息 {#section_ln2_gzh_hfb .section}

与 NFS 相比，SMB 文件系统访问协议更加适合于 Windows 客户端。各个版本的 Windows 对 SMB 协议都能很好的支持，绝大多数 Windows 应用程序不经修改即可通过 SMB 协议访问阿里云文件存储服务。因此，阿里云建议应用集中运行在 ECS Windows 实例上的用户优先考虑使用 SMB 文件系统。

阿里云是目前市场上唯一一个全面支持 NFS 和 SMB 协议的公共云厂商。阿里云 NAS 支持 SMB 2.1 及以上的 SMB 协议版本，支持 Windows 7 / Windows Server 2008 R2 及以上的各 Windows 版本，不支持 Windows Vista / Windows Server 2008 及以下的各 Windows 版本。与 SMB 2.1 及以后的版本相比，SMB 1.0 协议设计的巨大差异在性能和功能的上有严重的不足，同时只支持 SMB 1.0 或更早协议版本的 Windows 产品都已经完全退出微软支持的生命周期。如果用户创建新Windows 实例，建议至少选择 Windows 2008 R2 以上的版本。

Windows Server 目前仍然是非常流行的网站建构平台。到2017年2月止，全球仍然有超过43%站点的 Web Server 采用微软 IIS （来自 Netcraft February 2017 Web Server Survey ），很多网站和博客系统也是基于内容管理系统例如WordPress、Joomla 等在 Windows 平台得以实现。在阿里云现有的用户中，有不少用户选择用阿里云 ECS 提供的独享 Windows 虚拟机来提供网站服务。通过将网站内容资源集中存储在一个高可靠、高吞吐、按量付费的阿里云 SMB share 上，IIS 可以像访问本地文件系统一样访问阿里云 NAS 上的数据，从而让用户的网站可以实现存储和计算服务的分离。此外，计算资源和存储资源都可以支持按需弹性扩容，通过阿里云提供的负载均衡服务由多个虚拟机来共同承载一个弹性容错的网站架构。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650832845_zh-CN.png)

IIS 提供的 FTP 服务也同样有着非常广泛的需求。例如，很多 Web 站点的管理员通过 FTP 来远程管理 Web 站点的内容，同时还有很多用户希望利用 Windows 虚拟机上的 FTP 服务在广域网和阿里云之间传输和共享文件。

## 基本设置 {#section_w55_umd_hzn .section}

我们以 IIS 7.5 （Windows Server 2008 R2）的设置为例，展示如何通过阿里云 NAS 在阿里云上提供提供单节点的 Web 和 FTP 服务。其它 Windows 服务器版本如 Windows Server 2012 的安装和部署也类似。用户可以进一步使用阿里云负载均衡服务来建构多服务器节点的弹性容错的站点。

具体方法请参阅[阿里云负载均衡文档](https://www.alibabacloud.com/zh/product/server-load-balancer?spm=a2c63.p38356.1097650.dznavproductsa3.e0a6fa81VcnPgZ)。

在公网环境里提供 Web 和 FTP Service 的阿里云 ECS 虚拟机由于服务的开放性容易受到安全攻击。本文档的设置步骤着重说明如何在功能上连接 Web 服务与 NAS 存储，提出某些安全性的考虑，但不能作为完整的安全配置和实现方案。用户需要承担安全方面的所有最终责任，从系统级别（如设置防火墙、ECS 实例安全组和及时安装操作系统补丁）和服务级别（如使用阿里云的各个安全产品）来全面保障自己网站服务和数据的安全性。

-   IIS 安装：

    以 Windows Server 2008 R2 为例，通过服务器管理器添加 IIS 角色并安装 IIS 的过程如下图所示。在不同Windows 操作系统上安装 IIS 的详细过程请参阅下面的微软在线文档：

    IIS 7 的安装和部署

    安装 IIS 和 ASP.NET 模块（Windows Server 2012 和 Windows Server 2012 R2）

    1.  用户在服务器管理器中选择添加 Web 服务器（IIS）角色。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650832850_zh-CN.png)

    2.  用户选择为 Web 服务器安装的角色服务，除基本的 HTTP 功能以外，我们还包括了 FTP 服务及扩展、ASP 服务等，用于 FTP over SSL 服务和演示动态网页脚本的使用。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650832851_zh-CN.png)

    3.  单击**安装**，以下是安装成功的提示界面。 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650832852_zh-CN.png)
-   NAS SMB 文件系统的创建和设置：

    您的 Web 服务资源及配置文件可以集中存储在阿里云 NAS 的一个 SMB share 上。创建了一个支持 SMB 的阿里云 NAS 文件系统之后，通过设置权限组来保证当前 Web 服务器可以读写访问 SMB share 对应的文件系统。您可以使用 VPC 或者经典网络来连接 NAS 文件系统和 Web 服务器。创建和使用阿里云 NAS SMB 文件系统的具体步骤请参考阿里云博客[《阿里云文件存储 SMB 协议服务及其申请和使用指南》](https://yq.aliyun.com/articles/88298?spm=5176.100239.blogcont92854.23.RxId43)。

    创建 SMB 文件系统后，您可以在文件系统的**缺省 share** \> **myshare**下创建目录 www 来存储网站文件。本示例中，在 myshare\\www 下创建两个文件来说明静态网页 index.html 和动态 ASP 脚本 test.asp 的操作流程。前者显示`Hello World！`，后者动态获取并显示当前时间。

    Index.html

    ``` {#codeblock_lkm_ssi_dp1 .language-html}
    <HTML>
    
      <HEAD>
    
         <TITLE>Hello World in HTML</TITLE>
    
      </HEAD>
    
      <BODY>
    
         <CENTER><H1>Hello World!</H1></CENTER>
    
      </BODY>
    
    </HTML>
    
    					
    ```

    Test.asp

    ``` {#codeblock_oty_ysz_0w7 .language-asp}
    <HTML>
    
      <BODY>
    
         This page was last refreshed on <%= Now() %>.
    
      </BODY>
    
    </HTML>
    
    					
    ```

    如下图所示，当前的 ECS 虚拟机用户可以通过 Windows 文件管理器来验证对 SMB share 的访问。在本示例中，\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www是网站资源的物理路径，其中\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare为阿里云NAS SMB share。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913129_zh-CN.png)

    出于安全和管理的考虑，我们在系统里还加入了一个新用户 iis\_user。在提供 FTP 服务或者在 Windows Server2016 上运行时，我们选择通过该用户而不是系统管理员来进行数据访问。


## IIS Web 服务的设置 {#section_b2b_jd1_zwn .section}

如下图所示，Windows Server2008 R2 的用户打开网站的**基本设置**，并在编辑网站的交互窗口中将**物理路径**设置为网站资源在阿里云 NAS 上的存储路径。这里我们输入 UNC 地址\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www作为网站资源的物理路径。

**说明：** 由于 IIS 缺省通过 IIS 的应用程序账号和用户组访问，Windows 桌面用户不可直接使用在当前 user session 中映射的网络驱动器如（Z:\\），否则会出现访问失败的错误。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913130_zh-CN.png)

通过用本地浏览器访问 localhost 或者 127.0.0.1 的 index.html 和 test.asp，我们可以确认 IIS 现在已经可以正常进行 Web 服务了。服务器用户可以进一步设置阿里云安全组和 Windows 防火墙来进行 Web 访问安全的限制。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650932842_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650932843_zh-CN.png)

对于Windows Server 2016 的用户来说，由于微软在该产品周期做的几个改动，目前需要通过以下的两个额外设置来让 IIS 和阿里云 NAS 的 SMB 服务正确协同工作。

A 用户需要改动 SMB client 的一个注册表项来支持对 SMB share 的匿名访问。如下图所示，用户需要运行注册表编辑器 regedit 来修改下面的注册表值。

``` {#codeblock_3c6_4ma_dc8}
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\AllowInsecureGuestAuth
```

用户打开注册表编辑器之后需要找到HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters， 然后用右键选取新建DWORD（32 位）值。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913133_zh-CN.png)

创建并编辑该值 AllowInsecureGuestAuth 并将其设置为 1。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913134_zh-CN.png)

除了注册表项外，用户还需要在 IIS 的网站设置中指定一个本地用户来访问网站在阿里云 NAS 上的资源。具体的步骤如下面两图所示，用户选取网站的基本设置，再通过**连接为**设置**特定用户**，这里选用前面设置的用户 iis\_user。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913135_zh-CN.png)

另外，由于 IIS 使用 SMB share 的方式下访问一个文件时，IIS 后台会有多次访问 SMB share 操作，每次访问的时间不长，但是多次的叠加可能会造成客户端总时间比较长。改进的方式可以参考[SMB2 文档](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200(v=ws.10))将其中提到的三个注册表项都调大，比如600或者更大。需要注意的是这些注册表项都在注册表HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\LanmanWorkstation\\Parameters之下，分别为：

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

**说明：** 如果找不到以上三个注册表项，则按照 Windows 的字段格式要求进行创建。

除此之外，建议把 js/css 等网页程序相关的内容放在本地，因为 IIS 访问会非常频繁。

## IIS FTP 服务的设置 {#section_1hw_ye6_en3 .section}

很多 IIS 用户希望用 FTP 来共享文件或进行网站内容发布。在这里我们介绍如何通过 IIS 设置 FTP over SSL 服务 （又名 FTP-SSL，S-FTP， FTP Secure）。

-   安装 SSL 证书
    1.  用户在 IIS 的服务器中选择**服务器证书**，申请和管理服务器证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913137_zh-CN.png)

    2.  用户指定服务器证书的名称。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913138_zh-CN.png)

    3.  配置和创建 SSL 证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913139_zh-CN.png)

-   FTP 站点设置
    1.  用户在 IIS 的网站部分选择**添加FTP站点**，和 Web 服务一样，物理路径需要使用 UNC 格式的 SMB share 路径。示例中，我们仍使用前面用过的 Web service 的 www 目录。用户可以根据需要选取 myshare 上其它目录，也可以通过设置多个 FTP 站点利用不同的端口来提供对不同目录的访问。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913140_zh-CN.png)

    2.  用户绑定提供 FTP 服务的 IP 地址，并分配端口号。这个例子里，我们出于安全的考虑没有使用标准的21端口而是用2222端口来提供 FTP 的控制信息通道。需要格外注意的是，我们选择需要 SSL 证书才能连接这个 FTP 站点，并指定使用前面创建的 SSL 证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913141_zh-CN.png)

    3.  用户指定身份验证方式为**基本**，并授权用户 iis\_user 读写权限。您也可以选取更多的授权用户。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961650913142_zh-CN.png)

    4.  出于安全考虑，通过在IIS中打开服务器级别**FTP 防火墙支持**来限制 FTP 数据通道的端口范围，并选取**应用**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013143_zh-CN.png)

    5.  为了使该端口范围立即生效，需要在服务器管理器中重启 FTP 服务。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013144_zh-CN.png)

    6.  出于安全考虑，建议用户通过阿里云的安全组设置来限制 FTP 客户端的访问。在下面的例子里，我们将已经设置的 FTP 控制及数据端口范围只授权给一个客户端 IP 访问。您也可以授权给多个 IP、一个或多个网段。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013145_zh-CN.png)

    7.  下面几张图展示了通过FTP客户端 WinSCP 利用 FTP over SSL 来访问我们的 FTP 站点的过程。

        接受服务器证书，只在客户端第一次连接 FTP 站点才发生。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013146_zh-CN.png)

        设置协议类型，端口号和登录信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013147_zh-CN.png)

        登录后要求输入密码，即授权用户所在 IIS 服务器上的密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013148_zh-CN.png)

        数据连接建立，服务器读取和传输远程目录信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013149_zh-CN.png)

        用户完成初步连接，可以进行文件的上传下载。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155961651013150_zh-CN.png)


## 总结 {#section_s3l_pe4_i81 .section}

本文通过例子介绍了如何结合阿里云 NAS 的 SMB 协议支持 ECS Windows 虚拟机，使用 Windows 内置的互联网信息服务（IIS）来提供 Web 和 FTP 服务。阿里云 NAS 服务还在不断发展和演进中，后续会提供更好的协议服务和性能支持。

