# NAS备份服务 {#concept_73045_zh .concept}

文件存储NAS备份服务已经开始公测。该服务提供了操作便捷、策略灵活的备份支持。

## 简介 {#section_nvf_zvm_hfb .section}

NAS 备份服务能够接管整个备份流程，帮助您方便地完成整个自动化备份任务，将您从繁琐的人工操作与多版本管理中解放出来。您可以在控制台中快速定义备份任务。

NAS备份服务具有以下特性：

-   支持周期性备份。您可以指定备份间隔，每隔一段时间启动一次新的备份。目前支持的间隔为6/8/12/24小时。
-   支持多备份历史版本保存。每进行一次备份会生成一个新的备份版本。您可以设置需要保留的版本数。保留的版本数目最大为9。
-   支持基于备份的数据恢复。您可以选定特定版本的备份，将其恢复到一个文件系统。为了最大程度避免误操作，恢复目标必须是空文件系统。
-   支持手动触发新的备份任务。您可以手动地、即时地触发一个新的备份任务。这在自动备份的基础上为您提供了更加灵活的备份策略。

## 申请公测 {#section_vvh_mwm_hfb .section}

使用NAS备份服务需要申请公测资格，申请界面如下：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121113198_zh-CN.png)

您可以登录需要在NAS的控制台主页上进行申请。申请时需要填写公司名称以及需求。申请公测完成并在后端审核通过后，备份页面将被开启，如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121113199_zh-CN.png)

## 创建备份任务 {#section_azc_2xm_hfb .section}

获取公测资格后，您可以进行文件系统的备份。创建备份方法如下：

1.  登录[文件存储控制台](https://nas.console.aliyun.com/)。
2.  单击**备份**，单击右上角的**新建备份**，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121113200_zh-CN.png)

3.  在弹出的对话框中选择需要备份的**源文件系统**（即要备份的对象），如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121113201_zh-CN.png)

    创建备份任务中的其他选项描述如下：

    -    **开始时间**：目前只提供3个时间点供选择，分别是0点8点和16点。
    -    **备份间隔**：目前可选择6小时、12小时和24小时。一般情况下，推荐选择24小时，并将备份放在业务低峰时间。
    -    **备份保留份数**：指备份时需要保留最新版本的个数。
4.  创建备份任务完成后，备份服务会根据备份策略自动运行备份任务。

    **说明：** 您也可以在**备份**页面中单击源文件系统右侧的**立即备份**，人工触发一次备份，如下图所示：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121213202_zh-CN.png)


## 数据恢复 {#section_ww3_2ym_hfb .section}

备份服务目前支持将备份恢复到一个空的NAS文件系统上，恢复界面如下：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121213203_zh-CN.png)

您只需选择目标NAS文件系统及希望恢复的源文件系统备份版本号，即可将特定版本的备份恢复到目标文件系统。

关于希望恢复的源文件系统备份版本号，可在备份详情页中查找，如下图所示：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18698/153983121213204_zh-CN.png)

