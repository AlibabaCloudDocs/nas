# Scenarios {#concept_27521_zh .concept}

To identify the target scenarios of Alibaba Cloud Network Attached Storage \(NAS\) more precisely, the application scenarios of NAS can be classified into the following five types:

## Enterprise applications {#section_mcf_txw_pfb .section}

With high scalability, elasticity, availability, and persistence, NAS can be used to store the files of enterprise applications and the applications delivered as services. NAS provides standard file system interfaces and semantics. Therefore, you can easily construct new applications or migrate your enterprise applications to Alibaba Cloud.

## Media and entertainment workflows {#section_n1y_byw_pfb .section}

Shared storage is used to process large files in media workflows, such as video editing, audio and video production, broadcast processing, and sound design and rendering. With the powerful data consistency model, high throughput, and shared file access, NAS can reduce the time required to complete the work flows and merge multiple local file repositories into a single repository that can be accessed by all users.

## Big data analysis {#section_er5_2yw_pfb .section}

NAS can provide the scale, performance, and features required by big data applications, for example, high throughput of computing nodes, post-write read consistency, and file operations with low latency. Many analysis workloads use file interfaces for data interactions and depend on file system semantics such as the file lock. In addition, the workloads also require to write a part of a file. NAS supports the required file system semantics and can provide scalable capacity and performance.

## Content management and Web services {#section_ixg_qyw_pfb .section}

As a file system with high throughput and persistence, NAS can be used in content management systems and Web service applications to store and provide information for websites and online publishing and archiving applications. NAS follows the expected file system semantics, file naming conventions, and the privileges that Web developers are used to applying. Therefore, you can easily integrate NAS with Web applications and use it in websites and online publishing and archiving applications.

## Container storage {#section_jcn_wyw_pfb .section}

Containers are ideal for microservices construction thanks to such features as fast presetting, portability, and process isolation. For the containers that access raw data at every start, a shared file system is required to allow these containers to access the file system no matter which instance they run on. NAS is ideal for container storage because it provides persistent shared access to file data.

