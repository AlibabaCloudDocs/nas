# linux上NFS性能只有几MB速度 {#concept_53839_zh .concept}

Linux nfs客户端对于同时发起的NFS请求数量进行了控制，若该参数配置较小会导致IO性能较差，请查看该参数：cat /proc/sys/sunrpc/tcp\_slot\_table\_entries

默认编译的内核该参数最大值为256，可适当提高该参数的值来取得较好的性能，请以root身份执行以下命令：

```language-shell
echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
sysctl -w sunrpc.tcp_slot_table_entries=128

```

修改完成后，您需要重新挂载文件系统或重启机器。

