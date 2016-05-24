---
# required metadata

title: 開發人員注意事項 | Azure RMS
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

# 開發人員注意事項

本節涵蓋數個重要開發案例的特定指引。 本節中的案例僅適用此版 Rights Management Services SDK 2.1，後續版本可能會改變。

- [新增明確的擁有者權限](add-explicit-owner-rights.md) - 從頭開始建立授權時，您的應用程式應該明確加入「擁有者」權限 ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch))。
- [常見的錯誤狀況和解決方案](common-error-conditions-and-solutions.md) - 本主題包括使用 RMS SDK 2.1 開發人員工具時可能遭遇到的常見錯誤訊息。
- [啟用電子郵件通知](how-to-enable-email-notification.md) - 可存取受保護的內容時，用來通知其擁有者的電子郵件。
- [檔案 API 組態](file-api-configuration.md) - 可透過登錄中設定進行設定的檔案 API 的行為。
- [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md) - 本主題包含建立具備權限的應用程式範例的指示。
- [設定 API 安全性模式](setting-the-api-security-mode-api-mode.md) - 您可以使用 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)，選擇檔案 API 應用程式執行的安全性模式。
- [支援的檔案格式](supported-file-formats.md) - 檔案 API 支援原生與 Pfile 格式。
- [追蹤內容](tracking-content.md) - 本主題涵蓋了追蹤 RMS SDK 2.1 所保護之內容文件的基本實作指導方針。
- [使用加密](working-with-encryption.md) - 本主題會將您導向我們的加密套件，並顯示其部分程式碼使用片段。

 

## 相關主題 ##
* [概觀](ad-rms-overview.md)
* [如何使用](how-to-use-msipc.md)
 

 


<!--HONumber=Apr16_HO4-->


