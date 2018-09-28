# NFS挂载的客户端缓存以及如何使用noac选项 {#concept_hy2_hg3_ffb .concept}

## 问题现象 {#section_h4v_53h_hfb .section}

用户两台ECS挂载同一个NFS文件系统，在ECS-A上append写文件，在ECS-B用tail -f观察文件内容的变化。在ECS-A写完之后，在ECS-B看到文件内容变化会有10-30秒的延时。然而相同的场景下，如果直接在ECS-B上打开文件（比如vi）却是立即可以看到更新的内容的。

## 原因 {#section_rcj_w3h_hfb .section}

该现象与mount的选项以及tail -f实现相关。

用户使用的mount命令为：`mount -t nfs4 /mnt/`

对于在ECS-B上以这一方式NFS mount的文件系统，默认情况下kernel对文件和目录的属性维护了一份metadata缓存，文件和目录属性（包括许可权、大小、和时间戳记）缓存的目的是减少 NFSPROC\_GETATTR 远程过程调用（RPC）的需求。

tail -f 的实现是sleep+fstat来观察文件属性（主要是文件大小）的变化，然后读入文件并输出。可见，tail -f是否能实时输出文件内容，主要取决于fstat的结果，由于前面描述得metadata cache的存在，fstat轮询到的并不是实时的文件属性，因此，即使在NFS服务器端文件已经更新了，但tail -f却没法知道文件已经改动了，于是输出就会出现延时。

## 解决方法 {#section_mld_3jh_hfb .section}

使用mount 的noac选项可以disable文件和目录属性的缓存。

`mount -t nfs4 -o noac /mnt/`

