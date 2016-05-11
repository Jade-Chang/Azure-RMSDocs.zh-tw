---
# required metadata

title: 如何從 Azure 傳統入口網站啟動 Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何從 Azure 傳統入口網站啟動 Azure Rights Management

如果您有 Azure 入口網站的存取權，請使用下列指示。 例如，您有 Enterprise Mobility Suite 的訂用帳戶。

> [!TIP]
> 觀賞 2 分鐘的影片︰[如何啟用 Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  在您註冊 Azure 帳戶之後，[登入 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=275081)。

2.  在左窗格中，按一下 [ACTIVE DIRECTORY]。

3.  從 [active directory] 頁面中，按一下 [RIGHTS MANAGEMENT]。

4.  選取要為 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理的目錄，按一下 [啟動]，然後確認您的動作。

    > [!NOTE]
    > 如果出現啟動錯誤，則可能是因為您的服務方案或產品版本無法支援 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]。
    >
    > 使用[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)中的資訊來確認 RMS 支援。 如需這個問題的說明，請將電子郵件訊息傳送至 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)。

[RIGHTS MANAGEMENT 狀態] 現在應該會顯示為 [作用中] ，且 [啟動] 選項會取代為 [停用]。

## Azure 傳統入口網站中的 Rights Management 狀態值和說明
除了 [使用中] 狀態 (指出已啟用 Rights Management 服務並準備好可供使用) 之外，您可能也會看到 [非使用中]、 [無法使用]或 [未授權]。

|狀態值|說明|
|----------------|---------------|
|**[作用中]**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已啟用並準備好可供使用。|
|**[非使用中]**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已停用，而且必須在組織可以保護檔案之前啟動。|
|**[無法使用]**|已關閉 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務。 請稍後再試一次。|
|**[未授權]**|您沒有檢視 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務狀態的權限。 例如，已鎖定您的帳戶，或您不是所選取租用戶的全域管理員。|

## 後續步驟
回到[啟用 Azure Rights Management](activate-service.md)。

<!--HONumber=Apr16_HO3-->


