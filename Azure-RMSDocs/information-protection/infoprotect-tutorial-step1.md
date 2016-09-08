---
title: "Azure Information Protection 快速入門教學課程步驟 1 | Azure Rights Management"
description: "簡介教學課程的步驟 1，可為組織快速試用 Microsoft Azure Information Protection，只有 4 個步驟，花費時間約 10 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 07/291/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: b608ee307bf7388ab7c7ed70cc1286db5df176c8


---

# 步驟 1：啟動 Rights Management 服務
 
>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

> [!NOTE]
>如果您只想要分類資料而不想使用 Azure Rights Management 保護它，或如果您已為您的租用戶啟用 Azure Rights Management - 請直接前往[下一步](infoprotect-tutorial-step2.md)。 

啟動 Azure Rights Management 時，您可以在分類最敏感的文件和檔案之後保護它們。 若要啟動 Azure Rights Management，您可以使用 Office 365 系統管理中心或是 Azure 傳統入口網站：

-   如果您有包含 Azure Rights Management 的 Office 365 訂閱，或是所擁有的 Office 365 訂閱雖然沒有 Azure Rights Management，但您另外有 Azure RMS 進階版的訂閱：**使用 Office 365 系統管理中心**。

-   如果您沒有 Office 365 訂閱︰**使用 Azure 傳統入口網站**。

### 從傳統 Office 365 系統管理中心啟動 Rights Management

> [!NOTE]
> 如果您是使用 **Office 365 系統管理中心預覽**而不是 Office 365 傳統系統管理中心，則可以使用[如何從 Office 365 系統管理中心預覽啟用 Azure Rights Management](../deploy-use/activate-office365-preview.md) 的指示，或切換至傳統版本以使用這些指示。 若要切換，請在登入後按一下 [首頁] 頁面上的 [Go to the old admin center (移至舊系統管理中心)]。

1.  移至 [Office 365 入口網站](https://portal.office.com/)，並使用您的 Office 365 全域管理員帳戶登入。

2.  如果 Office 365 系統管理中心未自動顯示，請選取左上角的應用程式啟動器圖示，並選擇 [管理員]。 只有 Office 365 管理員才會看到 [管理員] 磚。

  > [!TIP]
  > 如需系統管理中心說明，請參閱[關於 Office 365 系統管理中心 - 管理員說明](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3.  展開左窗格中的 [服務設定]。

4.  按一下 [Rights Management]。

5.  在 [Rights Management] 頁面上，按一下 [管理]。

6.  在 [Rights Management] 頁面上，按一下 [啟動]。

7.  出現 [您要啟動 Rights Management 嗎?] 提示時，按一下 [啟動]。

現在，您應該會看到 [Rights Management 已啟動] 及用來停用的選項 (您可能需要手動重新整理頁面)

此時請不要按 **[進階功能]**。 這會帶您到 Azure 傳統入口網站供您設定自訂範本，但本教學課程不需要用到範本。 您反而可以關閉 Office 365 系統管理中心。

### 若要從 Azure 傳統入口網站啟動 Rights Management

1.  移至 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=275081)，並使用您的 Azure Active Directory 全域管理員帳戶登入。

2.  在左窗格中，按一下 **[ACTIVE DIRECTORY]**。

3.  從 [Active Directory] 頁面中，按一下 [Rights Management]。

4.  選取要為 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理的目錄，按一下 [啟動]，然後確認您的動作。

[Rights Management 狀態] 現在應顯示 [使用中]，且會以 [停用] 選項取代 [啟用] 選項。

雖然您可以在入口網站設定 Rights Management 的其他選項，但本教學課程不需要用到這些選項，因此您可以關閉 Azure 傳統入口網站。

在第一個步驟中，您只需要做到這個程度就行。 Azure Rights Management 服務已啟動，以便稍後在教學課程中，您可以選取其中一個預設 Azure Rights Management 範本，來保護分類為機密的文件和電子郵件。

針對生產部署，您可能會想要額外設定自訂範本，或是用來取代兩個預設 Azure Rights Management 範本。 但本教學課程不需要用到自訂範本，因此您已經可以進入步驟 2。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於啟用 Rights Management|[啟用 Azure Rights Management](../deploy-use/activate-service.md)|
|關於預設範本以及如何建立全新自訂範本|[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 簡介](infoprotect-quick-start-tutorial.md)
[步驟 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Aug16_HO4-->


