---
title: "Azure Rights Management 的快速部署指南 | Azure RMS"
description: "協助您快速部署和使用 Azure Rights Management (Azure RMS) 以保護組織資料的指南。 從選擇要實作的特定案例清單開始。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 81426cf43f31625c6e83d443fa925f6426eb89da
ms.openlocfilehash: 715290d2417df3b386d8e5b8a784e964355d4e15


---

# Azure Rights Management 的快速部署指南

>*適用於︰Azure Rights Management、Office 365*

使用此指南以及**部署與使用**一節中的組態資訊，協助您藉由從要實作的特定案例清單中選擇，以快速部署與使用 Azure Rights Management (Azure RMS)。

這些案例包含系統管理員指示和隨附的使用者文件。 將文件 (指示或公告) 提供給使用者之前，您必須先針對業務需求和現有工作流程自訂文件。 一組指示或公告範例顯示最終使用者文件看起來應該如何。

每個案例都有一份需求清單，其中含有詳細資訊的連結可供您在需要時參閱，因此您可以按照任何順序單獨部署這些解決方案。

此處所列的案例是最受歡迎的範例。 因為 Azure RMS 可以用來保護組織內和跨組織的大量案例中的資訊，您可以定義您自己的案例，並使用相同的模型將它們部署到您的環境和您的使用者。 藉由把焦點放在特定情況，您的 Azure RMS 部署會更緊密符合業務目標。 此外，我們的經驗是，相較於「保護機密文件」等一般指引，使用者通常會更密切而有系統地遵循案例的特定指示。

在您制定這些解決方案之前，您可能會想要傳送廣泛的公告給使用者，讓他們知道某些變更即將推出，以協助保護公司資料，並且可能需要使用者進行一些變更。 範例通訊會包含在下表之後。

> [!NOTE]
> 如果您有關於本指南的問題或意見，請使用本頁面上的意見反應機制，或將電子郵件訊息傳送至 [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback)。

## Azure RMS 的案例
為了協助您更快速部署 Azure RMS 來解決特定商務問題，請選擇最緊密符合商務目標的案例，並在必要時採用它們。



**透過電子郵件將 Office 檔案安全地傳送給另一個組織中的使用者，同時可追蹤產生的存取情形 (企業對企業共同作業)。**

範例：

- 傳送價目表、藍圖或發行計劃給客戶

- 傳送派工單或行銷規格給供應商

- 傳送標單或詢價單 (RFQ) 給合作夥伴

請參閱：[案例 - 與其他組織的使用者共用 Office 檔案](scenario-share-office-file-externally.md)

**確定您對儲存在 SharePoint 文件庫中的文件保有控制權**

範例：

- 部門的試算表和報告。

- 設計文件或其他交付項目的跨小組共同作業

請參閱：[保留 SharePoint 中儲存之文件的控制權](scenario-sharepoint.md)

**主管可以透過電子郵件安全地交換機密資訊**

範例：

- 共用併購計劃

- 討論或宣傳法律議題

- 關於潛在解雇或其他敏感主題的資訊

請參閱：[案例 - 主管安全地交換機密資訊](scenario-executives-email.md)

**自動保護檔案伺服器上的所有檔案**

範例：

- 必須保留在內部以避免遺失智慧財產的 CAD 文件

- 必須保持機密不公開洩漏以維護競爭優勢的行銷促銷計劃和日期

請參閱︰[案例 - 保護檔案伺服器共用上的檔案](scenario-fci.md)

**嚴密保護最機密、最高商業影響的文件**

範例：

- 公司專屬的配方或公式資訊

- 高機密性的接管或合併計劃

- 自然資源探索資料

請參閱︰[案例 - 保護您最 &#40;少&#41; 的重要檔案](scenario-secure-most-valuable-files.md)

**安全地傳送公司機密電子郵件和附件**

範例：

- 公司願景聲明

- 組織圖、重組新聞或促銷宣告

- 公司原則資訊

請參閱︰[案例 - 傳送公司機密電子郵件](scenario-company-confidential-email.md)

**將持續的保護套用至工作資料夾中的 Office 檔案**

範例：

- 在本機編輯的公司機密專案 Word 文件

- 在本機建立的試算表，包含機密資料或高商業影響資料

- 在本機儲存的進行中 PowerPoint 簡報，不得在簡報完成之前遺漏或不小心與組織外部的人員共用簡報

請參閱︰[案例 - 將工作資料夾設定為持續保護](scenario-work-folders.md)




## 首度發行之前對使用者的宣告
您可以使用下列範例通訊訊息，讓使用者知道，部署 Azure RMS 表示有些變更正在進行。 複製並貼上下列文字，要從貴組織領導小組的某個人，最好是您的執行長，透過電子郵件傳送給所有使用者。 請考慮對這段文字進行任何變更，讓訊息與使用者和組織更有相關性。

![Azure RMS 快速部署的範例使用者文件橫幅](../media/AzRMS_ExampleBanner.png)

### 我們正在進行變更以保護資料
您是否曾經想要針對您不小心傳送給夥伴的文件封鎖其存取權？ 您想要知道是否有辦法知道哪些客戶已閱讀您所傳送的最新產品新聞嗎？ 您需要共用機密的產品資訊，而不需擔心資訊可能會傳送給不應該看到的人嗎？

您很快就可以達成上述目標，因為 IT 部門即將推出一些變更，可實作 Microsoft Azure Rights Management (Azure RMS) 做為企業資料保護解決方案。 許多解決方案會自動套用我們需要的保護，您不必採取任何其他動作。 但是，某些變更可能需要您以不同的方式執行一些動作，在這個情況下，IT 部門將會傳送資訊和指示給您，並在您有疑問或問題時，提供技術支援人員的支援。

例如，若要追蹤 (和必要時撤銷) 您共用的文件，您將使用文件追蹤網站︰

![Azure RMS 文件追蹤螢幕擷取畫面](../media/AzRMS_Tutorial_5_Screenshots.png)

若要查看其運作方式，請觀看這部 2 分鐘的影片︰[Azure RMS 文件追蹤和撤銷](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

此組織最重要的資產之一是它的資料—我們可以每天產生、儲存和使用的資料。 它讓我們擁有競爭優勢，並可幫助我們成功。 這就是為什麼它如此重要，我們要持續掌控資料，並確保不應該存取資料的人員無法存取。

我們正在實作的解決方案將協助我們保護重要資料，並提供您工具以持續控制該資料。 在我們實作這些變更期間，感謝您的合作。




<!--HONumber=Aug16_HO4-->


