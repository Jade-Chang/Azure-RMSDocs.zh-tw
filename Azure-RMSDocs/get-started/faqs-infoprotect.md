---
title: "分類和標記的常見問題集 | Azure Information Protection"
description: "對 Azure Information Protection 的預覽版本有疑問？ 看看此處是否有解答。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: a05b33f5085bf31d4ef1e6a606322fda8b0febe7


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection 中分類和標記的常見問題集

>*適用對象︰Azure 資訊保護、Office 365*

對 Azure Information Protection 特有的分類和標籤有疑問？  看看此處是否有解答。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>我可以在 Azure Information Protection 中使用分類功能來執行哪些工作？

Azure Information Protection 用戶端新增 Information Protection 列到 Microsoft Office 應用程式，讓您檢視和修改指派給資料的分類標籤。 分類可以手動完成，或是自動套用，這也是建議您的方式。 針對您指定的分類，可以使用 Rights Management Service 來保護資料。  

分類標籤和行為是在 Azure 入口網站中設定。 您可以使用預設的內建原則，非常快速地評估 Azure Information Protection，或是完全自訂您自己的原則。 您可以變更分類標籤色彩、名稱和使用者看到的順序。 您也可以設定工具提示和分類的視覺標記，例如頁首、頁尾或浮水印。

請嘗試我們的快速入門教學課程，在短短幾分鐘內看到此運作︰[Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)。

目前版本有下列限制。 請留意 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection) (Enterprise Mobility and Security 部落格) 上的公告，以及我們的 [Yammer 網站](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)，以了解其他特性與功能可供使用的時機：

- 您可以只將標籤套用至 Office 檔案類型及 Outlook 電子郵件訊息。

- 所有已安裝 Azure 資訊保護用戶端的使用者皆可看見 Office 增益集的標籤。

- 標籤名稱和工具提示中只有一種語言支援。

- 無法從 Windows 檔案總管分類檔案。

- 針對分類和標記沒有任何集中式的記錄。

- 自動分類的條件必須為片語或模式。

- 目前尚不支援行動裝置 (iOS 和 Android) 和 Mac 電腦的 Office 應用程式和 Office Web 應用程式 (Office Online)。

- 沒有與 Exchange Online 或 SharePoint Online 的整合。

- 沒有合作夥伴和開發人員使用的 SDK。

## <a name="do-i-need-to-be-a-global-admin-to-try-azure-information-protection"></a>我需要是全域管理員才能試用 Azure Information Protection 嗎？

若要設定 Azure Information Protection 原則，您必須以 Azure Active Directory 的全域管理員身分登入 Azure 入口網站。

不過，如果您在安裝 [Azure Information Protection 用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)時選取安裝示範原則的選項，您不需要登入入口網站，就能查看及試用標記功能。 示範原則會在本機安裝 Azure Information Protection 的預設原則，因此您可以嘗試為文件和電子郵件加上標籤，但是若您不登入 Azure 入口網站將無法變更或新增標籤。 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Azure 入口網站中哪個選項是 P1 或 P2？

如需查看 **Azure 資訊保護 Premium 1** (P1) 訂用帳戶與 **Azure 資訊保護 Premium 2** (P2) 訂用帳戶分別包含哪些功能，請參閱 Azure 資訊保護網站的[功能清單](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection 支援內部部署與混合式案例嗎？

Azure Information Protection 是以雲端為基礎的解決方案。 如果您有興趣在混合式案例中部署 Azure Information Protection，請將電子郵件傳送至 askipteam@microsoft.com 來連絡 Information Protection 小組。

## <a name="how-do-computers-get-the-policy-information-from-azure-information-protection-and-how-often-is-it-refreshed"></a>電腦如何從 Azure Information Protection 取得原則資訊，以及它多久重新整理一次？

每次使用者開啟 Office 應用程式時，Azure Information Protection 用戶端便會檢查是否有新版的 Azure Information Protection 原則。 此外，Office 應用程式會每 24 小時檢查一次。 如果有更新的版本，用戶端會使用 HTTPS 連結下載來保護資料。 

如果在新的 Azure Information Protection 原則發佈時，已載入多個 Office 應用程式執行個體，您必須關閉所有執行個體以取得最新版的原則。 例如，您開啟了兩個 Word 文件，並只想要在一個文件中測試更新的 Azure Information Protection 原則：請將兩個 Word 文件都關閉，並重新開啟您想要搭配最新原則使用的文件。

## <a name="where-can-files-be-stored-to-use-azure-information-protection"></a>檔案可以儲存在何處以便使用 Azure Information Protection？ 

因為 Azure Information Protection 會將持續性的標籤和保護套用到檔案和電子郵件，所以檔案儲存位置並不重要。

## <a name="can-i-classify-only-new-data-or-can-i-also-classify-existing-data"></a>我只能分類新資料嗎？還是我也可以分類現有的資料？

針對新內容及現有內容的變更而儲存文件和傳送電子郵件時，Azure Information Protection 原則動作便會生效。 

如果您已儲存要分類的檔案，那麼只要在您的 Office 應用程式中開啟並儲存它們。 

目前，您無法大量掃描並套用分類，且必須在 Office 應用程式中開啟並儲存每份文件。 

## <a name="can-i-use-azure-information-protection-for-classification-only-without-enforcing-encryption-and-restricting-usage-rights"></a>可以使用 Azure Information Protection 只進行分類，而不強制執行加密和限制使用權限嗎？

可以。 您可以設定只套用標籤的 Azure Information Protection 原則。 事實上，我們預期對於您只需要保護一部分需要特殊資料管理之文件或電子郵件的部署網路而言，這是大多數的情況。

## <a name="how-does-automatic-classification-work"></a>自動分類如何運作？

在 Azure 入口網站中，您可以使用預先定義的模式，例如「信用卡號碼」或「美國社會安全碼」。 或者，您可以定義自訂字串或模式，作為自動分類的條件。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。 

分類的精確度取決於您如何設定分類規則，分類規則是以條件為基礎。 目前，條件支援文字模式和規則運算式。 如需預覽期間所提供選項的個別說明，以及一些供您測試的建議範例，請參閱[如何設定適用於 Azure Information Protection 的自動與建議分類條件](../deploy-use/configure-policy-classification.md)。 儲存文件或傳送電子郵件時，會執行偵測。

為了獲得最佳的使用者體驗，及確保業務持續性，我們建議您從使用者建議動作開始，而不要從完全自動動作開始。 這可讓您的使用者能夠接受標記或保護動作，或是覆寫這些建議。   

## <a name="can-azure-information-protection-prompt-users-to-classify-files-themselves-rather-than-use-automatic-classification"></a>Azure Information Protection 可以提示使用者自行分類檔案，而不要使用自動分類嗎？ 

可以。 使用 Azure 入口網站設定是否要使用自動分類，或對使用者提出建議，方法是將選項 [Select how this label is applied: automatically or recommended to user] (選取此標籤的套用方式︰自動或建議使用者) 設定為 [建議]。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。  

## <a name="can-i-force-all-documents-to-be-classified"></a>可以強制分類所有文件都？

可以。 如果您需要使用者分類他們儲存的所有檔案都，請在 Azure 入口網站中將選項 [All documents and emails must have a label] (所有文件和電子郵件必須有標籤) 設定為 [開啟]。 

## <a name="can-i-remove-classification-from-a-file"></a>可以從檔案移除分類嗎？

可以。 若要從檔案移除分類，請在 Office 應用程式中開啟檔案，然後依序按一下 Information Protection 列中的**編輯標籤**圖示、**移除標籤**圖示，再按一下 [確定] 來確認您的動作。 


## <a name="can-i-prompt-users-to-justify-why-they-are-changing-the-classification-level"></a>我可以提示使用者證明他們為何要變更分類層級嗎？

可以。 若要確認使用者為變更分類提供正當理由，請在 Azure 入口網站中，將選項 [使用者必須提供理由才能降低分類標籤、移除標籤或移除保護] 設為 [開啟]。 當他們這麼做時，其本機 Windows 事件記錄檔中會記錄動作和理由︰[應用程式] > [Microsoft Azure Information Protection]。

## <a name="how-can-i-automatically-protect-the-content-after-its-been-classified"></a>如何自動保護分類之後的內容？

在 Azure 入口網站中，您可以選取 Rights Management 範本來根據您指定的分類層級自動保護內容。

您會在 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)中此動作的範例。 如需詳細資訊，請參閱[如何設定標籤以套用 Rights Management 保護](../deploy-use/configure-policy-protection.md)。

## <a name="can-a-file-be-classified-with-two-different-classifications"></a>檔案可以分類在兩個不同的分類中嗎？

如有需要，您可以建立子標籤，更明確地描述特定敏感度標籤的子類別。 例如，主體標籤 [密碼] 可能會包含子標籤，例如 [密碼\法務] 和 [密碼\財務]。 您接著可以套用不同的分類視覺標記和不同的 Rights Management 範本給不同的子標籤。

雖然您目前可以設定視覺標記、保護，以及兩個層級的條件，不過當您使用子層級時，請只在子層級上設定這些設定。 如果您在父標籤和其子層級上設定相同的設定，子層級設定的優先順序較高。

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>標記電子郵件時，會有任何附件自動得到相同標籤嗎？

否。 當您標記有附件的電子郵件訊息時，附件不會繼承相同標籤。 附件會維持沒有標籤，或保留另外套用的標籤。 不過，如果電子郵件的標籤套用了保護，保護就會套用至附件。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP 方案和其他應用程式如何與 Azure Information Protection 整合？

因為 Azure Information Protection 使用持續性的中繼資料來進行分類，其中包括純文字標籤，所以 DLP 方案和其他應用程式可以讀取此資訊。 在檔案中，此中繼資料會儲存在自訂屬性。在電子郵件中，這項資訊是在電子郵件標頭中。

## <a name="how-does-document-tracking-and-revocation-work-for-azure-information-protection"></a>Azure Information Protection 的文件追蹤和撤銷運作方式為何？

您使用 Azure Information Protection 來分類和保護的檔案，其文件追蹤方式可搭配 Azure Rights Management 保護和 RMS 共用應用程式使用。 您也可以使用 Azure Information Protection 用戶端來存取文件追蹤網站 (版本 1.0.233 或更新版本)： 

- Office 應用程式中，在 [首頁] 索引標籤的 [保護] 群組中，按一下 [保護] >  [追蹤使用狀況] 。 

如需詳細資訊，請參閱[當您使用 RMS 共用應用程式時，追蹤及撤銷文件](../rms-client/sharing-app-track-revoke.md)。

## <a name="can-i-control-which-users-can-use-azure-information-protection-to-classify-and-protect-content"></a>我可以控制哪些使用者可以使用 Azure Information Protection 來分類與保護內容嗎？

您可以藉由控制 Azure Information Protection 用戶端的發佈，來限制哪些使用者可以分類和保護資料。 

Azure Information Protection 分類的檔案和電子郵件，可以供任何使用者取用或編輯，而無論是否安裝 Azure Information Protection 用戶端。 

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>如何針對 Azure Information Protection 回報問題或傳送意見反應？

如果您有 Azure Information Protection 的問題，而且正在使用最新版本的用戶端︰在 Office 應用程式之 [常用] 索引標籤的 [保護] 群組中，按一下 [保護]，然後按一下 [說明與意見反應]。 在 [Microsoft Azure Information Protection] 對話方塊中，按一下 [傳送意見反應]。 這樣會寄送電子郵件給 Information Protection 團隊，並自動從您的電腦附加記錄檔，以協助診斷問題。 

如果您有任何問題或意見，請使用 [Azure Information Protection Yammer 網站](https://www.yammer.com/askipteam/)。 


<!--HONumber=Nov16_HO2-->


