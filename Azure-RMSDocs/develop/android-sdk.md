---
title: "Android 設定 |Azure RMS"
description: "Android 應用程式可以使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 90c8c97c720c624ba8f1ca7703b6c79a66f77d08


---

# Android 設定

Android 應用程式可以藉由使用 Azure Active Directory Rights Management (AAD RM)，來使用 Microsoft Rights Management SDK 4.2 在其應用程式中啟用整合的資訊保護。

本主題將引導您設定您的環境，以建立您自己的新應用程式。

-   [必要條件](#prerequisites)
-   [選用](#optional)
-   [設定您的開發環境](#configuring-your-development-environment)
-   [另請參閱](#see-also)

## 必要條件

建議您在開發系統上使用下列軟體︰

-   Windows 或 OS X 作業系統以執行 [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 開發環境。
-   本指南假設您從 Eclipse Juno 4.2 開始使用 Eclipse SDK，並使用預設安裝。
-   Java 開始使用 Java 1.6。
-   [Android 開發人員工具 (ADT) 外掛程式](http://developer.android.com/sdk/installing/index.html)。 注意 - 系統可能會要求您重新啟動 Eclipse 以完成安裝。

     

-   適用於 Android 的 MS RMS SDK 4.2 套件。 如需詳細資訊，請參閱[開始使用](get-started.md)。

    此 SDK 可以用來開發 Android 4.0.3 (API 層級 15) 和更新版本中。

-   驗證程式庫︰建議您使用 [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。 不過，也可以使用其他支援 OAuth 2.0 的驗證程式庫。

    如需詳細資訊，請參閱 [Android 適用的 ADAL](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)。

    **注意**  如果您的應用程式將不會使用 ADAL 程式庫做為 OAuth 2.0 驗證程式庫，您應該檢閱這個 Android 指引，[某些 SecureRandom 想法](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html)。

     

如需 API 更新、版本資訊和常見問題集 (FAQ) 等相關資訊，請參閱[最新消息](release-notes.md)。

## 選用

我們的 UI 程式庫提供可重複使用的 UI，適用於不想要建立其自己的自訂 UI 之開發人員的耗用和保護作業 - [Android 的 UI 程式庫與範例應用程式](https://github.com/AzureAD/rms-sdk-ui-for-android)。

## 設定您的開發環境

**注意**  MS RMS SDK 4.2 預覽版本︰在此預覽版本中，尚未更新螢幕擷取畫面來顯示從 com/microsoft/protection 到 com/microsoft/rightsmanagment 之路徑名稱中的變更。 不過已更新文字。

 
-   開啟 Eclipse 開發環境。
-   若要建立新的 Android 應用程式專案，請在 [檔案] 功能表上，按一下 [新增]，按一下 [專案]，然後選取 [Android 應用程式專案]。

    ![建立新的 Android 應用程式](../media/Android-setup-01c.png)

-   輸入應用程式名稱。 專案名稱和套件名稱會根據應用程式名稱填入。
-   按 [下一步]，然後選取您想要建立工作區的地方。

    ![輸入應用程式名稱](../media/Android-setup-02a.jpg)

-   按 [下一步]，然後選取應用程式的圖示。

    ![選取應用程式的圖示](../media/Android-setup-03.png)

-   按 [下一步]，然後選取 [空白活動] 以建立活動。

    ![建立活動](../media/Android-setup-04.png)

-   按 [下一步]，並提供名稱給活動。 您可以將 *MainActivity* 保留為預設名稱，內含配置名稱 *activity\_main*。

    ![提供活動的名稱](../media/Android-setup-05a.jpg)

-   按一下 [完成] 。

    ![完成建立](../media/Android-setup-06.jpg)

-   已建立您的專案，以及主要活動類別 *MainActivity.java*。

**參考 SDK**

-   瀏覽至您在其中解壓縮 *adrms\_android\_sdk.zip* 的資料夾。 在「SDK > com > microsoft > rightsmanagement」資料夾中，請確定 *.classpath*、*.project* 和 *project.properties* 等檔案未標示為唯讀。
-   若要參考 SDK，您必須將它匯入工作區。

    在 Eclipse 中，按一下 [檔案]。 在 [檔案] 功能表上，按一下 [匯入]。 在 [匯入] 對話方塊中，選取 [Android / 現有 Android 程式碼至工作區]。

    ![將它匯入至工作區](../media/Android-setup-07.png)

-   按一下 [下一步] 。 瀏覽並選取您在其中解壓縮 *adrms\_android\_sdk.zip* 的資料夾。 SDK 應該會以 **com.microsoft.rightsmanagement** 出現在清單中。

    ![巡覽以選取資料夾](../media/Android-setup-08c.jpg)

-   當您按一下 [完成]，SDK 專案會顯示為您先前建立之應用程式的同層級。

    ![SDK 專案會顯示為您應用程式的同層級](../media/Android-setup-09.jpg)

-   以滑鼠右鍵按一下 [專案] 圖示，並檢視專案屬性。
-   瀏覽至 [Android] 索引標籤。
-   按一下 [新增]，然後選取工作區中的 *com.microsoft.rightsmanagement* 程式庫。

    ![新增程式庫](../media/Android-setup-10b.jpg)

-   按一下 [ **確定**]。

    由於 MS RMS SDK 4.2 會連接 AAD RM，所以必須授與應用程式 **INTERNET** 和 **ACCESS\_NETWORK\_STATE** 的權限。 若要這樣做，請在專案的根目錄中開啟 *AndroidManifest.xml* 檔案。

    若要新增權限，請按一下 [新增]，然後選取 [使用權限]。

    ![新增權限](../media/Android-setup-11d.jpg)

-   您可以藉由在文字編輯器檢視中檢視資訊清單，以確認資訊清單步驟。 請確定出現下列幾行︰


    <uses-sdk      android:minSdkVersion="15"      android:targetSdkVersion="19"/> <uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission/>


**注意**  SDK 會使用 *android.support.v4*

-   您現在已準備好建立您自己的新 Android 應用程式。

### 另請參閱

[開始使用](get-started.md)

[新功能](release-notes.md)

[開發人員詞彙和概念](core-concepts.md)

[Android API 參考](https://msdn.microsoft.com/library/dn758245.aspx)

 

 



<!--HONumber=Oct16_HO1-->


