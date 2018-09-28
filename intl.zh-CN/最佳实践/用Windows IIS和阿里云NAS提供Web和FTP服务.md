# 用Windows IIS和阿里云NAS提供Web和FTP服务 {#concept_54986_zh .concept}

阿里云文件存储服务NAS（阿里云NAS）是阿里云在2016年正式推出的公共云上的网络文件系统实现。阿里云NAS主要面向阿里云 ECS 实例、E-HPC、容器服务、弹性Web和BatchCompute 等计算节点提供文件存储服务。通过标准的文件访问协议，用户无需对现有应用做任何修改，即可在云上使用具备无限容量及性能扩展、单一命名空间、多共享、高可靠和高可用等特性的分布式文件系统。阿里云于2016年发布了支持NFS网络文件系统访问协议的阿里云文件系统\(NAS\)。2017年3月，又增加了SMB文件系统访问协议的支持，正式对外公测。

本文介绍如何结合阿里云NAS的SMB协议支持和ECS Windows虚拟机，使用Windows内置的互联网信息服务（IIS）来提供Web和FTP服务。

## 背景和基本信息 {#section_ln2_gzh_hfb .section}

为了丰富文件系统的协议支持和满足客户的兼容性需求，阿里云NAS在今年3月提供SMB（Server Message Block）文件系统访问协议的支持，并开始公测。与NFS相比，SMB文件系统访问协议更加适合于Windows客户端，各个版本的Windows对SMB协议的支持更加完善，绝大多数Windows应用程序不经修改即可通过SMB协议访问阿里云文件存储服务。因此，阿里云建议应用集中运行在ECS Windows实例上的用户优先考虑使用SMB文件系统。阿里云是目前市场上唯一一个全面支持NFS和SMB协议的公共云厂商。阿里云NAS支持SMB 2.0及以上的SMB协议版本，对应支持Windows Vista / Windows Server 2008及以上的各Windows版本，不支持Windows XP / Windows Server 2003及以下的各Windows版本。做出这一选择的主要原因是SMB 1.0与SMB 2.0 及以后的版本相比，由于协议设计的巨大差异在性能和功能的上有严重的不足，同时只支持SMB1.0或更早协议版本的Windows产品都已经完全退出微软支持的生命周期。如果用户创建新Windows实例，我们推荐至少选择Windows 2008 R2以上的版本。

Windows Server目前仍然是非常流行的网站建构平台。到2017年2月止，全球仍然有超过43%站点的Web Server采用微软IIS \(来自Netcraft February 2017 Web Server Survey\)，很多网站和博客系统也是基于内容管理系统例如WordPress、Joomla等和IIS在Windows平台一起实现的。在阿里云现有的用户中，有不少用户选择用阿里云ECS提供的独享Windows虚拟机来提供网站服务。通过将网站内容资源集中存储在一个高可靠，高吞吐，按量付费的阿里云 SMB share上，IIS可以象访问本地文件系统一样访问阿里云NAS上的数据，从而让用户的网站可以实现存储和计算服务的分离，同时计算资源和存储资源都可以支持按需弹性扩容, 通过阿里云提供的负载均衡服务由多个虚拟机来共同承载一个弹性容错的网站架构。一个简单的示意图如下：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013125_zh-CN.png)

IIS提供的FTP服务也同样存在着非常广泛的需求：很多Web站点的管理员通过FTP来远程管理Web站点的内容；同时也有很多客户希望利用Windows虚拟机上的FTP服务在广域网和阿里云之间传输和共享文件。

## 基本设置 { .section}

这里我们以IIS 7.5 \(Windows Server 2008 R2\)的设置为例，来展示如何通过阿里云NAS在阿里云上提供提供单节点的Web和FTP服务。其它Windows服务器版本如Windows Server 2008和Windows Server 2012的安装和部署也类似。对于Windows Server 2016，我们会指出一些需要注意的设置的不同之处。用户可以进一步使用阿里云负载均衡服务来建构多服务器节点的弹性容错的站点。

具体方法请参阅[阿里云负载均衡文档](https://www.alibabacloud.com/zh/product/server-load-balancer?spm=a2c63.p38356.1097650.dznavproductsa3.e0a6fa81VcnPgZ)。

需要着重指出的是，在公网环境里提供Web 和FTP Service的阿里云ECS虚拟机由于服务的开放性容易受到安全攻击。我们在这里给出的设置步骤着重于说明如何在功能上连接Web服务与NAS存储，虽然有安全性的考虑但不能作为完整的安全配置和实现方案。用户需要承担安全方面的所有最终责任，从系统级别（如设置防火墙、ECS实例安全组和及时安装操作系统补丁）和服务级别（如使用阿里云的各个安全产品）来全面保障自己网站服务和数据的安全性。

-   IIS安装：

    以Windows Server 2008 R2为例，通过服务器管理器添加IIS角色并安装IIS的过程如下面几张图所示。在不同Windows操作系统上安装IIS的详细过程请参阅下面的微软在线文档：

    IIS 7的安装和部署

    安装 IIS 和 ASP.NET 模块（Windows Server 2012 和2012 R2）

    1.  用户在服务器管理器中选择添加Web服务器（IIS）角色。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013126_zh-CN.png)

    2.  用户选择为Web服务器安装的角色服务，处理基本的HTTP功能以外，我们还包括了FTP服务及扩展，ASP服务等，用于后面提供FTP over SSL服务和演示动态网页脚本的使用。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013127_zh-CN.png)

    3.  用户选择安装，下面是安装完成的提示界面。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013128_zh-CN.png)

-   NAS SMB文件系统的创建和设置：

    用户的Web服务资源及配置文件可以集中存储在阿里云NAS的一个SMB share上。在创建了一个支持SMB的阿里云NAS文件系统之后，用户通过设置权限组来保证当前Web服务器可以读写访问SMB share对应的文件系统。用户可以使用VPC或者经典网络来连接NAS文件系统和Web服务器。创建和使用阿里云NAS SMB文件系统的具体步骤请参考阿里云博客[《阿里云文件存储SMB协议服务及其申请和使用指南》](https://yq.aliyun.com/articles/88298?spm=5176.100239.blogcont92854.23.RxId43)。

    在创建SMB 文件系统之后，用户可以在文件系统的缺省share “myshare”下面进一步创建目录如www来存储网站文件。我们在myshare\\www下创建两个简单的文件并在后面以它们为例来说明整个操作流程：静态网页index.html和动态ASP脚本test.asp。前者显示“Hello World！”，后者动态获取并显示当前时间。

    Index.html

    ```language-html
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

    ```language-asp
    <HTML>
    
      <BODY>
    
         This page was last refreshed on <%= Now() %>.
    
      </BODY>
    
    </HTML>
    
    
    ```

    如下图所示，当前的ECS虚拟机用户可以通过Windows文件管理器来验证对SMB share的访问。在我们的例子中，\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www是网站资源的物理路径，其中\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare是我们创建的阿里云NAS SMB share。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013129_zh-CN.png)

    出于安全和管理的考虑，我们在系统里还加入了一个新用户“iis\_user”。在后面的例子中，在提供FTP服务或者在Windows Server2016上运行时，我们选择通过该用户而不是系统管理员来进行数据访问。


## 三、IIS Web服务的设置 { .section}

如下图所示，Windows Server2008 R2的用户打开网站的“基本设置”，并在“编辑网站”的交互窗口中将“物理路径”设置为网站资源在阿里云NAS上的存储路径。继续前面的例子，我们输入UNC地址\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www作为网站资源的物理路径。这一点需要格外注意：由于IIS缺省通过IIS的应用程序账号和用户组访问，Windows桌面用户在当前user session中映射的网络驱动器如（Z:\\）是不可直接使用的，否则会出现访问失败的错误。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013130_zh-CN.png)

通过用本地浏览器访问localhost或者127.0.0.1的index.html和test.asp，我们可以确认IIS现在已经可以正常进行Web服务了。服务器用户可以进一步设置阿里云安全组和Windows防火墙来进行Web访问安全的限制。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359013131_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113132_zh-CN.png)

对于Windows Server 2016的用户来说，由于微软在该产品周期做的几个改动，目前需要通过以下的两个额外设置来让IIS和阿里云NAS的SMB服务正确协同工作。

1.Â 用户需要改动SMB client的一个注册表项来支持对SMB share的匿名访问。如下图所示，用户需要运行注册表编辑器regedit来修改下面的注册表值。

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\AllowInsecureGuestAuth

具体来说，在用户打开注册表编辑器之后，需要找到HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters， 然后用右键选取新建DWORD\(32位\)值。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113133_zh-CN.png)

用户接着创建并编辑该值AllowInsecureGuestAuth并将其设置为1。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113134_zh-CN.png)

除了注册表项外，用户还需要在IIS的网站设置中指定一个本地用户来访问网站在阿里云NAS上的资源。具体的步骤如下面两图所示，用户选取网站的基本设置，再通过“连接为”设置特定用户，这里我们选用前面设置的用户“iis\_user”。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113135_zh-CN.png)

另外，由于IIS使用SMB share的方式下访问一个文件时，IIS后台会有很多次访问SMB share操作，每次访问的时间不长，但是多次的叠加可能会造成客户端总时间比较长。改进的方式可以参考：https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200\(v=ws.10\) 将其中提到的三个注册表项都调大，比如600， 或者更大。需要注意的是这些注册表项都在注册表\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\LanmanWorkstation\\Parameters\]之下，分别是

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

除此之外，建议把js/css等网页程序相关的内容放在本地，因为IIS会非常频繁访问。

## IIS FTP服务的设置 { .section}

很多IIS用户希望用FTP来共享文件或进行网站内容发布。在这里我们介绍如何通过IIS设置FTP over SSL服务 （又名FTP-SSL, S-FTP， FTP Secure）。

-   安装SSL证书
    1.  用户 在IIS的服务器部分选择“服务器证书”，申请和管理服务器证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113137_zh-CN.png)

    2.  用户指定服务器证书的名称。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113138_zh-CN.png)

    3.  配置和创建成功SSL证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113139_zh-CN.png)

-   FTP站点设置
    1.  用户在IIS的网站部分选择“添加FTP站点”，和Web服务一样，物理路径需要使用UNC格式的SMB share路径。在这个例子里，我们仍使用前面用过的Web service的www目录。用户可以根据需要选取myshare上其它目录，也可以通过设置多个FTP站点利用不同的端口来提供对不同目录的访问。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113140_zh-CN.png)

    2.  用户绑定提供FTP服务的IP地址，并分配端口号。这个例子里，我们出于安全的考虑没有使用标准的21端口而是用2222端口来提供FTP的控制信息通道。需要格外注意的是，我们选择需要SSL证书才能连接这个FTP站点，并指定使用前面创建的SSL证书。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113141_zh-CN.png)

    3.  用户指定身份验证方式为“基本”，并且将读写权限提供给用户iis\_user。如果需要的话，这里也可以选取更多的授权用户。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113142_zh-CN.png)

    4.  出于安全考虑，用户可以如下图所示，在通过在IIS中打开服务器级别“FTP防火墙支持”来限制FTP数据通道的端口范围，并选取“应用”。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359113143_zh-CN.png)

    5.  在这之后，为了该端口范围立即生效，需要在服务器管理器中重启FTP服务。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213144_zh-CN.png)

    6.  出于安全考虑，建议用户通过阿里云的安全组设置来限制FTP客户端的访问。在下面的例子里，我们将已经设置的FTP控制及数据端口范围只授权给一个客户端IP访问。需要的话用户也可以授权给多个IP或者一个多个网段。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213145_zh-CN.png)

    7.  下面几张图展示了通过FTP客户端WinSCP利用FTP over SSL来访问我们的FTP站点的过程。

        接受服务器证书，只在客户端第一次连接FTP站点才发生。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213146_zh-CN.png)

        设置协议类型，端口号和登录信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213147_zh-CN.png)

        登录后要求输入密码，即授权用户所在IIS服务器上的密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213148_zh-CN.png)

        数据连接建立，服务器读取和传输远程目录信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213149_zh-CN.png)

        用户完成初步连接，可以进行文件的上传下载。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/153814359213150_zh-CN.png)


## 五、总结 { .section}

本文通过例子介绍了如何结合阿里云NAS的SMB协议支持和ECS Windows虚拟机，使用Windows内置的互联网信息服务（IIS）来提供Web和FTP服务。阿里云NAS服务还在不断发展和演进中，后续会提供更好的协议服务和性能支持。

