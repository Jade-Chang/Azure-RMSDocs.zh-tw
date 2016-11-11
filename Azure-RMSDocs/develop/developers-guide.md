---
title: "開發人員指南 | Azure RMS"
description: "開發人員工具使用概觀；SDK、額外程式庫和程式碼範例。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c50775c43aea8950ca9c560c61712ffbbede8599
ms.openlocfilehash: 442dd2e6b3487964d5740c533894aa4de30f00ab


---

# <a name="developers-guide"></a>開發人員指南

## <a name="overview"></a>概觀 ##
本指南概述 Rights Management SDK 套件以及跨所有支援平台之不斷增加的工具組和程式碼範例。

## <a name="software-development-kits"></a>軟體開發套件 ##
現在已提供三代的 RMS SDK (如下表所概述)。

| SDK | 說明 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | 提供輕量級開發經驗之簡化、下一代工具組，可讓您的 Android、iOS、Mac OS X、Windows Phone/RT 及 Linux/C++ 裝置應用程式透過 Microsoft Rights Management 服務保護資訊 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | 功能強大的 SDK 產品，適用於 Windows 桌面應用程式開發人員和伺服器架構方案提供者，以啟用版權管理其產品|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379.aspx)|**注意** - AD RMS SDK 運用 Msdrm.dll 中的用戶端所公開的功能，適用於 Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008 和 Windows Vista。 它在後續版本中可能會變更或無法使用。 請改用 Microsoft Rights Management Services SDK 2.1，此版本是利用用戶端在 Msipc.dll 中公開的功能。|
|[AD RMS 指令碼 API](https://msdn.microsoft.com/en-us/library/bb968797.aspx)| 用來建立指令碼以管理 AD RMS 安裝|

## <a name="powershell-guidance"></a>PowerShell 指引

[Azure Rights Management Cmdlet](https://msdn.microsoft.com/library/azure/dn629398.aspx) 可讓您從命令列管理 Azure RMS。 雖然這會啟用自動化，但同時仍會支援可靠而重複性的程序，以利降低管理工作負荷。 此外，部分 Azure RMS 進階設定及作業需要 Azure PowerShell。

[RMS Protection Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 可與 Azure 資訊保護的 Azure Rights Management (Azure RMS) 資料保護搭配使用，或是與 Active Directory Rights Management Services (AD RMS) 搭配並為這些 Rights Management 部署補充其他 PowerShell 模組。 使用這些 RMS Protection Cmdlet 為任何檔案類型大量保護檔案及解除檔案的保護。

## <a name="code-samples-and-tools"></a>程式碼範例和工具
此 Microsoft 集合跨所有支援的作業系統提供 RMS 程式碼範例和開發人員支援工具；會定期更新 Android、iOS/OS X、Windows Phone 和 Windows 桌面以維護與其支援的 SDK 的相容性。

### <a name="android"></a>Android

[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版 4.x SDK 支援 Android 上執行的下列元件。

- GitHub 上的 [UI 程式庫和範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-android)，因此您可以快速地開始，並在您的應用程式中重複使用我們的標準 UI。
- Java 中的 [Android 使用案例](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx)代表重要的開發案例，讓您習慣使用 RMS SDK。 範例包括使用 Microsoft 受保護的檔案格式、自訂受保護的檔案格式，以及自訂 UI 控制項。

### <a name="ios-os-x"></a>iOS / OS X

[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) 和更新版 4.x SDK 支援 iOS / OS X 上執行的下列元件。

- Objective C 中的 [iOS/OS X 使用案例](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx)代表重要的開發案例，讓您習慣使用 RMS SDK。 範例包括使用 Microsoft 受保護的檔案格式、自訂受保護的檔案格式，以及自訂 UI 控制項。
- GitHub 上的 [UI 程式庫和範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-ios)，因此您可以快速地開始，並在您的應用程式中重複使用我們的標準 UI。 **僅在 iOS** 上支援。

### <a name="windows-desktop"></a>Windows 桌面

[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) 和更新版 2.x SDK 支援 Windows 桌面上執行的下列元件。

- [讀取 PFILE 保護的 PDF](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) 是我們的 RMS 開發人員的專屬部落格上的簡單程式碼範例，其使用 MSIPC 檔案 API 來解密並開啟 PFILE 保護的 PDF 文件。
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是為了方便受管理應用程式啟用 RMS 的 RMS SDK 2.1 的 .NET (C#) 表示法。
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) 是啟用 RMS 的應用程式範例，會帶領您完成每個啟用 RMS 的應用程式在保護和取用受限制的內容時應執行的基本步驟。
- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是啟用 RMS 的資料流失防護 (DLP) 應用程式範例，會帶領您使用檔案 API 來保護和取用受限制的內容時，啟用 DLP RMS 的應用程式應執行的基本步驟。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是示範如何在 Azure 應用程式中使用 RMS SDK，以保護 Azure Blob 儲存體中資料的範例。
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是可提供任何 RMS 保護檔案相關資訊的工具，例如內容識別碼或使用者權限。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) 是範例，示範如何建置 Windows 應用程式，在檔案系統中監看目錄，並在每次變更 RMS 保護原則，例如新增檔案或修改檔案。

### <a name="windows-store-and-phone"></a>Windows 市集和 Phone

- [Windows 市集的 UI 程式庫](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - Windows 市集應用程式的 Microsoft RMS SDK v4.1 的 UI 程式庫。 此程式庫是選擇性的，開發人員可以選擇使用 Microsoft RMS SDK v4.1 建置其自己的 UI

- [Windows Phone 的 UI 程式庫](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - Windows Phone 應用程式的 Microsoft RMS SDK v4.1 的 UI 程式庫。 此程式庫是選擇性的，開發人員可以選擇使用 Microsoft RMS SDK v4.1 建置其自己的 UI

- [應用程式範例](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - Windows 市集應用程式的 Microsoft RMS SDK v4.1 範例為平台提供基本文件的使用範例。



<!--HONumber=Oct16_HO5-->


