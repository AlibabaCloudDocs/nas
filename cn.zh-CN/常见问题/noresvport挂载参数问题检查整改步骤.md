# noresvport挂载参数问题检查整改步骤 {#task_508507 .task}

只针对Linux系统的用户，Windows用户请忽略。

## 第一步，检查是否使用noresvport挂载参数 {#section_gw8_cy2_741 .section}

1.  在ECS上下载check\_noresvport.py检查脚本。

    ``` {#codeblock_jy8_0ht_zez}
    wget -N https://raw.githubusercontent.com/alibabacloudnas/nas-client-tools/master/linux_client/check_noresvport.py -P /tmp/
    ```

2.  使用python执行检查脚本。

    ``` {#codeblock_37o_qt1_8qp}
    python /tmp/check_noresvport.py
    ```

    如果脚本输出：本台ECS无须处理noresvport问题，则无须处理。否则请执行[第二步，noresvport参数修复方法](#section_9vr_izm_q8b)。


## 第二步，noresvport参数修复方法（建议在业务低峰进行） {#section_9vr_izm_q8b .section}

-   如果使用ECS直接挂载NAS，请使用参数-r再次执行检查脚本。

    ``` {#codeblock_dbe_htf_3do}
    python /tmp/check_noresvport.py -r
    ```

-   如果使用容器挂载NAS，请参考[K8S环境中NAS卷添加noresvport方法](https://yq.aliyun.com/articles/707169)重新挂载。如有疑问请联系NAS研发团队（钉钉群号：21906225）。

## 第三步，更新自动挂载配置 {#section_2ov_4wl_soy .section}

-   如果之前配置过自动挂载，请参考[自动挂载NFS文件系统](https://help.aliyun.com/document_detail/91476.html)更新自动挂载参数，加入noresvport挂载参数。
-   如果之前没有配置过自动挂载，可以跳过此步骤。

修复完成后，请再次执行[第一步，检查是否使用noresvport挂载参数](#section_gw8_cy2_741)确认修复生效。如果仍有问题请及时联系我们（钉钉群号：23110762）。

