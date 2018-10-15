# What is NAS and where can I use it {#concept_42179_zh .concept}

Alibaba Cloud Network Attached Storage \(NAS\) is a highly reliable, highly available file storage service featuring a distributed file system with unlimited capacity and performance scaling, with namespace and multiple client access support.

NAS supports standard file access protocols, so existing applications do not need to be modified. Furthermore, NAS supports multiple computing nodes \(such as ECS instances, E-HPC, and Container Service\) simultaneously reading or writing data to the file system.

Scenarios that benefit from Alibaba Cloud ECS instances using NAS include:

-   Deploying services using Server Load Balancer and multiple ECS servers \(such as web servers\) for scenarios where multiple ECS servers need to access the same bucket to share data.
-   Sharing logs for when apps on multiple ECS servers need to write logs to the same bucket to facilitate concentrated log data processing and analysis.
-   Sharing files where NAS enables you to store your enterprises public files in a centralized manner and share data to multiple business groups, all while maintaining data security.

