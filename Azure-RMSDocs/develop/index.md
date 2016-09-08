---
title: "RMS 開發人員指南 | Azure RMS"
description: "現在提供三個層代的 Rights Management SDK。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: f030cf299c7555f35c8ff61172b5d1debb2c9e6b


---

# RMS 開發人員指南

## 概觀 ##
現已提供三個層代的 Rights Management SDK：**Microsoft Rights Management SDK 4.2** (適用於 Android、iOS/OS X、Windows 裝置和 Linux)、**Microsoft Rights Management SDK 2.1** (適用於 Windows 桌面用戶端) 和已取代的 **AD RMS SDK**。

## 軟體開發套件 ##
| SDK | 說明 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | 提供輕量級開發經驗之簡化、下一代工具組，可讓您的 Android、iOS、Mac OS X、Windows Phone/RT 及 Linux/C++ 裝置應用程式透過 Microsoft Rights Management 服務保護資訊 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | 功能強大的 SDK 產品，適用於 Windows 桌面應用程式開發人員和伺服器架構方案提供者，以啟用版權管理其產品|
|[AD RMS SDK]()|**注意** - AD RMS SDK 運用 Msdrm.dll 中的用戶端所公開的功能，適用於 Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008 和 Windows Vista。 它在後續版本中可能會變更或無法使用。 請改用 Microsoft Rights Management Services SDK 2.1，此版本是利用用戶端在 Msipc.dll 中公開的功能。|
|[AD RMS Scripting API]()| 用來建立指令碼以管理 AD RMS 安裝|

## 程式碼範例和工具 ##
此 Microsoft 集合跨所有支援的作業系統提供 RMS 程式碼範例和開發人員支援工具；會定期更新 Android、iOS/OS X、Windows Phone 和 Windows 桌面以維護與其支援的 SDK 的相容性。

| 項目 | 作業系統 | 支援 SDK 版本 | 說明 |
|------|------------------|------------------------|-------------|
| [讀取 PFILE 保護的 PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) | Windows 桌面| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK | **讀取 PFILE 保護的 PDF** 是我們的 RMS 開發人員的專屬部落格上的簡單程式碼範例，其使用 MSIPC 檔案 API 來解密並開啟 PFILE 保護的 PDF 文件。|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows 桌面 | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK | **IpcManagedAPI** 是為了方便受管理應用程式啟用 RMS 的 RMS SDK 2.1 的 .NET (C#) 表示法。|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Windows 桌面 | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK| **IPCNotepad** 是啟用 RMS 的應用程式範例，會帶領您完成每個啟用 RMS 的應用程式在保護和取用受限制的內容時應執行的基本步驟。|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Windows 桌面|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK|**IpcDlp** 是啟用 RMS 的資料流失防護 (DLP) 應用程式範例，會帶領您使用檔案 API 來保護和取用受限制的內容時，啟用 DLP RMS 的應用程式應執行的基本步驟。|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows 桌面|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK|**IpcAzureApp** 是示範如何在 Azure 應用程式中使用 RMS SDK，以保護 Azure Blob 儲存體中資料的範例。|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows 桌面|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK|**RmsDocumentInspector** 是可提供任何 RMS 保護檔案相關資訊的工具，例如內容識別碼或使用者權限。|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows 桌面|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版本的 2.x SDK|**RmsFileWatcher** 是範例，示範如何建置 Windows 應用程式，在檔案系統中監看目錄，並在每次變更 RMS 保護原則，例如新增檔案或修改檔案。|
| [iOS/OS X 使用案例](https://msdn.microsoft.com/library/dn758307(v=vs.85).aspx) |iOS / OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版本的 4.x SDK|**Objective C** 程式碼範例代表重要的開發案例，讓您習慣使用 RMS SDK。 範例包括使用 Microsoft 受保護的檔案格式、自訂受保護的檔案格式，以及自訂 UI 控制項。|
| [UI 程式庫和範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版本的 4.x SDK|GitHub 上的 **iOS 的 UI 程式庫和範例應用程式**，因此您可以快速地開始，並在您的應用程式中重複使用我們的標準 UI。|
| [UI 程式庫和範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版本的 4.x SDK|GitHub 上的 **Android 的 UI 程式庫和範例應用程式**，因此您可以快速地開始，並在您的應用程式中重複使用我們的標準 UI。|
| [Android 使用案例](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版本的 4.x SDK|**Java 程式碼範例**代表重要的開發案例，讓您習慣使用 RMS SDK。 範例包括使用 Microsoft 受保護的檔案格式、自訂受保護的檔案格式，以及自訂 UI 控制項。|



<!--HONumber=Aug16_HO4-->


