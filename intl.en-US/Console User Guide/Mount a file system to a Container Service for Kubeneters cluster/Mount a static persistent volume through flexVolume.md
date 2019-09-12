# Mount a static persistent volume through flexVolume {#task_1780247 .task}

This topic describes how to mount a volume, a static persistent volume \(PV\), or a static persistent volume claim \(PVC\) to access an Apsara File Storage NAS file system from a Container Service for Kubernetes cluster by using the flexVolume driver.

1.  You have created a Kubernetes cluster. For more information, see [Create a Kubernetes cluster](../../../../reseller.en-US//Create a Kubernetes cluster.md#).

    If your cluster is a self-built cluster, download and install [Alibaba Cloud flexVolume driver](https://github.com/AliyunContainerService/flexvolume).

2.  You have created a file system. For more information, see [Create file systems](reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).

    The file system you have created and your Kubernetes cluster must be in the same zone.

3.  You have added a mount point. For more information, see [Create a mount point](reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).

    The mount point and the Kubernetes cluster must be in the same Virtual Private Cloud \(VPC\) network.


With the flexVolume driver provided by Alibaba Cloud, you can access Apsara File Storage NAS file systems by using the following methods:

-   Mount a volume
-   Mount a static PV and PVC

## Mount a volume {#section_zga_c4w_e7t .section}

Use a nas-deploy.yaml file to create pods.

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

|Parameter|Description|
|---------|-----------|
|server|The mount point of your Apsara File Storage NAS file system.|
|path|The mounted directory in your Apsara File Storage NAS file system. You can mount a sub-directory as a volume. If no sub-directory exists in the Apsara File Storage NAS file system, the system automatically creates and then mounts a sub-directory.|
|vers|The version number of Network File System \(NFS\) mount protocol. Version 3 and version 4.0 are supported. The recommended and default version is version 3.|
|mode|The access permission to the mounted directory. **Note:** 

-   You cannot configure the mode parameter if the root directory is mounted.
-   If the Apsara File Storage NAS file system stores a large amount of data, the process of mounting the volume may require a long period of time or fail. In this case, we recommend that you do not configure the mode parameter.

 |
|options|The options for mounting the Apsara File Storage NAS file system. If you do not configure the parameter, the default value is nolock,tcp,noresvport for the V3 protocol, and noresvport for the V4.0 protocol.|

## Mount a static PV and PVC {#section_ttm_d49_hu4 .section}

1.  Create a PV. 

    You can create a PV by using a YAML file or in the Alibaba Cloud Container Service console.

    -   Use a nas-pv.yaml file to create a PV.

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

        For more information about specific parameters, see [Table 1](#table_7je_ozo_c1v).

    -   Use the Alibaba Cloud Container Service console to create a PV:
        1.  Log on to the [Container Service console](https://cs.console.aliyun.com/).
        2.  Choose **Container Service-Kubernetes** \> **Clusters** \> **Persistent Volumes**. Select the target cluster and click **Create**.
        3.  In the Create PV dialog box, set related parameters.

            |Parameter|Description|
            |---------|-----------|
            |PV Type|Select NAS.|
            |Volume Name|The name of the PV. It must be unique in the cluster. In this example, use pv-nas as the name.|
            |Capacity|The capacity of the PV. **Note:** The capacity of the PV cannot exceed the disk capacity.

 |
            |Access Mode|The access mode is ReadWriteMany by default.|
            |Mount Point Domain Name|The mount point of the Apsara File Storage NAS file system. You can set this parameter based on your business requirements following the example of file-system-id.region.nas.aliyuncs.com.|
            |Subpath|The sub-directory of the Apsara File Storage NAS file system. It must start with a forward slash \(/\). After the PV is created, the specified sub-directory is mounted as the PV.             -   If no sub-directory exists in the root directory of an Apsara File Storage NAS file system, the system automatically creates a sub-directory.
            -   You do not need to specify this parameter. By default, the root directory of the NAS file system is mounted.
 |
            |Permissions|The access permission to the mounted directory. For example, you can set this parameter to 755, 644, or 777.             -   The permission can only be set when a sub-directory is mounted as the PV.
            -   You do not need to specify this parameter. The default permission is the original permission of the Apsara File Storage NAS file system.
            -   If the Apsara File Storage NAS file system stores a large amount of data, the process of mounting the volume may require a long period of time or fail. In this case, we recommend that you do not configure this parameter.
 |
            |Version|The version number of Network File System \(NFS\) mount protocol. Version 3 and version 4.0 are supported. The recommended and default version is version 3.|
            |Label|The label of the PV.|

        4.  After you complete the parameter configurations, click **Create**.
2.  Use a nas-pvc.yaml file to create a PVC: 

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

3.  Use a nas-pod.yaml file to create pods as follows: 

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


