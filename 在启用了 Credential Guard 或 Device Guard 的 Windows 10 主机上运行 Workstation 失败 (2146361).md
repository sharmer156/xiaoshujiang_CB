---
layout: post
title:  "在启用了 Credential Guard 或 Device Guard 的 Windows 10 主机上运行 Workstation 失败 (2146361)"
categories: 虚拟机
tags:  兼容问题, 虚拟机,硬件保护
author: 飘的沙鸥
---
* content
{:toc}

---
安装完DOCKER和安卓stiudio之类的软件无意间打开了HYPER-V的功能导致虚拟机无法运行，此为官方解决方案，到第二步就已经解决，后面的代码没有尝试。
在启用了 Credential Guard 或 Device Guard 的 Windows 10 主机上运行 Workstation 失败 (2146361)

* * *

* [Symptoms](#symptoms)
* [Purpose](#purpose)
* [Cause](#cause)
* [Resolution](#resolution)






**Last Updated: **2017/1/1 
# Symptoms 
**免责声明**：本文为 [Windows 10 host where Credential Guard or Device Guard is enabled fails when running Workstation (2146361)](https://kb.vmware.com/s/article/2146361?r=3&CoveoV2.CoveoLightningApex.getInitializationData=1&other.KM_Utility.getAllTranslatedLanguages=1&other.KM_Utility.getArticleDetails=1&other.KM_Utility.getArticleMetadata=1&other.KM_Utility.getUrl=1&other.KM_Utility.getUser=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1) 的翻译版本。尽管我们会不断努力为本文提供最佳翻译版本，但本地化的内容可能会过时。有关最新内容，请参见英文版本。

* * *

在启用了 Credential Guard 或 Device Guard 的 Windows 10 主机上运行 Workstation 失败并显示蓝色诊断屏幕 (BSOD)。  
# Purpose 
本文介绍了为 Windows 10 Enterprise 主机禁用 Credential Guard 或 Device Guard 的步骤。 
# Cause 
出现此问题的原因是，Device Guard 或 Credential Guard 与 Workstation 不兼容。
# Resolution 
要在基于 Itanium 的计算机上禁用 Device Guard 或 Credential Guard，请执行以下操作：

1.  禁用用于启用 Credential Guard 的组策略设置。

    1.  在主机操作系统上，单击**启动**>**运行**，键入gpedit.msc,，然后单击**确定**。将打开本地组策略编辑器。
    2.  转到**本地计算机策略**>**计算机配置**>**管理模板 > 系统**>**Device Guard**>打开基于虚拟化的安全。
    3.  选择**禁用**。

2.  转到**控制面板**>**卸载程序**>**打开或关闭 Windows 功能以关闭 Hyper-V**。
** <---操作完第2步基本就能能运行了--->

3.  选择**不重新启动**。
4.  通过使用管理员帐户在主机上启动命令提示符来删除相关的 EFI 变量并运行以下命令：

>     mountvol X: /s
>     copy %WINDIR%\System32\SecConfig.efi X:\EFI\Microsoft\Boot\SecConfig.efi /Y
>     bcdedit /create {0cb3b571-2f2e-4343-a879-d86a476d7215} /d "DebugTool" /application osloader
>     bcdedit /set {0cb3b571-2f2e-4343-a879-d86a476d7215} path "\EFI\Microsoft\Boot\SecConfig.efi"
>     bcdedit /set {bootmgr} bootsequence {0cb3b571-2f2e-4343-a879-d86a476d7215}
>     bcdedit /set {0cb3b571-2f2e-4343-a879-d86a476d7215} loadoptions DISABLE-LSA-ISO,DISABLE-VBS
>     bcdedit /set {0cb3b571-2f2e-4343-a879-d86a476d7215} device partition=X:
>     mountvol X: /d

    **注意**：确保X为未使用的驱动器，否则更改为其他驱动器。

5.  重新启动主机。
6.  接受引导屏幕上的提示，禁用 Device Guard 或 Credential Guard。

如果您的主机使用传统 BIOS 引导，请执行以下操作：

1.  以管理员身份在主机上打开命令提示符。
2.  运行以下命令：

    bcdedit /set hypervisorlaunchtypeoff

3.  重新引导主机。

**注意**：在“运行”选项卡中查找 EFI 或 BIOS 类型msinfo32.exe。  Related Information [Powering on a vm in VMware Workstation prior to version 12.5 on Windows 10 host where Credential Guard/Device Guard is enabled fails with BSOD](https://kb.vmware.com/s/article/2146361?r=3&CoveoV2.CoveoLightningApex.getInitializationData=1&other.KM_Utility.getAllTranslatedLanguages=1&other.KM_Utility.getArticleDetails=1&other.KM_Utility.getArticleMetadata=1&other.KM_Utility.getUrl=1&other.KM_Utility.getUser=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1)  Request a Product Feature To request a new product feature or to provide feedback on a VMware product, please visit the [Request a Product Feature](http://www.vmware.com/contact/contactus.html?department=prod_request) page