---
title: "iOS 和 OS X 設定 | Azure RMS"
description: "iOS 和 OS X 應用程式可以藉由使用 AAD RM，以使用 RMS SDK 4.2 在其應用程式中啟用整合的資訊保護。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 80d79ead119b5dbe86d94f979742ecc2b62d1ef9


---

# iOS 和 OS X 設定

iOS 和 OS X 應用程式可以藉由使用 Azure Rights Management (Azure RMS)，使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。

本主題將引導您設定您的環境，以建立您自己的新應用程式。

**注意**  這個 SDK 不支援 iPod Touch。


-   [必要條件](#prerequisites)
-   [選用](#optional)
-   [設定您的開發環境](#configuring-your-development-environment)
-   [另請參閱](#see-also)

## 必要條件

建議您在開發系統上使用下列軟體︰

-   所有 iOS 開發都需要 OS X。
-   Xcode 6.0 版和更新版本

    Xcode 可透過 [Mac App Store](https://developer.apple.com/technologies/mac/) 取得。

-   適用於 iOS 和 OS X 的 MS RMS SDK 4.2 套件。如需詳細資訊，請參閱[開始使用](get-started.md)。

    此 SDK 可以用來開發 iOS 7.0 和 OS X 10.8 及更新版本。

-   驗證程式庫︰建議您使用 [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。 不過，也可以使用其他支援 OAuth 2.0 的驗證程式庫。

    如需詳細資訊，請參閱 [ADAL for iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) 或 [ADAL for OS X](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)

如需 API 更新、版本資訊和常見問題集 (FAQ) 等相關資訊，請參閱[最新消息](release-notes.md)。

## 選用

我們的 UI 程式庫提供可重複使用的 UI，適用於不想要建立其自己的自訂 UI 之開發人員的耗用和保護作業 - [iOS 的 UI 程式庫與範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-ios)。

## 設定您的開發環境

-   若要建立新專案，請在 [檔案] 功能表上按一下 [新增]，然後按一下 [專案]。
-   選取 [單一檢視應用程式]。

    ![建立新的專案](../media/iOS-Project.png)

-   輸入新專案的名稱和識別碼。

    ![命名您的專案](../media/iOS-project-options.png)

-   按 [下一步]，然後選取專案的位置。
-   若要新增 iOS 架構的 **MSRightsManagement**，請從 SDK 安裝資料夾拖曳 .framework 資料夾到 [專案導覽器] 的 [架構] 區段。

    ![設定位置](../media/ios-add-dependencies-01a.png)

-   選取 [建立任何新增資料夾的群組] 選項按鈕，然後清除 [將項目複製到目的地群組資料夾 (如果必要)] 核取方塊。

    這個動作會維護參考至 SDK 安裝資料夾，而不是建立複本。

    ![設定 SDK 安裝資料夾的參考](../media/iOS-create-groups.png)

-   若要新增 MS RMS SDK 4.2 至資源配套，請從 MSRightsManagement.framework/Resources 資料夾將 MSRightsManagementResources.bundle 檔案拖曳到 [專案導覽器] 的 [架構] 區段。

    ![新增資源配套](../media/iOS-add-resource-bundle-02a.png)

-   如同您在複製架構時的執行內容，請選取 [建立任何新增資料夾的群組] 選項按鈕，然後清除 [將項目複製到目的地群組資料夾 (如果必要)] 核取方塊。
-   SDK 會依賴其他架構，包括︰**CoreData**、**MessageUI**、**SystemConfiguration**、**Libresolv** 和 **Security**。 若要新增這些架構，請瀏覽至目標之 [摘要] 窗格的 [連結架構與程式庫] 區段中，並展開該區段以將其新增。

    **UIKit** 和 **Foundation** 架構是必要項，而且根據預設通常會出現。

    ![新增資源](../media/iOS-add-libraries.png)

-   新增 **-ObjC** 旗標至目標 [建置設定] 中的 [其他連結器旗標]。

    ![新增組建設定](../media/iOS-linker-flags.png)

-   現在您的 [專案導覽器] 應該如此樹狀結構所示。

    ![檢閱專案](../media/iOS-verify-setup-01a.png)

-   您現在已準備好建立您自己的新 iOS/OS X 應用程式。

### 另請參閱

* [開始使用](get-started.md)

* [新功能](release-notes.md)

* [開發人員詞彙和概念](core-concepts.md)

* [iOS / OS X API 參考](/information-protection/sdk/4.2/api/ios/ios)

 

 






<!--HONumber=Oct16_HO1-->


