---
# required metadata

title: 從 AD RMS 移轉至 Azure Rights Management - 階段 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# 移轉階段 2 - 用戶端組態
針對從 AD RMS 移轉至 Azure Rights Management (Azure RMS) 的階段 2 使用下列資訊。 這些程序涵蓋[從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 的步驟 5。


## 步驟 5： 重新設定用戶端使用 Azure RMS
對於 Windows 用戶端：

1.  [下載移轉指令碼](http://go.microsoft.com/fwlink/?LinkId=524619)：

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    這些指令碼會重設 Windows 電腦上的組態，使其使用 Azure RMS 服務，而不是 AD RMS。

2.  遵循重新導向指令碼 (Redirect_OnPrem.cmd) 中的指示修改指令碼，以指向新的 Azure RMS 租用戶。

3.  在 Windows 電腦上，於使用者內容中以提高權限執行這些指令碼。

對於行動裝置用戶端和 Mac 電腦：

-   移除部署 [AD RMS 的行動裝置延伸模組](http://technet.microsoft.com/library/dn673574.aspx)時所建立的 DNS SRV 記錄。

#### 移轉指令碼所進行的變更
本節記載移轉指令碼所進行的變更。 此資訊僅供參考或進行疑難排解，或者，您可能會想要自己進行這些變更。

CleanUpRMS_RUN_Elevated.cmd：

-   刪除 %userprofile%\AppData\Local\Microsoft\DRM 和 %userprofile%\AppData\Local\Microsoft\MSIPC 資料夾的內容，包括任何子資料夾和任何具有長檔名的檔案。

-   刪除下列登錄機碼的內容：

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   刪除下列登錄值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd：

-   針對下列每個位置中每個提供為參數的 URL，建立下列登錄值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    每個項目都有 https://OldRMSserverURL/_wmcs/licensing 的 REG_SZ 值，而其資料格式如下：https://&lt;YourTenantURL&gt;/_wmcs/licensing。

    > [!NOTE]
    > &lt;YourTenantURL&gt; 具有下列格式：{GUID}.rms.[Region].aadrm.com。
    > 
    > 例如：5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > 在針對 Azure RMS 執行 Get-AadrmConfiguration Cmdlet 時，您可以藉由辨識 [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 值來找出該值。


## 後續步驟
若要繼續移轉，請移至[第 3 階段 - 支援服務組態](migrate-from-ad-rms-phase3.md)。

<!--HONumber=Apr16_HO3-->


