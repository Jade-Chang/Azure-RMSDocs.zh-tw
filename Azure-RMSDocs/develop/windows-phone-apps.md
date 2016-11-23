---
title: "Windows Phone 設定 | Azure RMS"
description: "Windows Phone 應用程式可以使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: dc452dac3a86cd9cc39127d5a29106ae87ba94be
ms.openlocfilehash: 790f0d847c57b9e13d9074298b3e89584dc24760


---

# <a name="windows-phone-setup"></a>Windows Phone 設定


Windows Phone 應用程式可以藉由使用 Azure Active Directory Rights Management (AAD RM)，來使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。

本主題將引導您設定您的環境，以建立您自己的新應用程式。

-   [必要條件](#prerequisites)
-   [設定您的開發環境](#configuring-your-development-environment)
-   [另請參閱](#see-also)

## <a name="prerequisites"></a>必要條件


您的開發系統必須使用下列軟體︰

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) 作業系統。
-   [Windows Phone 8.1 開發工具 (SDK)](http://dev.windowsphone.com/en-us/downloadsdk)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 或以上版本，或 Visual Studio Express 2012 (隨附於 Windows Phone SDK 8.0/8.1)
-   適用於 Windows Phone 的 MS RMS SDK 4.2 套件。 如需詳細資訊，請參閱[開始使用](get-started.md)。
-   驗證程式庫︰建議您使用 [Azure AD 驗證程式庫](https://msdn.microsoft.com/en-us/library/jj573266.aspx)和其他可使用的驗證程式庫。

如需 API 更新、裝置和環境資訊、版本資訊和常見問題集 (FAQ) 的相關資訊，請參閱[最新消息](release-notes.md)。

檢閱 Windows Phone 開發人員中心的 [Windows Phone 開發](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)指南中的資訊。

## <a name="configuring-your-development-environment"></a>設定您的開發環境


-   開啟 *Visual Studio*。
-   按一下 [檔案]。 在 [檔案] 功能表上按一下 [新增]，然後按一下 [專案]。
-   在 [新增專案] 對話方塊中，依序選取 [Visual C\#] 和 [空白應用程式 (Windows Phone)]，然後按一下 [確定]。

    ![建立新專案](../media/wpsetup-newproj.png)

-   在 [方案總管] 中，以滑鼠右鍵按一下您的專案，然後選取 [加入參考] 以開啟 [加入參考] 對話方塊。

    ![新增參考](../media/wpsetup-addref.png)

-   按一下 [加入參考] 對話方塊左側的 [瀏覽]，然後選取位於您解壓縮封裝的資料夾中的 *Microsoft.RightsManagment.dll* 檔案。
-   **受管理的應用程式** - 若要建置受管理的應用程式，必須新增此參考，並依序選取 [Windows 8.1] -&gt; [延伸模組] 及 [Windows Visual C++ Runtime Package for Windows] 核取方塊

    ![新增擴充功能](../media/wpsetup-refmngr.png)

-   **加入功能** - 您的應用程式將需要「網際網路 (用戶端和伺服器)」功能，才能使用 SDK。 若要將這項功能加入您的應用程式，請開啟專案中的 *Package.appxmanifest* 檔案，瀏覽至 [功能] 索引標籤以新增功能。

您現在已準備好建立您自己的新 Windows Phone 應用程式。

### <a name="see-also"></a>另請參閱

[開始使用](get-started.md)

[新功能](release-notes.md)

[核心概念](core-concepts.md)

[Windows Phone 開發](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)

[Windows API 參考](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows Phone SDK](http://dev.windowsphone.com/en-us/downloadsdk)

 

 






<!--HONumber=Nov16_HO1-->


