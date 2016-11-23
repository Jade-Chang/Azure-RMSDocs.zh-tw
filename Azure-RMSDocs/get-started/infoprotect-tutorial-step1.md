---
title: "快速入門教學課程步驟 1 | Azure Information Protection"
description: "簡介教學課程的步驟 1，可讓貴組織快速試用 Microsoft Azure Information Protection，需時約 30 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: b23022c5fbec3d4f6f19ab5017ecf9badf01a9e7
ms.openlocfilehash: 247ab8dd5a47f9370f03fbd5badd7c78784d20b5


---

# 步驟 1：啟動 Rights Management 服務
 
>*適用於：Azure Information Protection*

> [!NOTE]
>如果您已為租用戶啟用 Azure Rights Management Service，請直接前往[下一個步驟](infoprotect-tutorial-step2.md)。 

啟用 Azure Rights Management Service 之後，您就可以保護組織最敏感的文件和電子郵件，並在您與其他人共用時追蹤使用狀況。 啟用此服務的方法有許多種，包括使用 Windows PowerShell，以及巡覽管理入口網站。

在本教學課程中，我們將直接前往 Office 365 系統管理員的啟用頁面，此頁面在 Office 365 傳統入口網站和 Office 365 系統管理中心預覽上會相同。 

如果您想要從 Office 365 系統管理中心巡覽至此頁面，而不是直接前往此頁面，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md) 中的完整指示。 如果您具有 Azure 入口網站的存取權，但沒有 Office 365 管理入口網站的存取權，也可以使用這些完整指示。

## 啟用 Rights Management Service

1. 開啟新的瀏覽器視窗，並直接前往 Office 365 系統管理員的 [Rights Management 啟用頁面](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)。
    
    如果系統提示您登入，請使用 Office 365 的全域管理員帳戶。

2. 在 [Rights Management] 頁面上，按一下 [啟動]。

3. 出現 [您要啟動 Rights Management 嗎?] 提示時，按一下 [啟動]。

    現在，您應該會看到 [Rights Management 已啟動] 及用來停用的選項 (您可能需要手動重新整理頁面)

    此時請不要按 **[進階功能]**。 這會帶您到 Azure 傳統入口網站供您設定自訂範本，但本教學課程不需要用到範本。 相反地，您可以關閉此頁面。

在完成本教學課程的第一個步驟中，您只需要做到這個程度就行。 針對生產部署，您可能會想要額外設定自訂範本，或是用來取代兩個預設 Azure Rights Management 範本。 但本教學課程不需要用到自訂範本，因此您已經可以進入步驟 2。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於啟用 Rights Management|[啟用 Azure Rights Management](../deploy-use/activate-service.md)|
|關於預設範本以及如何建立全新自訂範本|[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 簡介](infoprotect-quick-start-tutorial.md)
[步驟 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Sep16_HO4-->


