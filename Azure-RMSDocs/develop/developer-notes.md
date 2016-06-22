---
# required metadata

title: 開發人員指導與資訊 | Azure RMS
description: 本主題涵蓋數個重要開發案例的特定指引。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 開發人員指導與資訊

本章節涵蓋數個重要開發案例的指導，以及使用此 SDK 進行開發的一般資訊。 本節中的案例僅適用此版 Rights Management Services SDK 2.1，後續版本可能會改變。
- [如何：使用 ADAL 驗證](how-to-use-adal-authentication.md) - 使用 Azure Active Directory Authentication Library (ADAL) 向 Azure RMS 驗證您的應用程式。
- [如何：新增明確的擁有者權限](add-explicit-owner-rights.md) - 從頭開始建立授權時，您的應用程式應該明確新增「擁有者」權限 ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch))。
- [如何：對已啟用權限應用程式偵錯](debugging-applications-that-use-ad-rms.md) - 本主題顯示如何對您的應用程式偵錯及使用 Windows 事件記錄檔。
- [如何：啟用文件追蹤及撤銷](tracking-content.md) - 本主題涵蓋實作內容文件追蹤的基本指導，以及用於中繼資料更新及建立應用程式 **[追蹤使用情況]** 按鈕的範例程式碼。
- [如何：啟用電子郵件通知](how-to-enable-email-notification.md) - 電子郵件通知可讓受保護內容的擁有者，在有人存取他 (她) 的內容時收到通知。
- [如何：允許您的服務應用程式使用雲端式 RMS](how-to-use-file-api-with-aadrm-cloud.md) - 本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。
- [如何：安裝及設定 RMS 伺服器](how-to-install-and-configure-an-rms-server.md) - 本主題涵蓋連線到 RMS 伺服器以測試已啟用權限應用程式的步驟。
- [如何：設定 API 安全性模式](setting-the-api-security-mode-api-mode.md) - 您可以使用 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函式，選擇檔案 API 應用程式要執行的安全性模式。
- [如何：使用加密設定](working-with-encryption.md) - 本主題會將您導向我們的加密套件，並顯示其適用的幾個程式碼片段。
- [應用程式類型](application-types.md) - 本主題涵蓋您可能會選擇建立為具備權限的應用程式類型。
- [檔案 API 組態](file-api-configuration.md) - 可透過登錄中設定進行設定的檔案 API 的行為。
- [支援的檔案格式](supported-file-formats.md) - 檔案 API 支援原生與 Pfile 格式
- [支援的平台](supported-platforms.md)：本主題說明支援 RMS SDK 2.1 的用戶端與伺服器平台。
- [了解使用限制](understanding-usage-restrictions.md) - RMS 啟用的所有應用程式必須強制使用限制。
- [使用限制參考](usage-restriction-reference.md) - 使用限制是由本主題中列出的常數所定義。

 
## 相關主題 ##
* [概觀](ad-rms-overview.md)
 

 


<!--HONumber=Jun16_HO2-->


