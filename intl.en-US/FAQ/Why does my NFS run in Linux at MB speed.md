# Why does my NFS run in Linux at MB speed {#concept_53839_zh .concept}

The Linux nfs client has restrictions on the number of NFS requests which can be simultaneously initiated. If the parameter is too small, it causes relatively poor I/O performance. In such cases, check the following parameter:

```
cat /proc/sys/sunrpc/tcp_slot_table_entries
```

For the default kernel, the maximum value of this parameter is 256. For better performance, you can increase the value of this parameter. Run the following command as root:

```language-shell
echo "options sunrpc tcp_slot_table_entries=128" >> /etc/modprobe.d/sunrpc.conf
echo "options sunrpc tcp_max_slot_table_entries=128" >>  /etc/modprobe.d/sunrpc.conf
sysctl -w sunrpc.tcp_slot_table_entries=128

```

After you apply the change, you must re-mount the file system or restart the client.

