# Attach NAS to Windows IIS for data {#concept_54986_zh .concept}

This document explains how to use the SMB protocol \(supported by Alibaba Cloud NAS\) and ECS instances in Windows to enable Web and FTP services through Windows built-in Internet Information Service \(IIS\).

## Product implementation {#section_ln2_gzh_hfb .section}

Alibaba Cloud is the only public cloud vendor with a file storage system \(NAS\) that supports both the Network File System \(NFS\) protocol \(NFSv3 and NFSv4\) and the Server Message Block \(SMB\) protocol \(versions 2.0 and later\). To ensure IIS works in conjunction with NAS, the following are recommended:

-   You must use Windows Vista/Windows Server 2008 or any later Windows version. Earlier versions \(such as Windows XP or Windows Server 2003\) are not supported. We strongly recommend using Windows 2008 R2 or later.
-   Prioritize use of an SMB file system so that Windows applications can directly access NAS without needing modification.

With centralized resource storage on a highly reliable, high throughput Alibaba Cloud NAS and SMB share, IIS can access data in Alibaba Cloud NAS as though it were accessing a local file system. This allows for the separation of storage and computing services of websites. Additionally, computing resources and storage resources can be re-sized on demand to meet requirements. Furthermore, Alibaba Cloud’s Server Load Balancer \(SLB\) allows multiple instances to support a website architecture, to improve error tolerance and resilience. The following illustration demonstrates a simple architecture example:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413125_en-US.png)

FTP services provided by IIS are also widely used. Many website administrators remotely manage website content using FTP, and many customers want to transfer and share files between WAN and Alibaba Cloud using the FTP services of Windows instances.

## Basic settings { .section}

Using IIS 7.5 \(Windows Server 2008 R2\) as an example, the following explains how to provide single-node Web and FTP service on Alibaba Cloud through Alibaba Cloud NAS. The installation and deployment of other Windows Server versions \(for example, Windows Server 2008 and Windows Server 2012\) implement a similar setup. For Windows Server 2016, a key difference related to settings are detailed in a following section. Additionally, you can choose to deploy Alibaba Cloud Server Load Balancer to create multi-server-node websites with error tolerance and resilience. For more information, see [What is Server Load Balancer?](../../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#).

**Note:** 

Ensure you take all necessary steps to maintain the security of your data and website services. While Alibaba Cloud strives to maintain the highest data security standards, it is not responsible for protecting against all attacks that may occur. We recommend that you take comprehensive security measures such as setting a firewall and ECS instance security group, and installing updated OS patches as they become available, in order to fully protect your resources.

## Install IIS {#section_nrg_zmb_mfb .section}

Using Windows Server 2008 R2 as an example, the procedure for adding an IIS role and installing the IIS through the server console are illustrated as follows: For a detailed procedure of IIS installation on Windows OS, see Microsoft’s online documentation.

-   Install and deploy of IIS 7
-   Install IIS and ASP.NET module \(Windows Server 2012 and 2012 R2\)

**Note:** For a detailed procedure of IIS installation on Windows OS, see Microsoft’s online documentation

1.  Select the Web Server \(IIS\) role from the server console.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413126_en-US.png)

2.  Select role services for the Web Server. In this example, in addition to basic HTTP functions, FTP services and extensions, ASP services, and other services are selected. They are used for FTP over SSL services and dynamic web page scripts. Then, click **Next**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413127_en-US.png)

3.  Click **Install**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413128_en-US.png)


## Create an SMB file system in NAS {#section_kyz_3nb_mfb .section}

You can centralize the storage of your Web service resources and configuration files on an Alibaba Cloud NAS SMB share. After creating an Alibaba Cloud NAS file system that supports SMB, set the permission group so that the current Web server has read and write access to the corresponding file system of the SMB share. You can use VPC or classic network to connect the NAS file system and the Web server.

After creating an SMB file system, create a directory in the file system’s default share myshare, for example `www`, to store website files. In this and all following examples, a static file index.html and a dynamic ASP script file test.asp are created under myshare\\www. The former displays `Hello World!`, and the latter dynamically acquires and displays the current time.

-   The index.html file is as follows:

    ```language-html
    <HTML>
    
      <HEAD>
    
         <TITLE>Hello World in HTML</TITLE>
    
      </HEAD>
    
      <BODY>
    
         <CENTER><H1>Hello World! </H1></CENTER>
    
      </BODY>
    
    </HTML>
    
    
    ```

-   The test.asp file is as follows:

    ```language-asp
    <HTML>
    
      <BODY>
    
         This page was last refreshed on <%= Now() %>.
    
      </BODY>
    
    </HTML>
    
    
    ```


As illustrated in the following figure, users in the current ECS instance can verify access to the SMB share through Windows File Manager. In this example:

-   \\\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www is the physical path of the website resources.
-   \\\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare is the Alibaba Cloud NAS SMB share that was created in the preceding step.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413129_en-US.png)

For security and management purposes, the user “iis\_user” is added to the system. In the following examples, when provisioning the FTP service or running Windows Server 2016, data access is by this user rather than the administrator.

## Set up IIS Web services { .section}

Open the Basic Settings of the website and go to **Edit Website** \> **Physical path** to input the storage path for website resources on Alibaba Cloud NAS.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413130_en-US.png)

Then, enter the UNC address \\\\32f214a370-pcy74.cn-shanghai.nas.aliyuncs.com\\myshare\\www as the physical path of the website resources.\(ui\) By default, IIS accesses data through user accounts and user groups of IIS applications. If, during the current session, a Windows user maps a network drive \(for example, Z:\), the network drive cannot be directly used, or the system returns an access failure error.

After accessing the files index.html and test.asp at the localhost, or at 127.0.0.1 through a browser, and viewing results similar to the following examples, IIS is ready to provide normal Web services, as shown in the following example:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413131_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413132_en-US.png)

Additionally, a server user can establish an Alibaba Cloud Security Group and a Windows Firewall to limit web access.

## Windows Server 2016 {#section_qxw_gpb_mfb .section}

For Windows Server 2016 users, as Microsoft has made several changes in the product cycle of IIS, you must implement the following two additional settings to make sure that IIS works properly with Alibaba Cloud NAS SMB services.

-   Modify the following registry key of the SMB client to support access to the SMB share as an anonymous user. You can edit the registry by running the Registry Editor \(regedit\).

    HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters\\AllowInsecureGuestAuth

    The procedure is as follows:

    1.  Run the Registry Editor, find

        HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters, and right click to select New\(N\) \> DWORD \(32\) Value\(D\).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413133_en-US.png)

    2.  Edit AllowInsecureGuestAuth, and set the value to 1.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439413134_en-US.png)

-   Specify a local user in the IIS Website Settings to access the website resources on Alibaba Cloud NAS. \(ui\)Specific steps are illustrated in the following figures. You can select Basic Settings of the website, and then set the specified user by clicking **Connect As**. In this example, user "iis\_user" is selected.\(ui\)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513135_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513136_en-US.png)


## Set up IIS FTP services { .section}

To enable users to share files or release website contents through FTP, you must set the FTP over SSL service \(also known as FTP-SSL, S-FTP, or FTP Secure\) through IIS.

-   Install the SSL certificate
    1.  Select **Server Certificate** in the IIS Server section to apply for and manage server certificates.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513137_en-US.png)

    2.  Specify the name of the server certificate.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513138_en-US.png)

    3.  If successful, a certificate displays as follows:

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513139_en-US.png)

-   Setting up FTP sites
    1.  Select **Add FTP Site** in the IIS Website section.

        Similar to Web services, the physical path is the SMB share path in the UNC format. In this example, the www directory of the Web services is used. You can select other directories on myshare based on your needs, or set multiple FTP sites to access different directories through different ports.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513140_en-US.png)

    2.  Bind the IP address that provides the FTP service, and assign a port number.

        For security, this example uses port 2222 rather than the standard port 21, to provide the FTP control information channel. We recommended you select **Require SSL certificate to connect to this FTP site**, and use the SSL certificate previously created.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513141_en-US.png)

    3.  Specify the ID authentication method as **Basic**, and assign the read and write permission to iis\_user. If required, you can select multiple authorized users at this stage.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513142_en-US.png)

    4.  For security, this example limits the port range of the FTP data channel by enabling the server level FTP Firewall Support in IIS console. To do so, click **Apply**, as follows:

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439513143_en-US.png)

    5.  Restart the FTP service in the server console, so that the port range can immediately take effect.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613144_en-US.png)

    6.  For security, this example limits FTP client access by modifying Alibaba Cloud Security Group settings as follows:

        Authorize only one client IP address to access the FTP control and data port range. If needed, you can also authorize multiple IP addresses, or one or more CIDR blocks.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613145_en-US.png)

    7.  The following pictures illustrate how you can access the FTP site through an FTP client WinSCP by selecting FTP over SSL.

        1.  Accept the server certificate. This message appears only when you connect to the FTP site for the first time.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613146_en-US.png)

        2.  Set the protocol type, port number, and login information.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613147_en-US.png)

        3.  Click **Login**. You are prompted to enter a the password of the authorized user on the IIS server.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613148_en-US.png)

        4.  Data connection is established. This may take some time.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613149_en-US.png)

        If successful, the following is displayed, indicating you can upload and download files.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18707/155080439613150_en-US.png)


