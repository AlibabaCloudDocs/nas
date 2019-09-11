# 通过Flexvolume驱动-动态NAS存储卷挂载文件系统 {#task_1780353 .task}

本文介绍如何通过Flexvolume驱动-动态NAS存储卷方式实现在容器服务Kubernetes集群中使用阿里云NAS数据卷。

1.  已创建阿里云Kubernetes集群，详情请参见[创建Kubernetes 集群](../../../../cn.zh-CN/Kubernetes集群用户指南/集群管理/创建集群/创建Kubernetes 集群.md#)。

    如果是自建Kubernets集群，请先下载并安装[阿里云Flexolume驱动](https://github.com/AliyunContainerService/flexvolume)。

2.  确认Flexvolume驱动版本为v1.12.6.52-f6604e5-aliyun及以上版本。

    如果低于该版本，请升级Flexvolume驱动，详情请参见 [升级Flexvolume驱动](升级Flexvolume驱动../../SP_235/DNCSK19102190/ZH-CN_TP_80841_V2.dita#task_z3j_tvk_2gb)。

3.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。

    创建的文件系统需要与您的Kubernetes集群在同一可用区。

4.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。

    添加挂载点时所选的VPC网络要与您Kubernetes集群所在的VPC网络保持一致。


本方案实现的动态NAS存储卷，是在某个NAS文件系统下通过创建子目录、并把子目录映射为一个动态PV提供给应用。

**说明：** 动态生成NAS存储卷的本质是在一个已有的文件系统上，自动生成一个目录，这个目录定义为目标存储卷。

## 安装控制器 {#section_2hv_yu7_erq .section}

通过下面模板部署alicloud-nas-controller。

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

## 创建动态NAS存储卷 {#section_bvt_62z_uqy .section}

1.  配置StorageClass。 

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

    |参数|说明|
    |--|--|
    |mountOptions|表示生成的pv options配置，挂载NAS存储卷时使用这个挂载选项进行挂载。|
    |server|表示生成目标PV所使用的NAS挂载点列表。     -   格式为nfsurl1:/path1,nfsurl2:/path2。
    -   当配置多个server时，通过此storageclass创建的PV会轮询使用上述server作为配置参数。
    -   极速型NAS配置path时，需要以/share开头。
 |
    |driver|支持flexvolume、nfs两种驱动，默认为nfs。|
    |reclaimPolicy|PV的回收策略，建议配置为Retain。 当配置为Delete时，删除PV后NAS文件系统中对应的目录会默认修改名字（path-name ==\> archived-path-name）。如果需要删除文件系统中对应的存储目录，可在storageclass中配置archiveOnDelete为false。

 |

2.  使用动态NAS存储卷。 

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


