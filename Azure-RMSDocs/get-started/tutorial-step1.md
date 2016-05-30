---
# required metadata

title: Azure RMS 快速入門教學課程 - 步驟 1 | Azure RMS
description: 教學課程的第一步，可為組織快速試用 Microsoft Azure Rights Management，只有 5 個步驟，花費時間不超過 15 分鐘。
keywords:
author: Cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# Azure RMS 快速入門步驟 1︰啟用 Rights Management 服務

*適用於︰Azure Rights Management、Office 365*


跳至︰ 
> [!div class="op_single_selector"]
- [簡介](quick-start-tutorial.md)
- [步驟 1︰啟用 Azure RMS](tutorial-step1.md)
- [步驟 2︰安裝 RMS 共用應用程式](tutorial-step2.md)
- [步驟 3︰傳送機密文件電子郵件](tutorial-step3.md)
- [步驟 4︰收件者讀取文件](tutorial-step4.md)
- [步驟 5︰追蹤您的文件](tutorial-step5.md)


![Azure RMS 快速入門教學課程步驟 1](../media/AzRMS_QuickStartSteps1.PNG)

雖然您擁有的訂閱可能會支援 Azure Rights Management，但這項服務預設是停用狀態。 若要啟動它，您可以使用 Office 365 系統管理中心或是 Azure 傳統入口網站：

-   如果您有包含 Azure Rights Management 的 Office 365 訂閱，或是所擁有的 Office 365 訂閱雖然沒有 Azure Rights Management，但您另外有 Azure RMS 進階版的訂閱：**使用 Office 365 系統管理中心**。.

-   如果您沒有 Office 365 訂閱︰**使用 Azure 傳統入口網站**。.

![教學課程步驟 1 螢幕擷取畫面](../media/AzRMS_Tutorial_1_Screenshots.png)

### 從傳統 Office 365 系統管理中心啟動 Rights Management

1.  移至 [Office 365 入口網站](https://portal.office.com/) ，以您的工作或學校帳戶登入。

2.  如果 Office 365 系統管理中心未自動顯示，請選取左上角的應用程式啟動器圖示，並選擇 [管理員]。 只有 Office 365 管理員才會看到 **[管理員]** 方塊。

    > [!TIP]
    > 如需系統管理中心說明，請參閱 [關於 Office 365 系統管理中心 - 管理員說明](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。.

3.  展開左窗格中的 **[服務設定]**.

4.  按一下 **[Rights Management]**.

5.  在 **[RIGHTS MANAGEMENT]** 頁面上，按一下 **[管理]**。.

6.  在 **[RIGHTS MANAGEMENT]** 頁面上，按一下 **[啟動]**。.

7.  出現 **[是否要啟動 Rights Management?]** 提示時，按一下 **[啟動]**。.

現在，您應該會看到 **[Rights Management 已啟動]** 及用來停用的選項 (您可能需要手動重新整理頁面)。

此時請不要按 **[進階功能]**。 這會帶您到 Azure 傳統入口網站供您設定範本，但本教學課程不需要用到範本。 您反而可以關閉 Office 365 系統管理中心。

### 若要從 Azure 傳統入口網站啟動 Rights Management

1.  移至 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=275081)並登入。

2.  在左窗格中，按一下 **[ACTIVE DIRECTORY]**。.

3.  從 **[Active Directory]** 頁面中，按一下 **[RIGHTS MANAGEMENT]**.

4.  選取要為 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理的目錄，按一下 [啟動]，然後確認您的動作。

**[RIGHTS MANAGEMENT 狀態]** 現在應該會顯示為 **[作用中]**，且 **[停用]** 會取代 **[啟動]** 選項。.

雖然您可以在入口網站設定 Rights Management 的其他選項，但本教學課程不需要用到這些選項，因此您可以關閉 Azure 傳統入口網站。

在第一個步驟中，您只需要做到這個程度就行。 將服務啟動，讓您組織中的所有使用者現在可以開始保護重要且敏感的文件。 在生產環境中，您可能會想要限制可以首先執行這項操作的使用者，以便分階段實作。 但在本教學課程中，則不需要這麼做。

雖然本文並未提及，但在生產部署期間，您可能也會想要設定自訂範本。 有了範本，使用者就能在需要保護檔案時，更輕鬆快速地套用正確設定。 您在啟動 Rights Management 時會自動獲得 2 個預設範本，並且您很可能會想讓生產環境中除了有這兩個預設範本外，再補上自己的自訂範本。 但本教學課程不需要用到範本，因此您已經可以進入下一個步驟。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於啟動 Rights Management 以及控制誰可以在服務啟動時保護檔案和電子郵件|[啟用 Azure Rights Management](../deploy-use/activate-service.md)|
|關於預設範本以及如何建立全新自訂範本|[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« 簡介](quick-start-tutorial.md)
[步驟 2 »](tutorial-step2.md)

<!--HONumber=Apr16_HO4-->


