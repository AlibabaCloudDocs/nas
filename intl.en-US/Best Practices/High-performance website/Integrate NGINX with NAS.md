# Integrate NGINX with NAS {#concept_y2t_qmf_xgb .concept}

## Scenarios {#section_k4t_54f_xgb .section}

NGINX is a powerful high-performance Web server, which can be used as a reverse proxy. It has many excellent features. NGINX is a popular reverse proxy. A proxy server is a go‑between or intermediary server that forwards requests for information from multiple clients to different servers across the Internet. A reverse proxy server is a type of proxy server that typically sits behind the firewall in a private network and directs client requests to the appropriate backend server.

Assume that a server is located in a private network cannot be accessed by external networks. In this case, a proxy server is required as an intermediary server, which is located in the same private network as the server and can be accessed by external networks. A server can be both an application server and a proxy server but uses separate ports.

## Configure NAS as a reverse proxy to share storage {#section_rhv_cnf_xgb .section}

Configure one NGINX client as a reverse proxy and four NGINX clients as proxy servers. These clients use shared file storage provided by NAS in the background. You can use NAS to store multiple types of proxy server files, such as cache files, back-to-origin files, and static data files uploaded by users. Several proxy servers share access to NAS data to synchronize data. This prevents data inconsistency and frequent back-to-origin requests from occurring because data is not synchronized. The configuration is shown in the following figure:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/155374849239582_en-US.png)

-   Deploy an NGINX reverse proxy
    1.  Install NGINX

        ```
        [root@Reverse proxy~]#yum install nginx
        ```

    2.  Configure a reverse proxy

        Configure a reverse proxy and associate it with a backend proxy server

        ```
        [root@Reverse proxy~]#vim /etc/nginx/nginx.conf
        ```

        ` `

        You can configure NGINX as follows:

        ```
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

-   Create a NAS file system
    1.  Create a file system for the corresponding region

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/155374849239585_en-US.png)

    2.  Create a NAS mount point

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/155374849239587_en-US.png)

    3.  The newly created NAS mount point is for future use.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/155374849239588_en-US.png)


## Deploy NGINX proxy servers {#section_z2r_mrf_xgb .section}

You can deploy an NGINX proxy server as follows:

1.  Install NGINX and NFS clients

    ```
    [root@proxy~]#yum install nginx
    [root@proxy~]#yum install nfs-utils
    ```

2.  Mount a shared file storage on the web directory of NGINX

    ```
    [root@proxy~]#sudo mount -t nfs -o vers=4.0, <the domain name of the mount point>:/ /usr/share/nginx/html/ 
    ```

3.  Modify the file of the NGINX main directory

    ```
    [root@proxy~]#echo “This is Testing for Nginx&NAS”> /usr/share/nginx/html/index.html
    ```


Repeat the preceding procedure for the other three NGINX proxy servers and mount the same NAS file system. At this point, all Nginx proxy servers can access the index.html test file.

## Testing results {#section_efv_vrf_xgb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/131493/155374849239589_en-US.png)

