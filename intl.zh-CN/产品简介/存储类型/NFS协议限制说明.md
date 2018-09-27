# NFS协议限制说明 {#concept_27535_zh .concept}

文件存储 NAS 目前支持的 NFS 协议包括 NFSv3 和 NFSv4，在某些功能的支持上存在限制。

-   NFSv4.0 不支持的 Attributes 包括：FATTR4\_MIMETYPE， FATTR4\_QUOTA\_AVAIL\_HARD，FATTR4\_QUOTA\_AVAIL\_SOFT，FATTR4\_QUOTA\_USED，FATTR4\_TIME\_BACKUP，FATTR4\_TIME\_CREATE，客户端将显示 NFS4ERR\_ATTRNOTSUPP 错误。

-   NFSv4.1 不支持的 Attributes 包括：FATTR4\_DIR\_NOTIF\_DELAY，FATTR4\_DIRENT\_NOTIF\_DELAY，FATTR4\_DACL，FATTR4\_SACL，FATTR4\_CHANGE\_POLICY，FATTR4\_FS\_STATUS，FATTR4\_LAYOUT\_HINT，FATTR4\_LAYOUT\_TYPES， FATTR4\_LAYOUT\_ALIGNMENT，FATTR4\_FS\_LOCATIONS\_INFO，FATTR4\_MDSTHRESHOLD，FATTR4\_RETENTION\_GET，FATTR4\_RETENTION\_SET，FATTR4\_RETENTEVT\_GET，FATTR4\_RETENTEVT\_SET， FATTR4\_RETENTION\_HOLD，FATTR4\_MODE\_SET\_MASKED，FATTR4\_FS\_CHARSET\_CAP，客户端将显示 NFS4ERR\_ATTRNOTSUPP 错误。

-   NFSv4 不支持的 OP 包括：OP\_DELEGPURGE，OP\_DELEGRETURN，NFS4\_OP\_OPENATTR，客户端将显示 NFS4ERR\_NOTSUPP 错误。

-   NFSv4 暂不支持 Delegation 功能。

-   关于 UID 和 GID 的问题：

    -   对于 NFSv3 协议，如果 Linux 本地账户中存在文件所属的 UID 或 GID，则根据本地的 UID 和 GID 映射关系显示相应的用户名和组名；如果本地账户不存在文件所属的 UID 或 GID，则直接显示 UID 和 GID。

    -   对于 NFSv4 协议，如果本地 Linux 内核版本低于 3.0，则所有文件的 UID 和 GID 都将显示 nobody；如果内核版本高于 3.0，则显示规则同 NFSv3 协议。

        **说明：** 若使用 NFSv4 协议挂载文件系统，且 Linux 内核版本低于 3.0，建议您不要对文件或目录进行 change owner 或 change group 操作，否则该文件或目录的 UID 和 GID 将变为 nobody。

-   单个文件系统最多能够被10,000个计算节点同时挂载访问。

