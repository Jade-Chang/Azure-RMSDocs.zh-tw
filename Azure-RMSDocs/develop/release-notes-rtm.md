---
# required metadata

title: 版本資訊 | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 84a93d5b-37e9-4d9c-9b7c-ad00963a68d7

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 版本資訊

本主題包含此版和舊版 RMS SDK 2.1 的相關重要資訊。

## 2015 年 12 月更新的新功能

-   效能改進已在數個區域內實作，包含︰

    使用僅限授權伺服器時，從主要授權伺服器發行。

    沒有網路連線時，RMS SDK 2.1 會更快失敗。

-   改善錯誤訊息和疑難排解體驗的許多更新。
-   也請注意，[支援的平台](supported-platforms.md)清單也會更新。

## 2015 年 5 月更新

-   服務應用程式和以雲端為基礎的 RMS - [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 需要三項資訊；對稱金鑰、AppPrincipalId 和 TenantBposId。 這個主題已更新為提供處理此必要資訊的指引。 如需了解這項更新，請參閱更新版的[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 2015 年 4 月更新

-   文件追蹤現在可以透過一組新 API 執行。 如需詳細資訊，請參閱[追蹤內容](tracking-content.md)。
-   加密類型 - 我們現在支援加密套件選擇的 API 層級控制。 如需詳細資訊，請參閱[使用加密](working-with-encryption.md)。

    注意  我們將不再公開 API 中的 IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS 旗標。 這表示如果未來的應用程式參考這個旗標，它們將不再編譯，但已建置的應用程式仍將繼續運作，因為我們將會私下以 API 程式碼採用旗標。 我們仍然可以藉由變更旗標來達成取得已被取代之舊加密演算法旗標的優點。 如需詳細資訊，請參閱[使用加密](working-with-encryption.md)。

     

-   伺服器模式應用程式使用 IPC\_API\_MODE\_SERVER 的 [API 模式值](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)，不再需要應用程式資訊清單。 您可以對生產 RMS 伺服器測試應用程式，而且不需要在切換到生產環境時取得生產授權。 如需伺服器模式應用程式的詳細資訊，請參閱[應用程式類型](application-types.md)。
-   記錄目前透過檔案和 Windows 的事件追蹤等方法實作。
-   如果您在 Windows 7 SP1 或 Windows Server 2008 R2 機器上執行，請參閱「重要的開發人員注意事項」後面的注意事項。

## 2015 年 1 月更新

-   支援的受保護檔案 (pfile) 大小增加 - 現在可支援大於 1 GB 的 pfile 大小。 如需 pfiles 的詳細資訊，請參閱[支援檔案格式](supported-file-formats.md)。
-   為了更佳診斷而改善的記錄 - 記錄層級會顯示錯誤或警告做為應檢閱的訊息。 所有其他訊息，包括仍然顯示的例外狀況，將會記錄為資訊。

    我們選擇這個方法，讓您不會遺失任何詳細資料。 現在，只有重要訊息會顯示為警告層級。

-   取得公司範本 – 根據客戶報告和意見反應，大幅修正為範本取得程式碼。
-   改善的當地語系化一致性

## 2014 年 10 月更新

-   已更新 SDK 之檔案 API 元件的預設行為。 如需詳細資訊，請參閱[檔案 API 組態](file-api-configuration.md)。
-   新的電子郵件通知功能會在[啟用電子郵件通知](how-to-enable-email-notification.md)開發人員注意事項主題中說明。

## 2014 年 7 月更新

SDK 的檔案 API 元件已經擴充，並提供下列功能︰

-   識別要使用哪些保護裝置。
-   提供檔案資料粒度層級的 RMS 保護。

    此版本中新增的功能︰

    注意  進一步支援的資料類型和結構 (未列在這裡) 已新增至檔案 API 擴充功能。 已更新為此版本的所有主題都標示為初步主題而且可能變更。

     

    -   [**IpcfOpenFileOnHandle**]()
    -   [**IpcfOpenFileOnILockBytes**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfopenfileonilockbytes)
    -   [**IpcfGetFileProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetfileproperty)
    -   [**IpcfLogicalFileRangeToRawFileRange**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcflogicalfilerangetorawfilerange)
    -   [**IpcfReadFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfreadfile)
    -   [**IpcfSetEndOfFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfsetendoffile)
    -   [**IpcfWriteFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfwritefile)

## 2014 年 4 月更新

-   檔案 API 記憶體使用量，特別是針對大型 PFile，已大幅改善。
-   內容識別碼 現在可透過 IPC\_LI\_CONTENT\_ID 屬性寫入。 如需詳細資訊，請參閱[授權屬性類型](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)。
-   生產資訊清單需求 - 當 RMS 啟用的應用程式/服務正在以伺服器模式執行時，我們將不再需要資訊清單。 如需詳細資訊，請參閱[應用程式類型](application-types.md)。
-   **文件更新**

    已重新組織 - [如何使用](how-to-use-msipc.md)釐清環境設定和應用程式測試的步驟順序。

    測試最佳作法 - 利用 Azure RMS 測試之前為使用內部部署伺服器而新增的指引。 如需詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 重要的開發人員注意事項

-   **所有檔案類型的原生支援**

    原生支援可新增至具備此版 Rights Management Services SDK 2.1 的任何檔案類型 (副檔名)。 比方說，針對任何副檔名 &lt;ext&gt; (非 office 和 pdf)，如果該副檔名的系統管理員組態為「原生」，則會使用 \*.p&lt;ext&gt;。

    如需受支援檔案類型的詳細資訊，請參閱[檔案 API 組態](file-api-configuration.md)。

-   沒有 [KB2533623](https://support.microsoft.com/en-us/kb/2533623) 更新的 Windows 7 SP1 和 Windows Server 2008 R2 SP1 機器可能會出現下列錯誤，以保護任何 office 檔案，「參數不正確。 錯誤碼 0x80070057」。 如果您發現此情形，請安裝更新然後再試一次。 如果您仍發現問題，請連絡 RMS SDK 搶鮮版 (Beta) 的意見反應別名 <rmcstbeta@microsoft.com>。

    注意  如同 2015 年 4 月版，已新增檢查至此知識庫文章的安裝程序。

     

-   **檔案 API 整合**

    內含檔案 API 新增內容的 Active Directory Rights Management Services 提供下列優點和功能。

    您可以自動化方式保護機密資料，而不需要知道各種檔案格式所使用之資訊版權管理 (IRM) 實作的詳細資料。

    Microsoft Office 檔案、可攜式文件格式 (PDF) 檔案，以及選取的其他檔案類型可以使用原生保護來保護。 如需可利用原生保護加以保護的檔案類型完整清單，請參閱[檔案 API 組態](file-api-configuration.md)。

    除了系統檔案和 Office 檔案之外，所有檔案都可以使用 RMS 保護的檔案格式 (PFile) 加以保護。

-   問題︰從頭開始建立授權時，必須明確授與擁有權。

    解決方案︰使用 [IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 從頭開始建立授權時，您的應用程式必須明確將擁有者權限新增給授權擁有者。 如需詳細資訊，請參閱[新增明確的擁有者權限](add-explicit-owner-rights.md)。

-   問題︰如果應用程式使用其控制代碼對相同視窗呼叫 [IpcProtectWindow](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) 或 [IpcUnprotectWindow](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) 兩次，RMS SDK 2.1 會在 HRESULT 中傳回失敗。

    解決方案︰如需此情形的特定指引，請參閱 [IpcProtectWindow](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow) 和 [IpcUnprotectWindow](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow) 中的「備註」一節。

-   問題︰針對多個架構建置時，您必須使用本指引。

    解決方案︰如果您想要將 Ipcsecproc\*isv.dll 用於不同的架構 (例如，您已在 64 位元電腦上安裝 64 位元 SDK，但現在想要在需要 Ipcsecproc\*isv.dll 的 32 位元電腦上部署)，您必須在不同的電腦上安裝 32 位元 SDK，並從「%PROGRAMFILES%\\Microsoft 資訊保護與控制」資料夾將 Ipcsecproc\*isv.dll 檔案複製到該處 (預設位置或您選擇安裝 SDK 的位置)。

## 常見問題集

問︰預設語言行為如何使用採用 LCID 參數的函式？

答︰使用 0 做為預設地區。 在此情況下，AD RMS Client 2.1 會以下列順序查閱名稱和描述，並擷取可用的第一項︰

1 - 使用者偏好的 LCID。
2 - 系統地區設定 LCID。
3 - 在 Rights Management Server (RMS) 範本中指定的第一個可用語言。
如果無法擷取任何名稱和描述，則會傳回錯誤。 一個特定的 LCID 可能只有一個名稱和描述。

## 相關主題

* [概觀](ad-rms-overview.md)
* [新增明確的擁有者權限](add-explicit-owner-rights.md)
* [檔案 API 組態](file-api-configuration.md)
* [**IpcfGetSerializedLicenseFromFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfgetserializedlicensefromfile)
* [**IpcfEncryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfIsFileEncrypted**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfisfileencrypted)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)
* [**IpcUnprotectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcunprotectwindow)
 

 





<!--HONumber=Apr16_HO3-->


