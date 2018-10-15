# How to improve the access performance from IIS to NAS {#concept_65228_zh .concept}

## Symptom {#section_mjy_qfh_hfb .section}

When IIS uses the NAS share method to access a file, the IIS accesses the NAS many times. In contrast to the access to a local file system, each access to NAS involves at least one interaction over the network. Although each access lasts a short time, the client waits for a long time after many accesses of the IIS.

## Solution { .section}

To improve the performance, see: [https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200\(v=ws.10\)?spm=a2c4g.11186623.2.12.3f0e4f0bYtWYjJ&file=ff686200\(v=ws.10\)](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/ff686200(v=ws.10)?spm=a2c4g.11186623.2.12.3f0e4f0bYtWYjJ&file=ff686200(v=ws.10)).

You can change the three registry keys mentioned in the article to a greater value, for example, 600 or greater.

The three registry keys are all at HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters. Their names are:

-   FileInfoCacheLifetime
-   FileNotFoundCacheLifetime
-   DirectoryCacheLifetime

We recommend that you store JS files, CSS files, and other content related to webpage programs on your local storage, because the IIS accesses these files quite frequently.

