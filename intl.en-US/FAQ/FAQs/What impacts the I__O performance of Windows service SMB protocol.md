# What impacts the I/O performance of Windows service SMB protocol {#concept_61903_zh .concept}

## Symptom {#section_yz4_q1h_hfb .section}

By default, the `large mtu` option is disabled on a Windows SMB client, which affects the increase in I/O performance.

## Solution { .section}

You can modify the following registry key to enable the `large mtu` option:

HKLM\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters

Create a `DWORD` at this location with the key named DisableLargeMtu and value set to `0`. Restart the file system to apply the change.

