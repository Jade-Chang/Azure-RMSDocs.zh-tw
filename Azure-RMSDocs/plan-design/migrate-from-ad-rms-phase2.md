---
title: "從 AD RMS 移轉至 Azure Rights Management - 階段 2 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/23/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a9dc45fb5146b0a4d2f013bff9d090723ce95ee5
ms.openlocfilehash: 1016ecdd77e818840f2a2cfab8212e908291bb89


---
# 移轉階段 2 - 用戶端組態

*適用於︰Active Directory Rights Management Services、Azure Rights Management*

針對從 AD RMS 移轉至 Azure Rights Management (Azure RMS) 的階段 2 使用下列資訊。 這些程序涵蓋[從 AD RMS 移轉至 Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) 的步驟 5。


## 步驟 5： 重新設定用戶端使用 Azure RMS
對於 Windows 用戶端：

1.  [下載移轉指令碼](http://go.microsoft.com/fwlink/?LinkId=524619)：

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    這些指令碼會重設 Windows 電腦上的組態，使其使用 Azure RMS 服務，而不是 AD RMS。

2.  遵循重新導向指令碼 (Redirect_OnPrem.cmd) 中的指示修改指令碼，以指向新的 Azure RMS 租用戶。

    > [!IMPORTANT]
    > 上述指示包含使用您自己的 AD RMS 伺服器位址取代 **adrms** 和 **adrms.contoso.com** 範例位址。 當您執行這項動作時，請務必確認位址之前或之後都沒有任何其他空格，以免中斷移轉指令碼並造成難以識別的問題根本原因。 有些編輯工具會自動在貼上文字之後加入一個空格。

3. 如果使用者擁有 Office 2016︰指令碼尚未更新為包含 Office 2016 的設定，因此如果使用者具有這個版本的 Office，就必須手動更新指令碼︰

    - 針對 **CleanUpRMS.cmd** - 搜尋 `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` 這一行，並在其正下方加入下列一行：

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - 針對 **Redirect_Onprem.cmd** - 搜尋 `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F1` 這一行，並在其正下方加入下列兩行：

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    選擇性︰指令碼在註解中不會參考 Office 2016。 如果您想要更新註解以反映 Office 2016 的這些新增項目，請針對 **Redirect_Onprem.cmd** 進行下列變更：

    - 搜尋 `::     or MSIPC (Office 2013) with on-premises AD RMS`，並將其取代為下列：
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - 搜尋 `echo Redirect SCP for Office 2013`，並將其取代為下列：
    
            echo Redirect SCP for Office versions based on MSIPC

    - 搜尋 `echo Redirect MSIPC for Office 2013`，並取代為下列：
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  在 Windows 電腦上：

    - 在使用者內容中，以較高的權限執行這些指令碼。

    對於行動裝置用戶端和 Mac 電腦：

    -  移除部署 [AD RMS 的行動裝置延伸模組](http://technet.microsoft.com/library/dn673574.aspx)時所建立的 DNS SRV 記錄。

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

-   新增下列登錄值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd：

-   針對下列每個位置中每個提供為參數的 URL，建立下列登錄值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    每個項目都有 **https://舊 RMS 伺服器 URL/_wmcs/licensing** 的 REG_SZ 值，而其資料格式如下：**https://&lt;您的租用戶 URL&gt;/_wmcs/licensing**。

    > [!NOTE]
    > *&lt;您的租用戶 URL&gt;* 具有下列格式：**{GUID}.rms.[區域].aadrm.com**。
    > 
    > 例如：5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > 在針對 Azure RMS 執行 **Get-AadrmConfiguration** Cmdlet 時，您可以藉由辨識 [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 值來找出該值。


## 後續步驟
若要繼續移轉，請移至[第 3 階段 - 支援服務組態](migrate-from-ad-rms-phase3.md)。


<!--HONumber=Jul16_HO2-->


