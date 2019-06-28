# noresvport挂载参数问题检查整改步骤 {#task_508507 .task}

只针对Linux系统的用户，Windows用户请忽略。

## 第一步，检查是否使用noresvport挂载参数 {#section_gw8_cy2_741 .section}

1.  检查内核：执行命令`uname -r`，如果大于等于2.6.32-696.16.1，请继续操作， 否则请联系NAS研发团队（钉钉群号：23177020）。
2.  查看使用的NAS：执行命令`df -h | grep "nas.aliyuncs"`，如果非空请继续操作， 否则检查结束，表示您没有使用相关产品。
3.  检查参数：执行命令`mount | grep "nas.aliyuncs" | grep noresvport`，如果非空请继续操作，否则执行[第二步，noresvport参数修复方法](#section_9vr_izm_q8b)。
4.  确认参数生效：执行命令`ss -nt | grep 2049 | awk '{print $4}' | awk -F ':' '{print $2}'`，如果结果中存在小于1024的端口，则进行[第二步，noresvport参数修复方法](#section_9vr_izm_q8b)，否则检查结束，表示您已按指导完成配置。

## 第二步，noresvport参数修复方法（建议在业务低峰进行） {#section_9vr_izm_q8b .section}

1.  暂停挂载了NAS的ECS业务，然后在这些ECS上执行如下操作。
2.  执行命令`mount | grep "nas.aliyuncs"`，查询所有阿里云NAS挂载点的本地路径。
3.  `umount <挂载点本地路径>`，如果返回deviceisbusy，执行 4，否则执行6 。
4.  对每个挂载点本地路径执行命令`fuser -mv <挂载点本地路径>`，会返回使用 NAS的进程pid（pid为kernel的进程不需要处理），再执行`kill <pid>`杀掉这些进程（kill前请根据实际业务情况评估影响，建议在业务低峰进行）。
5.  执行命令`umount <挂载点本地路径>`（需要umount本台ECS的所有阿里云 NAS本地挂载路径），如果umount失败，请再次执行4。
6.  执行命令`mount | grep "nas.aliyuncs"`，确认返回结果为空，所有NAS文件系统全部卸载成功。否则使用剩余的挂载点本地路径执行3。
7.  重新用noresvport挂载（需要替换命令中的挂载点地址和本地挂载路径）。
    -   使用NFSV4挂载：

        ``` {#codeblock_xoj_l3x_3ra}
        sudo mount -t nfs -o vers=4,minorversion=0,noresvport fid-xxxx.cn-xxx.nas.aliyuncs.com:/ /mnt
        ```

    -   使用NFSV3挂载：

        ``` {#codeblock_e83_3uz_wow}
        sudo mount -t nfs -o vers=3,nolock,proto=tcp,noresvport fid-xxxx.cn-xxx.nas.aliyuncs.com:/ /mnt
        ```

8.  如果使用自动挂载，请在/etc/fstab中配置（需要替换命令中的挂载点地址和本地挂载路径）。
    -   使用NFSV4挂载：

        ``` {#codeblock_ktf_6h0_arr}
        fid-xxxx.cn-xxx.nas.aliyuncs.com:/ /mnt nfs vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
        ```

    -   使用NFSV3挂载：

        ``` {#codeblock_tf2_1yi_bm6}
        fid-xxxx.cn-xxx.nas.aliyuncs.com:/ /mnt nfs vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
        ```


至此修复完毕，可以执行[第一步，检查是否使用noresvport挂载参数](#section_gw8_cy2_741)确认修复生效。如仍有问题请及时联系我们（钉钉群号：23110762）。

