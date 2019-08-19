# 通过Flexvolume驱动-静态NAS存储卷挂载文件系统 {#task_1780247 .task}

本文介绍如何通过Flexvolume驱动-静态NAS存储卷方式实现在容器服务Kubernetes集群中使用阿里云NAS数据卷。

1.  已创建Kubernetes集群，详情请参见[创建Kubernetes 集群](../../../../cn.zh-CN/Kubernetes集群用户指南/集群管理/创建集群/创建Kubernetes 集群.md#)。
2.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
3.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。

**说明：** 

-   文件系统与Kubernetes集群所属同一个可用区。
-   文件系统与Kubernetes集群所属同一个VPC。

您可以通过阿里云提供的flexvolume插件使用阿里云NAS文件存储服务，可通过以下两种方式：

-   通过volume方式使用阿里云NAS数据卷
-   使用PV/PVC方式使用阿里云NAS数据卷

## 通过volume方式使用阿里云NAS数据卷 {#section_zga_c4w_e7t .section}

使用nas-deploy.yaml文件创建Pod。

``` {#codeblock_00t_sm9_mmp}
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nas-static
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
        volumeMounts:
          - name: nas1
            mountPath: "/data"
      volumes:
      - name: "nas1"
        flexVolume:
          driver: "alicloud/nas"
          options:
            server: "0cd8b4a576-grs79.cn-hangzhou.nas.aliyuncs.com"
            path: "/k8s"
            vers: "3"
            options: "nolock,tcp,noresvport"
```

|参数|说明|
|--|--|
|server|NAS数据盘的挂载点。|
|path|连接NAS数据卷的挂载目录，支持挂载NAS子目录，且当子目录不存在时，会自动创建子目录并挂载。 极速型NAS的Path时，需要以 /share开头。

 |
|vers|定义NFS挂载协议的版本号，支持3和4.0，默认且推荐使用版本3。|
|mode|定义挂载目录的访问权限。 **说明：** 

-   挂载NAS数据盘根目录时不能配置挂载权限。
-   当NAS盘中数据量很大时，不建议配置mode，会导致执行挂载非常慢，甚至挂载失败。

 |
|options|定义挂载参数。不配置此参数时，v3版本的默认挂载选项为nolock,tcp,noresvport，v4.0版本的默认挂载选项为noresvport。|

## 通过PV/PVC方式使用阿里云NAS数据卷 {#section_ttm_d49_hu4 .section}

1.  创建PV。 

    您可以使用yaml文件或者通过阿里云容器服务控制台创建NAS数据卷。

    -   使用nas-pv.yaml文件创建PV。

        ``` {#codeblock_yom_17l_mtm}
        apiVersion: v1
        kind: PersistentVolume
        metadata:
          name: pv-nas
        spec:
          capacity:
            storage: 5Gi
          storageClassName: nas
          accessModes:
            - ReadWriteMany
          flexVolume:
            driver: "alicloud/nas"
            options:
              server: "0cd8b4a576-uih75.cn-hangzhou.nas.aliyuncs.com"
              path: "/k8s"
              vers: "3"
              options: "nolock,tcp,noresvport"
        ```

        重要参数说明请参见[表 1](#table_7je_ozo_c1v)。

    -   通过容器控制台创建NAS数据卷
        1.  登录[容器服务管理控制台](https://cs.console.aliyun.com/)。
        2.  选择**容器服务 - Kubernetes** \> **集群** \> **存储卷**，选择目标集群，单击**创建**。
        3.  在创建存储卷对话框中，配置存储卷的相关参数。

            ![创建存储卷](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1410108/156620729656299_zh-CN.png)

            |参数|说明|
            |--|--|
            |存储卷类型|选择NAS。|
            |数据卷名|创建的数据卷的名称，数据卷名在集群内必须唯一。本例以pv-nas为例。|
            |总量|所创建存储卷的容量。 **说明：** 所创建的存储卷容量不能超过磁盘容量。

 |
            |访问模式|默认为ReadWriteMany。|
            |挂载点域名|NAS文件系统挂载点的挂载地址，例如：file-system-id.region.nas.aliyuncs.com，请根据实际值替换。|
            |子目录|NAS路径下的子目录，以 / 开头。设定后，数据卷将挂载到指定的子目录。             -   如果 NAS 根目录下没有此子目录，会默认创建后再挂载。
            -   您可以不填此项，默认挂载到NAS根目录。
            -   极速NAS需要以/share开头。
 |
            |权限|设置挂载目录的访问权限，例如：755、644、777 等。             -   只有挂载到NAS子目录时才能设置权限，挂载到根目录时不能设置。
            -   您可以不填此项，默认权限为NAS文件原来的权限。
            -   当NAS盘中数据量很大时，不建议配置此参数，会导致执行挂载非常慢，甚至挂载失败。
 |
            |版本|NFS挂载协议的版本号，支持3和4.0，默认且推荐使用版本3。|
            |标签|为该存储卷添加标签。|

        4.  完成配置后，单击**创建**。
2.  使用nas-pvc.yaml文件创建PVC。 

    ``` {#codeblock_5fq_kil_fh2}
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-nas
    spec:
      accessModes:
        - ReadWriteMany
      storageClassName: nas
      resources:
        requests:
          storage: 5Gi
    ```

3.  使用nas-pod.yaml文件创建Pod。 

    ``` {#codeblock_2df_quw_mr0}
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nas-static
      labels:
        app: nginx
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx
            ports:
            - containerPort: 80
            volumeMounts:
              - name: pvc-nas
                mountPath: "/data"
          volumes:
            - name: pvc-nas
              persistentVolumeClaim:
                claimName: pvc-nas
    ```


