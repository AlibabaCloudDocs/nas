# Nginx 代理服务器阿里云文件存储 NAS {#concept_y2t_qmf_xgb .task}

本文介绍如何通过Nginx 代理服务器代理阿里云文件存储 NAS。

Nginx 是一个很强大的高性能 Web 和 反向代理服务，它具有很多非常优越的特性。反向代理是 Nginx一种最常见的应用模式。 反向代理（Reverse Proxy）是指以代理服务器来接受 internet 上的连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给 internet 上请求连接的客户端，此时代理服务器对外就表现为一个反向代理服务器。

简单来说就是真实的服务器不能直接被外部网络访问，需要一台代理服务器，而代理服务器能被外部网络访问的同时又跟真实服务器在同一个网络环境。或者真实服务器与代理服务器是同一台服务器但端口不同。

## 配置 NAS 做反向代理共享存储 {#section_rhv_cnf_xgb .section}

1 台 Nginx 做反向代理，4 台 Nginx 做代理服务器，后端使用文件共享存储 NAS。文件共享存储 NAS 用于存储 Proxy 代理服务器的缓存文件、镜像回源文件或者用户上传的静态数据文件，不同 Proxy 代理服务器间共享访问 NAS 数据，实现数据同步，避免由于数据不同步导致的数据不一致或者重复镜像回源而浪费带宽。配置组网如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/156706378939582_zh-CN.png)

1.  部署 Nginx 反向代理服务器。 
    1.  安装 Nginx。 

        ``` {#codeblock_pj1_31y_kr3}
        [root@Reverse proxy~]#yum install nginx
        ```

    2.  执行如下命令配置反向代理。 

        配置反向代理服务器指向后端代理服务器。

        ``` {#codeblock_0cz_g32_ppn}
        vim /etc/nginx/nginx.conf
        ```

        在nginx.conf中配置如下信息。

        ``` {#codeblock_34c_bh0_1a9}
        http {
        upstream web{
                 server 192.168.0.105;
                 server 192.168.0.106;
                 server 192.168.0.107;
                 server 192.168.0.108;
              }
              server {
                  listen 80;
                      location / {
                           proxy_pass http://web;
                       }
              }
        }
        ```

2.  创建文件存储 NAS。 
    1.  创建对应区域的文件系统，详情请参见[创建文件系统](../../../../cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
    2.  为文件存储添加挂载点，详情请参见[添加挂载点](../../../../cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。

## 部署 Nginx 代理服务器 {#section_z2r_mrf_xgb .section}

1.  执行以下命令安装 Nginx、NFS客户端。 

    ``` {#codeblock_d6v_jtw_2pg}
    yum install nginx
    yum install nfs-utils
    ```

2.  执行以下命令挂载文件共享存储 NAS 到 Nginx 网站目录。 

    ``` {#codeblock_l2c_iqx_3ol}
    sudo mount -t nfs -o vers=4.0,挂载点域名:/ /usr/share/nginx/html/ 
    ```

3.  编辑 Nginx 主目录文件。 

    ``` {#codeblock_2hc_oy8_ei0}
    echo “This is Testing for Nginx&NAS”> /usr/share/nginx/html/index.html
    ```

4.  重复以上步骤，配置另外三台 Nginx 代理服务器，均挂载同一个 NAS 文件系统，所有 Nginx 代理服务器都可以访问 index.html 测试文件。

## 测试配置结果 {#section_efv_vrf_xgb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/156706379039589_zh-CN.png)

