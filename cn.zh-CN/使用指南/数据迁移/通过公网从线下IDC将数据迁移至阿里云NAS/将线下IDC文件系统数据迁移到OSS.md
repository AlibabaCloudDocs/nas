# 将线下IDC文件系统数据迁移到OSS {#task_fft_gxj_kfb .task}

通过公网从线下 IDC 迁移数据到阿里云 NAS 时，需要先使用 ossutil 将数据迁移至阿里云 OSS。

1.  在阿里云创建 OSS 存储空间，并获取对应子账号的 AccessKey。 
2.  下载 ossutil。 

    各版本的 binary 下载地址如下：

    -   \[Linux x86 32bit\] ：[ossutil32](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524643908776/ossutil32)
    -   \[Linux x86 64bit\] ：[ossutil64](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524643963683/ossutil64)
    -   \[Windows x86 32bit\] ：[ossutil32.zip](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524644014650/ossutil32.zip)
    -   \[Windows x86 64bit\] ：[ossutil64.zip](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524644040363/ossutil64.zip?spm=a2c4g.11186623.2.5.179c779cUGcduC&file=ossutil64.zip)
    -   \[Mac x86 64bit\] ：[ossutilmac64](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524644116085/ossutilmac64)
3.  安装 ossutil。 
    -   在 Linux 中，运行下载的 binary 文件。

        ```
        ./ossutil config
        ```

        **说明：** 如果 binary 为不可执行文件，请运行`chmod 755 ossutil` 给 binary 增加可执行权限。

    -   在 Windows 系统中，解压下载的压缩包，双击运行其中的 bat 文件，输入ossutil64.exe。
    -   在 Mac OS 中，执行以下命令：

        ```
        ./ossutilmac64 config
        ```

4.  在显示的 ossutil 交互界面中，按照提示输入配置参数。Windows 中的界面如下：![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22768/155616119413493_zh-CN.png)

 

    **说明：** 配置参数中，accessKeyID 和 accessKeySecret是必选项。

5.  运行以下命令，启动拷贝。 

    ```
    ./ossutil cp -r userdir oss://ossutil-test
    ```

    **说明：** 命令中userdir是用户待上传的目录，oss://ossutil-test是用户创建的 OSS 存储空间，请根据实际参数输入。


