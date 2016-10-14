---
title: "什麼是 Azure 資訊保護？ | Azure 資訊保護"
description: "Azure 資訊保護服務概觀。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: cd8a88e2-3555-4be2-9637-3cdee992f2c8
translationtype: Human Translation
ms.sourcegitcommit: 590f12e0c6c6122a6bc0a559940870c18f0e2d39
ms.openlocfilehash: 350a3cb877674208b4c560bb841135904aee1136


---

# 什麼是 Azure 資訊保護？

>*適用於：Azure 資訊保護*

Azure 資訊保護是雲端式解決方案，可協助組織分類、標記及保護其文件和電子郵件。 這可以由系統管理員定義規則和條件來自動完成、由使用者手動完成，或在提供建議給使用者的情況下由系統管理員搭配使用者的組合來完成。 

下圖顯示 Azure 資訊保護運作方式的範例。 系統管理員已設定規則來偵測敏感性資料 (在本例中為信用卡資訊)。 當使用者儲存包含信用卡資訊的 Word 文件時，會出現自訂工具提示，建議套用系統管理員所設定的特定標籤，以分類並選擇性地保護文件。 

![Azure 資訊保護的建議分類範例](../media/info-protect-recommend-callouts.png)

在您分類 (並選擇性地保護) 內容之後，您可以接著追蹤及控制內容的使用方式。 您可以分析資料流程以深入探索您的業務、偵測風險行為並採取矯正措施、追蹤文件的存取、防止資料外洩或不當使用，以及執行其他作業。

## 標籤如何套用分類

您可以使用 Azure 資訊保護標籤，將分類套用至文件和電子郵件。 當您這樣做時，即可隨時識別分類，無論資料的儲存位置或與誰共用。 持續性的標籤包括視覺標記，例如頁首、頁尾或浮水印。 中繼資料會以純文字加入檔案和電子郵件頁首，讓其他服務 (例如資料外洩防護解決方案) 可以識別分類並採取適當動作。 

例如，下列電子郵件訊息已分類為「內部」。 此標籤會加入作為電子郵件訊息的頁尾，這是給所有收件者的視覺指標，僅供內部使用，不應該傳送到組織外部。 此標籤也會嵌入電子郵件頁首，使電子郵件服務可以檢查此值，而無法建立稽核項目或傳送到組織外部。

![顯示 Azure 資訊保護分類的電子郵件頁尾和頁首範例](../media/example-email-footer-header.png)


## 如何保護資料

此保護技術使用 *Azure Rights Management* (通常縮寫為 Azure RMS)。 這項技術與 Office 365 及 Azure Active Directory 等其他 Microsoft 雲端服務和應用程式整合。 它也可以搭配使用您自己的企業營運系統應用程式與軟體廠商中的資訊保護解決方案，不論這些應用程式和解決方案是在內部部署環境還是雲端中。

這項保護技術使用加密、身分識別和授權原則。 與持續標籤類似，使用 Rights Management 所套用的保護會跟著文件和電子郵件，不受位置影響 - 不論是在貴組織內部或外部、網路、檔案伺服器及應用程式。 此資訊保護解決方案可讓您在與他人共用資料的情況下，依然能控管資料。

例如，您可以設定讓報表文件或銷售趨勢預測試算表僅供貴組織中的人員存取，以及控制該文件是否可供編輯、限制成唯讀或防止列印。 您也可以使用類似方式設定電子郵件，此外，還可以防止它們被轉寄或防止使用 [全部回覆] 選項。 只要使用「Rights Management 範本」，即可簡化這些保護工作並使工作變得有效率。

### Rights Management 範本

啟用 Azure Rights Management Service 之後，系統會為您建立兩個預設範本，以限制您組織中使用者的資料存取權。 您可以使用這些範本，立即協助防止資料從您的組織外洩。 您也可以設定套用更嚴格控制的自訂範本，來補充這些預設範本。

這些範本可以是標籤組態的一部分，以在特定標籤套用至文件 (或電子郵件訊息) 之後，對資料進行分類並自動提供保護。 使用者或系統管理員也可以在支援 Azure Rights Management 技術的產品和服務中選取這些範本。

此範例示範如何在從 Azure 入口網站設定 Azure 資訊保護原則時，選取標籤的範本：

![在 Azure 入口網站中選取範本的範例](../media/templates-infoprotection-callouts.png)

您可以從 Exchange 系統管理中心選取相同的範本，以設定 Exchange Online 郵件流程規則來支援 Azure Rights Management 技術：

![選取適用於 Exchange Online 範本的範例](../media/templates-exchangeonline-callouts.png)

如需 Azure Rights Management 保護的詳細資訊，請參閱[什麼是 Azure 資訊保護？](what-is-azure-rms.md)

## 與使用者工作流程整合

安裝 Azure 資訊保護用戶端之後，Azure 資訊保護會與使用者的現有工作流程整合。 此用戶端會將 Information Protection 列安裝到 Office 應用程式，如第一張圖片中所示。 Excel、PowerPoint 和 Outlook 中會加入相同的列。 例如：

![Excel 中的 Azure 資訊保護列範例](../media/excel2013-infoprotect-bar2.png)

此 Information Protection 列可讓使用者輕鬆選取正確分類的標籤，而且在必要情況下，這些標籤也可以自動保護其文件和電子郵件。

當使用者透過電子郵件共用其受保護的文件時，可以使用文件追蹤網站來監視存取這些文件的人員和時間。 如果他們懷疑誤用，也可以撤銷這些文件的存取權。


## Azure 資訊保護的資源

- 公告︰[Azure 資訊保護功能現已公開推出](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/04/azure-information-protection-is-now-generally-available/)

- 免費試用：[Enterprise Mobility + Security E5](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)

- 下載用戶端：[Azure 資訊保護用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)

- 常見問題集︰[Azure 資訊保護的常見問題集](../get-started/faqs.md)

- Yammer：[Azure 資訊保護](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)

- 視訊簡報：

    <iframe width="560" height="315" src="https://www.youtube.com/embed/N9Ip0m6d3G0" frameborder="0" allowfullscreen></iframe>


## 後續步驟

藉助 5 個步驟的 [Azure 資訊保護快速入門教學課程](../get-started/infoprotect-quick-start-tutorial.md)自行設定及查看 Azure 資訊保護。

想要知道 Azure 資訊保護或 Azure Rights Management 的其他名稱嗎？ 請參閱[服務的替代詞彙清單](azure-rms-aka.md)。


<!--HONumber=Oct16_HO1-->


