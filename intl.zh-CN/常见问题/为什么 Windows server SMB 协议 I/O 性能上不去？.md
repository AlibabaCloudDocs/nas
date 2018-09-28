# 为什么 Windows server SMB 协议 I/O 性能上不去？ {#concept_61903_zh .concept}

## 现象 {#section_yz4_q1h_hfb .section}

Windows SMB 客户端默认不打开 `large mtu` 选项，因此影响 I/O 性能提升。

## 解决方案 { .section}

您可以去修改注册表项来打开 `large mtu` 特性。

注册表路径： HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters 。

在该路径下，增加`DWORD`类型的键，命名为DisableLargeMtu，设置其值为 `0`，重新挂载后即可生效。

