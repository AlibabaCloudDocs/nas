# 数据迁移上NAS工具（支持本地文件和OSS等） {#concept_45306_zh .concept}

nasimport工具可以帮助您将本地数据中心数据，阿里云 OSS 或第三方云存储服务上的文件同步到阿里云NAS 文件系统上。

## 主要特性 { .section}

nasimport工具具有以下特性：

-   支持将本地、OSS、七牛、百度对象存储、金山对象存储、又拍云、亚马逊 s3、腾讯云 cos、HTTP 链接形式的文件同步到指定 NAS 文件系统上。
-   支持自动挂载 NAS 文件系统。
-   支持存量数据同步\(允许指定只同步某个时间点之后的文件\)。
-   支持增量数据自动同步。
-   支持断点续传。
-   支持并行 list 和并行数据下载/上传。

如果您有较大量级的数据\(超过 2T\)，且期望以较短时间迁移到 NAS 上，除了nasimport同步工具之外，我们的专业技术人员还可以为您提供多机器并行同步方案，请加旺旺群：1562614356 联系我们。

## 运行环境 { .section}

您需要在能够挂载目标NAS文件系统的ECS虚拟机上运行该迁移工具。如需了解能否挂载NAS文件系统及如何挂载，请参阅[挂载前注意事项](../../../../intl.zh-CN/快速入门/挂载文件系统/挂载前注意事项.md#)。

您需要在 Java JDK 1.7 以上的环境中运行nasimport同步工具，建议使用 Oracle 版本 JDK： [点击查看](http://www.oracle.com/technetwork/indexes/downloads/index.html?spm=5176.doc32201.2.1.Y4A7gH#java) 

**说明：** 程序运行前请检查进程允许打开的文件数的配置\(ulimit -n 查看），如果小于10240，需要作相应修改。

## 部署及配置 { .section}

首先，在您本地服务器上创建同步的工作目录，并且将nasimport工具包下载在该目录中。

示例：

创建 /root/ms 目录为工作目录，且工具包下载在该工作目录下。

```language-shell
export work_dir=/root/ms
wget http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/45306/cn_zh/1479113980204/nasimport_linux.tgz
tar zxvf ./nasimport_linux.tgz -C "$work_dir"

```

编辑工作目录\($work\_dir\)下的配置文件 config/sys.properties：

```
vim $work_dir/config/sys.properties
workingDir=/root/ms
slaveUserName=
slavePassword=
privateKeyFile=
slaveTaskThreadNum=60
slaveMaxThroughput(KB/s)=100000000
slaveAbortWhenUncatchedException=false
dispatcherThreadNum=5

```

建议您直接使用配置默认值。如有特殊要求，可以编辑配置字段值。各字段的说明如下表所示：

|字段|说明|
|--|--|
|workingDir|表示当前的工作目录，即工具包解压后所在的目录|
|slaveTaskThreadNum|表示同时执行同步的工作线程数|
|slaveMaxThroughput\(KB/s\)|表示迁移速度总的流量上限限制|
|slaveAbortWhenUncatchedException|表示遇到未知错误时是否跳过还是 abort，默认不 abort|
|dispatcherThreadNum|表示分发任务的并行线程数，默认值一般够用|

## 运行服务 { .section}

nasimport 支持如下命令：

-   任务提交：`java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties submit $jobConfigPath`
-   任务取消：`java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties clean $jobName`
-   状态查看：`java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties stat detail`
-   任务重试：`java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties retry $jobName`

服务的运行和使用步骤如下：

1.  启动服务，执行如下命令：

    ```
    cd $work_dir
    nohup java -Dskip_exist_file=false -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties start > $work_dir/nasimport.log 2>&1 &
    
    ```

    **说明：** 相关的 log 文件会自动生成在您执行启动服务的当前目录中，建议您在工作目录（$work\_dir）下执行启动命令。启动任务时如果 skip\_exist\_file=true，则在上传中如果碰到 NAS 文件系统中上存在且长度和源端一致的文件，将会跳过此文件。

2.  编辑示例任务描述文件nas\_job.cfg。文件中的字段说明如下表：

    |字段名|说明|
    |---|--|
    |jobName|自定义任务名字，任务的唯一标识， 支持提交多个名字不同的任务|
    |jobType|可以配置为 import\(执行数据同步操作\)或者 audit（仅进行同步源数据与同步目标数据全局一致性校验\)|
    |isIncremental=false|是否打开自动增量模式，如果设为 true，会每间隔incrementalModeInterval\(单位秒\)重新扫描一次增量数据，并将增量数据同步到nas上|
    |incrementalModeInterval=86400|增量模式下的同步间隔|
    |importSince|指定时间，用于同步大于该时间的数据，这个时间为 unix 时间戳（秒数）；默认为0|
    |srcType|同步源类型，目前支持 oss,qiniu,baidu,ks3,youpai,local|
    |srcAccessKey|如果 srcType设 置为 oss,qiniu,baidu,ks3或youpai，则需要填写数据源的 access key|
    |srcSecretKey|如果 srcType 设置为 oss,qiniu,baidu,ks3或youpai，则需要填写数据源的 secret key|
    |srcDomain|源 endpoint|
    |srcBucket|源 bucket 名字|
    |srcPrefix|源前缀，默认为空；如果 srcType=local，则填写本地待同步目录，请注意您需要填写完整的目录路径\(以’/‘结尾\)。如果 srcType 设置为 oss,qiniu,baidu,ks3或youpai，则需要填写待同步的 Object 前缀，同步所有文件前缀可以设置为空。|
    |destType|同步目标类型（默认为 nas）|
    |destMountDir|NAS 本地挂载目录|
    |destMountTarget|NAS 挂载点域名|
    |destNeedMount=true|工具是否执行自动挂载，默认为 true，您也可以选择false并手动将NAS挂载点到 destMountDir目录下|
    |destPrefix|填写同步目标端文件前缀，默认为空|
    |taskObjectCountLimit|每个子任务最大的文件个数限制，这个会影响到任务执行的并行度，一般配置为总的文件数/你配置的下载线程数,如果不知道总文件数，可以配置为默认值|
    |taskObjectSizeLimit|每个子任务下载的数据量大小限制\(bytes\)|
    |scanThreadCount|并行扫描文件的线程数，与扫描文件的效率有关|
    |maxMultiThreadScanDepth|最大允许并行扫描目录的深度，采用默认值即可|

    **说明：** 

    -   如果配置了自动增量模式，则任务会定期被执行以扫描最新的数据，该任务永远不会结束。
    -   对于 srcType为 youpai的情况，由于又拍云本身 API 限制，list 文件的操作无法实现 checkpoint，在 list 完成之前杀掉进程会导致重新 list 所有文件的操作。
3.  执行以下命令，提交任务：

    ```
    java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties  submit $work_dir/nas_job.cfg
    
    ```

    **说明：** 

    -   如果有同名任务正在执行，则提交任务会失败。
    -   如果您需要暂停同步任务，您可以停止 nasimport 进程，需要同步时重启 nasimport 进程即可，重启后会按照上次的进度继续上传。
    -   如果您需要重新全量同步文件，您可以先停止 nasimport 进程，再调用如下命令清除当前任务。 示例：假设当前任务名为 nas\_job（这个任务名配置在文件 nas\_job.cfg 中），命令如下：

        ```
        ps axu | grep "nasimport.jar.* start" | grep -v grep | awk '{print "kill -9 "$2}' | bash
        java -jar $work_dir/nasimport.jar  -c $work_dir/conf/sys.properties clean nas_job
        
        ```

4.  查看任务执行状态：

    ```
    java -jar $work_dir/nasimport.jar -c $work_dir/config/sys.properties  stat detail
    --------------job stats begin---------------
    ----------------job stat begin------------------
    JobName:nas_job
    JobState:Running
    PendingTasks:0
    RunningTasks:1
    SucceedTasks:0
    FailedTasks:0
    ScanFinished:true
    RunningTasks Progress:
    FD813E8B93F55E67A843DBCFA3FAF5B6_1449307162636:26378979/26378979 1/1
    ----------------job stat end------------------
    --------------job stats end---------------
    
    ```


## 常见任务失败原因 {#section_eyx_4qn_hfb .section}

-   任务配置出错，比如 access key/id 出错，权限不足等，这种情况下通常现象是所有task都失败，具体确认需要查看 $work\_dir/nasimport.log 文件。
-   源文件名的编码方式与系统默认的文件名编码方式不符，例如在 windows 下文件名默认为 gbk 编码，linux 下默认为 utf-8 编码，对于数据源是 nfs 的情况下较容易出现该问题。
-   上传过程中源目录的文件发生了修改，这种情况在 audit.log 里会提示SIZE\_NOT\_MATCH 相关字样的错误，这种情况下老的文件已经上传成功，新的修改没有上传到 nas。
-   源文件在上传过程中被删除，导致下载文件时失败。
-   数据源出现问题导致下载数据源文件失败。
-   没有先杀掉进程再执行 clean 有可能会导致程序执行异常。
-   程序异常退出，任务状态为 Abort，这种情况请联系我们（请加旺旺群：1562614356 ）。

## 建议 {#section_bmz_pqn_hfb .section}

在配置迁移服务时，如果源端是 oss，请将 srcDomain 设为带 internal 的内网域名，可以省掉从 oss 源端下载的流量费，仅收取 oss 访问次数的费用，且可以获得更快的迁移速度，oss 内网域名您可以从 oss 控制台获取。

如果您的 NAS 在专有网络中，且源端是 oss，请将 srcDomain 设为 oss 提供 的VPC 环境域名各有关 Region 对应的 VPC 环境域名，请参阅：[访问域名和数据中心](../../../../intl.zh-CN/开发指南/访问域名和数据中心.md#)。

