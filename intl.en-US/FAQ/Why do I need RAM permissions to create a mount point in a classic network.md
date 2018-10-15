# Why do I need RAM permissions to create a mount point in a classic network {#concept_42176_zh .concept}

Unlike Virtual Private Cloud \(VPC\) environments, classic network environments are not isolated at the network layer. To ensure data security of your NAS file system, NAS must be authorized through RAM to list your ECS instances. This makes sure that only your own ECS instances can mount or access the NAS file system. Note that the NAS file system and the ECS instance must be under the same Alibaba Cloud account.

**Note:** 

-   NAS is only granted permission to call your DescribeInstances interface and has no permission to call any other instances. ECS instances acquired by NAS through the DescribeInstances interface are only used for permission verification, and are not recorded in any form.
-   Do not delete or edit AliyunNASDefaultRole in RAM as it may cause an operation exception error or failure when mounting the file system.

