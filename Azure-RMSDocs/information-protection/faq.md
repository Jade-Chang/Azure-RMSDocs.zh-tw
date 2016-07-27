---
title: "Azure Information Protection 預覽的常見問題集 | Azure Information Protection"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e60cd910a8e995a2681d7eb87a13f815183d9124
ms.openlocfilehash: 846578a84df383821a64d32ce6dd69290a5fdee9


---

# Azure Information Protection 預覽的常見問題集

*適用於：Azure Information Protection 預覽*

對 Azure Information Protection 的預覽版本有疑問？  看看此處是否有解答。 

此清單會隨著某些資訊移至主要文件而經常更新，我們也會包含從客戶收到的新問題。 

## 我可以用預覽版本的 Azure Information Protection 來做什麼，目前有哪些限制？

此預覽版本將 Information Protection 列加入 Microsoft Office 應用程式，讓您檢視和修改指派給資料的分類標籤。 分類可以手動完成，或是自動套用，這也是建議您的方式。 針對您指定的分類，可以使用 Azure Rights Management 範本來保護資料。  

分類標籤和行為是在 Azure 入口網站中設定。 您可以使用預設的內建原則，非常快速地評估 Azure Information Protection，或是完全自訂您自己的原則。 您可以變更分類標籤色彩、名稱和使用者看到的順序。 您也可以設定工具提示和分類的視覺標記，例如頁首、頁尾或浮水印。

請嘗試我們的快速入門教學課程，在短短幾分鐘內看到此運作︰[Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)。

請注意，預覽可讓您試用新的 **Premium P2 服務方案**，而一些進階功能，例如自動與建議標記，在正式運作時可能無法在您目前的方案使用。 如需不同服務方案 (Azure Information Protection Premium P1 和 Azure Information Protection Premium P2) 的詳細資訊，請參閱下列部落格文章：[Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/) (企業行動力 + 安全性簡介)。

此預覽版本有下列限制。 請留意 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格) 上的公告，以及我們的 [Yammer 網站](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)，了解其他特性與功能的提供時機：

- 針對分類和標記沒有任何集中式的記錄。

- 標籤名稱和工具提示僅提供英文版支援。

- 自動分類的條件必須為片語或模式。

- 無法從 Windows 檔案總管分類檔案。

- 目前尚不支援行動裝置 (iOS 和 Android) 和 Mac 電腦的 Office 應用程式和 Office Web 應用程式 (Office Online)。

- 沒有與 Exchange Online 或 SharePoint Online 的整合。

- 沒有合作夥伴和開發人員使用的 SDK。

## 我需要什麼訂用帳戶才能試用 Azure Information Protection？

針對預覽版本，您可以使用包含 Azure Rights Management 的任何訂用帳戶。 所有地區均可使用 Azure Information Protection。 如需可用訂用帳戶和免費試用連結的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。

若要在 Azure 入口網站中設定 Azure Information Protection 原則，您必須有 Azure 訂用帳戶。 如果您的組織尚無 Azure 訂用帳戶，您可以註冊免費試用以取得訂用帳戶：移至 [Azure 快速入門](https://account.windowsazure.com/organization)頁面，並遵循指示進行。

訂用帳戶需求的任何變更將會公告於 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格)。

## 如果 Azure Information Protection 現在是公開預覽版本，為什麼我在 Azure 入口網站找不到它？

目前，您必須使用此連結才能在入口網站中看到 Azure Information Protection︰https://portal.azure.com/?Microsoft_Azure_InformationProtection=true

然後在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 "Information Protection"。 從結果中，選取 [Azure Information Protection]。

## 我需要是全域管理員才能嘗試 Azure Information Protection 預覽嗎？

僅限預覽版本，Azure 已驗證的任何使用者都可以在 Azure 入口網站中看到及設定其租用戶的 Azure Information Protection 原則。

如果您在安裝 [Azure Information Protection 用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)時選取安裝示範原則的選項，您甚至不需要登入入口網站即可嘗試預覽。 示範原則會在本機安裝 Azure Information Protection 的預設原則，因此您可以嘗試為文件和電子郵件加上標籤，但是若您不登入 Azure 入口網站將無法變更或新增標籤。 

如果您想要保護您分類和標記的文件和電子郵件，且尚未啟用 Azure Rights Management，則啟動程序需要特殊的系統管理員權限。 如需詳細資訊，請參閱[僅有全域管理員才能設定 Azure RMS，或是我可以將此作業委派給其他系統管理員？](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)


## Azure Information Protection 支援內部部署與混合式案例嗎？

Azure Information Protection 是以雲端為基礎的解決方案。 如果您對混合式案例有興趣，請連絡 Information Protection 團隊，請寄送電子郵件至 askipteam@microsoft.com。

## Azure Information Protection 支援哪些用戶端平台和應用程式？

這現在已記錄，而且會在 [Azure Information Protection 需求](requirements-azure-infoprotect.md)中更新。


## 電腦如何從 Azure Information Protection 取得原則資訊，以及它多久重新整理一次？

每次使用者開啟 Office 應用程式時，Azure Information Protection 用戶端便會檢查是否有新版的 Azure Information Protection 原則。 如果有更新的版本，用戶端會使用 HTTPS 連結下載來保護資料。 

如果 Azure Information Protection 原則更新時應用程式已經載入，您必須關閉再重新開啟應用程式，才能取得最新版的原則。

## 檔案可以儲存在何處以便使用 Azure Information Protection？ 

因為 Azure Information Protection 會將持續性的標籤和保護套用到檔案和電子郵件，所以檔案儲存位置並不重要。

## 我只能分類新資料嗎？還是我也可以分類現有的資料？

針對新內容及現有內容的變更而儲存文件和傳送電子郵件時，Azure Information Protection 原則動作便會生效。 

如果您已儲存要分類的檔案，那麼只要在您的 Office 應用程式中開啟並儲存它們。 

目前，您無法大量掃描並套用分類，且必須在 Office 應用程式中開啟並儲存每份文件。 

## 可以使用 Azure Information Protection 只進行分類，而不強制執行加密和限制使用權限嗎？

可以。 您可以設定只套用標籤的 Azure Information Protection 原則。 事實上，我們預期對於您只需要保護一部分需要特殊資料管理之文件或電子郵件的部署網路而言，這是大多數的情況。

## 自動分類如何運作？

在 Azure 入口網站中，您可以使用預先定義的模式，例如「信用卡號碼」或「美國社會安全碼」。 或者，您可以定義自訂字串或模式，作為自動分類的條件。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。 

分類的精確度取決於您如何設定分類規則，分類規則是以條件為基礎。 目前，條件支援文字模式和規則運算式。 如需預覽期間提供之每項選項的說明，以及供您測試的一些建議範例，請參閱 Yammer 文章 [Description of content matching for our pre-define Information types](https://www.yammer.com/askipteam/#/Threads/show?threadId=737163344) (預先定義之資訊類型的內容比對描述)。 儲存文件或傳送電子郵件時，會執行偵測。

為了獲得最佳的使用者體驗，及確保業務持續性，我們建議您從使用者建議動作開始，而不要從完全自動動作開始。 這可讓您的使用者能夠接受標記或保護動作，或是覆寫這些建議。   

## Azure Information Protection 可以提示使用者自行分類檔案，而不要使用自動分類嗎？ 

可以。 使用 Azure 入口網站設定是否要使用自動分類，或對使用者提出建議，方法是將選項 [Select how this label is applied: automatically or recommended to user] (選取此標籤的套用方式︰自動或建議使用者) 設定為 [建議]。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。

## 可以強制分類所有文件都？

可以。 如果您需要使用者分類他們儲存的所有檔案都，請在 Azure 入口網站中將選項 [All documents and emails must have a label] (所有文件和電子郵件必須有標籤) 設定為 [開啟]。 

## 可以從檔案移除分類嗎？

可以。 若要從檔案移除分類，請在 Office 應用程式中開啟檔案，然後依序按一下 Information Protection 列中的**編輯標籤**圖示、**移除標籤**圖示，再按一下 [確定] 來確認您的動作。 


## 我可以提示使用者證明他們為何要變更分類層級嗎？

可以。 若要確定使用者證明其分類變更，請在 Azure 入口網站中，將選項 [Users must provide justification when lowering the sensitivity level] (降低敏感度等級時，使用者必須提供理由) 設定為 [開啟]。 當他們這麼做時，其本機 Windows 事件記錄檔中會記錄動作和理由︰[應用程式] > [Microsoft Azure Information Protection]。

## 如何自動保護分類之後的內容？

在 Azure 入口網站中，您可以選取 Azure Rights Management 範本來根據您指定的分類層級自動保護內容。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。

## 檔案可以分類在兩個不同的分類中嗎？

如有需要，您可以建立子標籤，更明確地描述特定敏感度標籤的子類別。 比方說，主體標籤 [密碼] 可能會包含子標籤，例如 [密碼 - 法務] 和 [密碼 - 財務]。 您接著可以套用不同的分類視覺標記和不同的 Rights Management 範本給不同的子標籤。

雖然您目前可以設定視覺標記、保護，以及兩個層級的條件，不過當您使用子層級時，請只在子層級上設定這些設定。 如果您在父標籤和其子層級上設定相同的設定，子層級設定的優先順序較高。

## DLP 方案和其他應用程式如何與 Azure Information Protection 整合？

因為 Azure Information Protection 使用持續性的中繼資料來進行分類，其中包括純文字標籤，所以 DLP 方案和其他應用程式可以讀取此資訊。 在檔案中，此中繼資料會儲存在自訂屬性。在電子郵件中，這項資訊是在電子郵件標頭中。

## Azure Information Protection 的文件追蹤和撤銷運作方式為何？

您使用 Azure Information Protection 來分類和保護的檔案，其文件追蹤方式與目前 Azure Rights Management 的方式相同。 如需詳細資訊，請參閱[當您使用 RMS 共用應用程式時，追蹤及撤銷文件](../rms-client/sharing-app-track-revoke.md)。

## Azure Information Protection 如何強制執行我所設定的原則？

當使用 Azure Rights Management 範本來保護文件時，會先驗證使用者，以確保其具有文件的權限，然後應用程式會強制執行使用權限原則。 

## Azure Information Protection 如何使用 Azure Active Directory？

Azure Information Protection 使用 Azure Active Directory 進行使用者驗證。

## 我可以控制哪些使用者可以使用 Azure Information Protection 來分類與保護內容嗎？

您可以藉由控制 Azure Information Protection 用戶端的發佈，來限制哪些使用者可以分類和保護資料。 

Azure Information Protection 分類的檔案和電子郵件，可以供任何使用者取用或編輯，而無論是否安裝 Azure Information Protection 用戶端。 

## 如何報告問題或傳送此預覽的意見反應？

如果在使用此預覽版本時發現問題，請在您的 Office 應用程式的 [首頁] 索引標籤的 [保護] 群組中，按一下 [保護]，然後按一下 [說明與意見反應]。 在 [Microsoft Azure Information Protection] 對話方塊中，按一下 [傳送意見反應]。 這樣會寄送電子郵件給 Information Protection 團隊，並自動從您的電腦附加記錄檔，以協助診斷問題。 

如果您有任何問題或意見，請使用 [Azure Information Protection Yammer 網站](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)。 

## 我的問題不在那裏怎麼辦？

首先，請確定您的問題不包含在 [Azure Information Protection 預覽公告](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/)中，這位於 Enterprise Mobility and Security 部落格上。

接著，請前往我們的 [Yammer 網站](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)，查看其他人是否已提出相同的問題。 如果沒有，則在該處張貼您的問題。







<!--HONumber=Jul16_HO3-->


