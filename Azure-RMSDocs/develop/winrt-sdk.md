---
title: "Windows 市集設定 | Azure RMS"
description: "Windows 市集應用程式可以使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: dc452dac3a86cd9cc39127d5a29106ae87ba94be
ms.openlocfilehash: c3dfa23a4bb03aec3ad9eae835382040a5347006


---

# <a name="windows-store-setup"></a>Windows 市集設定

Windows 市集應用程式可以藉由使用 Azure Active Directory Rights Management (AAD RM)，來使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。

本主題將引導您設定您的環境，以建立您自己的新應用程式。

-   [必要條件](#prerequisites)
-   [選擇性](#optional)
-   [設定您的開發環境](#configuring-your-development-environment)
-   [另請參閱](#see-also)

## <a name="prerequisites"></a>必要條件


您的開發系統必須使用下列軟體︰

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) 作業系統
-   [適用於 Windows 8.1 的 Windows 軟體開發套件 (SDK)](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 或以上版本，或 Visual Studio Express 2012 (適用於 Windows 8.0/8.1 的 Windows SDK 隨附)。
-   適用於 Windows 市集應用程式的 MS RMS SDK 4.2 套件。 如需詳細資訊，請參閱[開始使用](get-started.md)。
-   驗證程式庫︰建議您使用 [Azure AD 驗證程式庫](https://msdn.microsoft.com/en-us/library/jj573266.aspx)和其他可使用的驗證程式庫。

如需 API 更新、裝置和環境資訊、版本資訊和常見問題集 (FAQ) 的相關資訊，請參閱[最新消息](release-notes.md)。

## <a name="optional"></a>選用

我們的 UI 程式庫提供可重複使用的 UI，適用於不想要建立其自己的自訂 UI 之開發人員的耗用和保護作業 - [適用於 Windows 市集應用程式的 UI 程式庫](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)。 我們也提供 Windows 市集應用程式範例應用程式- [適用於 Windows 市集的 RMS 範例應用程式](https://github.com/AzureADSamples/rms-samples-for-windowsstore)。

## <a name="configuring-your-development-environment"></a>設定您的開發環境


-   開啟 Visual Studio。
-   依序按一下 [檔案]、[新增]，然後按一下 [專案]。
-   在 [新增專案] 對話方塊中，按一下 [Visual C\#]，並選取 [空白應用程式 (Windows)]，然後按一下 [確定]。

    ![建立新專案](../media/winrtsetup-newproj.png)

-   在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [新增參考] 以開啟 [新增參考] 對話方塊。

    ![新增參考](../media/winrtsetup-addref.png)

-   在 [新增參考] 對話方塊中，按一下 [瀏覽]，選取位於您解壓縮 SDK 封裝的資料夾中的 *Microsoft.RightsManagement.dll* 檔案。
-   **受管理的應用程式** - 若要建置受管理的應用程式，必須新增此參考，並依序選取 [Windows 8.1] -&gt; [延伸模組] 及 [Windows Visual C++ Runtime Package for Windows] 核取方塊

    ![新增擴充功能](../media/winrtsetup-refmngr.png)

-   **新增功能** - 您的應用程式將需要使用 SDK 的「網際網路 (用戶端和伺服器)」功能。 若要將這項功能加入您的應用程式，請開啟專案中的 *Package.appxmanifest* 檔案，瀏覽至 [功能] 索引標籤以新增功能。

您現在已準備好建立您自己的新 Windows 市集應用程式。

### <a name="see-also"></a>另請參閱

[開始使用](get-started.md)

[新功能](release-notes.md)

[開發人員詞彙及概念](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows API 參考](https://msdn.microsoft.com/library/dn891914.aspx)



<!--HONumber=Nov16_HO1-->


