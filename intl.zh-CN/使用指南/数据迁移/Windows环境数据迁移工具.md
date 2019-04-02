# Windows环境数据迁移工具 {#concept_56937_zh .concept}

Nasimport也提供Windows版本，下载后解压即用。用于将对象存储（如OSS、七牛等）或本地磁盘上的文件同步到 NAS文件系统。

## 特性 {#section_yxg_drn_hfb .section}

Nasimport具有以下特性：

-   支持的数据源：本地磁盘、OSS、七牛、百度对象存储、金山对象存储、又拍云、亚马逊 s3、腾讯云 cos、HTTP链接；
-   支持存量数据同步（允许指定只同步某个时间点之后的文件）；
-   支持增量数据自动同步；
-   支持断点续传；
-   支持并行数据下载和上传。

## 运行要求 { .section}

Nasimport需要在能够挂载目标NAS文件系统的ECS虚拟机上运行。有关虚拟机能否挂载NAS文件系统及如何挂载，请参见[挂载前注意事项](../../../../intl.zh-CN/快速入门/挂载文件系统/挂载前注意事项.md#)中的SMB部分。

## 支持的操作系统 { .section}

1.  Windows Server 2008 标准版 SP2 32位
2.  Windows Server 2008 R2 数据中心版 64位
3.  Windows Server 2012 R2 数据中心版 64位
4.  Windows Server 2016 数据中心 64位

## 部署及配置 { .section}

首先，在您本地服务器上创建同步的工作目录（这里以C:\\NasImport作为示例），并且将nasimport工具包下载在该目录中。

1.  从以下链接下载工具包：[http://nasimport.oss-cn-shanghai.aliyuncs.com/nasimport-win.zip](http://nasimport.oss-cn-shanghai.aliyuncs.com/nasimport-win.zip) 
2.  创建一个新的工作目录，并将压缩包解压到目录中

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013210_zh-CN.png)

3.  编辑工作目录下的配置文件config/sys.properties

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013211_zh-CN.png)

    建议您直使用配置默认值。如有特殊要求，可以编辑配置字段值

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013212_zh-CN.png)


## NasImport命令 { .section}

-   提交任务：`nasimport -c config/sys.properties submit <your-job-configuration>` 
-   取消任务：`nasimport -c config/sys.properties clean <job-name>` 
-   查看任务：`nasimport -c config/sys.properties stat detail` 
-   重试任务：`nasimport -c config/sys.properties retry <job-name>` 
-   启动服务：`nasimport -c config/sys.properties start` 

## 启动服务 { .section}

1.  进入工作目录，并在当前目录中打开一个命令行。
2.  在命令行中运行`nasimport –c config/sys.properties start` 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013213_zh-CN.png)


**说明：** 

-   请保持nasimport处于运行状态。或者，用户可以将其设置为一个Windows后台服务
-   启动nasimport时，可以将日志重定向到文件，方便以后查看`nasimport -c config\sys.properties start > nasimport.log 2>&1` 

## 定义任务 { .section}

config\\local\_job.cfg是一个任务定义文件的模板，您可以按照此模板来定义自己的任务。模板中的字段和说明如下所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013214_zh-CN.png)

**说明：** 

-   如果配置了自动增量模式，则任务会定期被执行以扫描最新的数据，该任务永远不会结束。
-   对于 srcType为 youpai 的情况，由于又拍云本身 API 限制，list 文件的操作无法实现 checkpoint，在 list 完成之前杀掉进程会导致重新 list 所有文件的操作。

## 示例任务提交 { .section}

这里，我们尝试将本地的C:\\Program Files\\Internet Explorer复制到NAS上。

1.  编辑任务：复制一份config\\local\_job.cfg到工作目录，编辑以下项

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013215_zh-CN.png)

    **说明：** destMountDir要选择一个当前不存在的盘符，否则会和已经存在的产生冲突。destMountTarget为NAS的挂载点。

2.  提交任务：在工作目录重新启动一个命令行，运行`nasimport -c config\sys.properties submit local_job.cfg` 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013216_zh-CN.png)

    **说明：** 

    -   如果有同名任务正在执行，则提交任务会失败。
    -   如果您需要暂停同步任务，您可以停止 nasimport 进程，需要同步时重启 nasimport 进程即可，重启后会按照上次的进度继续上传。

## 查看任务状态 { .section}

在命令行中输入`nasimport -c config\sys.properties stat detail` 

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392013217_zh-CN.png)

这里会显示当前任务的总体的执行进度，并且会显示当前正在执行的 task进度。例如上文中：“4158464/30492741”表示：已经上传完成的数据量\(4158464字节\)/总共需要上传的数据量\(30492741字节\)。“1/1” 表示：总共需要上传的文件个数\(1个\)/已经上传完成的文件个数\(1个\)。

迁移工具会将用户提交的一个 job 任务分解为多个 task 并行执行，当所有的 task 都执行完成之后，job 任务才算执行完成。任务执行完成之后，JobState 会显示为”Succeed”或者”Failed”，表示任务执行成功或者失败。如果任务执行失败，可以通过以下文件查看各个task失败的原因：

```
master/jobs/$jobName/failed_tasks/*/audit.log

```

对于任务失败的情况，我们在工具中已经做了较为充分的重试，对于可能由于数据源或者目标源暂时不可用引起的失败情况，可以通过如下命令尝试重新执行失败的 TASK：

```language-bash
nasimport  -c config/sys.properties retry <job-name>

```

一段时间后，再次运行stat detail命令，

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392113218_zh-CN.png)

此时，`SucceededTasks`为1，表示任务已经完成。打开文件浏览器，可以看到，h:盘中，已经有相关的文件了：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392113219_zh-CN.png)

## 常见失败原因 { .section}

-   任务配置出错，比如 access key/id 出错，权限不足等，这种情况下通常现象是所有task都失败，具体确认需要查看工作目录下的nasimport.log 文件（启动nasimport时需要将日志重定向到此文件，或者，直接在运行nasimport start的命令行上直接查看）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18701/153821392113220_zh-CN.png)

-   源文件名的编码方式与系统默认的文件名编码方式不符，例如在 windows下文件名默认为 gbk 编码，linux 下默认为 utf-8 编码，对于数据源是 nfs 的情况下较容易出现该问题。
-   上传过程中源目录的文件发生了修改，这种情况在 audit.log 里会提示SIZE\_NOT\_MATCH 相关字样的错误，这种情况下老的文件已经上传成功，新的修改没有上传到 nas。
-   源文件在上传过程中被删除，导致下载文件时失败。
-   数据源出现问题导致下载数据源文件失败。
-   没有先杀掉进程再执行 clean 有可能会导致程序执行异常。
-   程序异常退出，任务状态为 Abort，这种情况请联系我们（请加旺旺群：1562614356 ）。

## 建议 { .section}

在配置迁移服务时，如果源端是 oss，请将 srcDomain 设为带 internal 的内网域名，可以省掉从 oss 源端下载的流量费，仅收取 oss 访问次数的费用，且可以获得更快的迁移速度，oss 内网域名您可以从 oss 控制台获取。

如果您的 NAS 在专有网络中，且源端是 oss，请将 srcDomain 设为 oss 提供 的VPC 环境域名。有关各 Region 对应的 VPC 环境域名，请参阅[访问域名和数据中心](../../../../intl.zh-CN/开发指南/访问域名和数据中心.md#)。

