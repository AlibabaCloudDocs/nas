# Mount a dynamic persistent volume to access Apsara File Storage NAS through flexVolume {#task_1780353 .task}

This topic describes how to mount a dynamic persistent volume \(PV\) to access an Apsara File Storage NAS file system from a Container Service for Kubernetes cluster by using the flexVolume driver.

1.  You have created a Kubernetes cluster in Alibaba Cloud. For more information, see [Create a Kubernetes cluster](../../../../reseller.en-US//Create a Kubernetes cluster.md#).

    If your cluster is a self-built Kubernetes cluster, download and install [Alibaba Cloud flexVolume driver](https://github.com/AliyunContainerService/flexvolume).

2.  You have created a file system. For more information, see [Create file systems](reseller.en-US/Console User Guide/Manage file systems.md#section_5jo_0kj_jn5).

    The file system and the Kubernetes cluster must be in the same zone.

3.  You have added a mount point. For more information, see [Create a mount point](reseller.en-US/Console User Guide/Manage mount points.md#section_6xi_a3u_zkq).

    The mount point and the Kubernetes cluster must be in the same Virtual Private Cloud \(VPC\) network.


A dynamic PV is dynamically provisioned based on the mapping from a sub-directory in an Apsara File Storage NAS file system.

**Note:** When you use dynamic provisioning, a directory is automatically created in an existing NAS file system and mounted as the target volume.

## Install the NAS controller {#section_2hv_yu7_erq .section}

Configure a deployment named alicloud-nas-controller by using the following template.

``` {#codeblock_842_fcf_7kx}
kind: Deployment
apiVersion: extensions/v1beta1
metadata:
  name: alicloud-nas-controller
  namespace: kube-system
spec:
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: alicloud-nas-controller
    spec:
      tolerations:
      - operator: "Exists"
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 1
            preference:
              matchExpressions:
              - key: node-role.kubernetes.io/master
                operator: Exists
      priorityClassName: system-node-critical
      serviceAccount: admin
      hostNetwork: true
      containers:
        - name: nfs-provisioner
          image: registry.cn-hangzhou.aliyuncs.com/acs/alicloud-nas-controller:v1.14.3.8-58bf821-aliyun
          env:
          - name: PROVISIONER_NAME
            value: alicloud/nas
          securityContext:
            privileged: true
          volumeMounts:
          - mountPath: /var/log
            name: log
      volumes:
      - hostPath:
          path: /var/log
        name: log
```

## Mount a dynamic PV {#section_bvt_62z_uqy .section}

1.  Configure StorageClass. 

    ``` {#codeblock_yjr_n8t_4ka}
    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: alicloud-nas
    mountOptions:
    - nolock,tcp,noresvport
    - vers=3
    parameters:
      server: "23a9649583-iaq37.cn-shenzhen.nas.aliyuncs.com:/nasroot1/"
      driver: flexvolume
    provisioner: alicloud/nas
    reclaimPolicy: Delete
    ```

    |Parameter|Description|
    |---------|-----------|
    |mountOptions|The options used for mounting the PV.|
    |server|The mount points used for mounting the PV,     -   in the nfsurl1:/path1, nfsurl2:/path2 format.
    -   If multiple servers are specified, the PV provisioned through StorageClass will poll these servers to select a mount point.
 |
    |driver|The driver used for access to an Apsara File Storage NAS file system. Valid values: flexvolume and nfs. Default value: nfs.|
    |reclaimPolicy|The reclaim policy for a PV. We recommend that you set this parameter to Retain. If you set this parameter to Delete, the name of the directory in the Apsara File Storage NAS file system corresponding to the PV will automatically be changed when you delete a PV. For example, path-name will be changed to archived-path-name. If you want to delete the directory in the file system corresponding to the PV, set archiveOnDelete to false in Storage Class.

 |

2.  Access the dynamic PV. 

    ``` {#codeblock_kmr_nkx_766}
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx
    ---
    apiVersion: apps/v1beta1
    kind: StatefulSet
    metadata:
      name: web
    spec:
      serviceName: "nginx"
      replicas: 5
      volumeClaimTemplates:
      - metadata:
          name: html
        spec:
          accessModes:
            - ReadWriteOnce
          storageClassName: alicloud-nas
          resources:
            requests:
              storage: 2Gi
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:alpine
            volumeMounts:
            - mountPath: "/data"
              name: html
    ```


