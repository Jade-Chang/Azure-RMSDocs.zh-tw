---
title: "如何從 Azure 傳統入口網站啟用 Azure Rights Management | Azure Information Protection"
description: "當您可以存取 Azure 入口網站時，適用於 Azure Rights Management Service 的啟用指示。 例如，當您有 Enterprise Mobility Suite 訂用帳戶或 Azure Information Protection Premium 訂用帳戶的情況下。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 805644a7c6dacc00519ad9ac07f39367d0784745
ms.openlocfilehash: a553ea57bd4b396b7629dc24aea9f76b4a2a5e5a


---

# 如何從 Azure 傳統入口網站啟動 Azure Rights Management

>*適用於：Azure Information Protection*


如果您有 Azure 入口網站的存取權，請使用下列指示。 例如，當您有 Enterprise Mobility Suite 訂用帳戶或 Azure Information Protection Premium 訂用帳戶的情況下。

> [!TIP]
> 觀賞 2 分鐘的影片︰[如何啟用 Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  在您註冊 Azure 帳戶之後，[登入 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=275081)。 使用全域管理員帳戶 (例如您用來訂閱包含 Azure Rights Management 等項目的帳戶)。

2.  在左窗格中，按一下 [Active Directory]。

3.  從 [Active Directory] 頁面中，按一下 [Rights Management]。

4.  選取要為 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 管理的目錄，按一下 [啟動]，然後確認您的動作。

    > [!NOTE]
    >如果您看到啟用錯誤，有可能是因為您的服務方案或產品版本不包含 Azure Information Protection 的 Azure Rights Management Service。
    >
    >使用[訂用帳戶資訊](https://go.microsoft.com/fwlink/?LinkId=827589)，確認您的訂用帳戶包含 Azure Rights Management。 如需這個問題的說明，請將電子郵件訊息傳送至 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)。


[Rights Management 狀態] 現在應顯示 [使用中]，且會以 [停用] 選項取代 [啟用] 選項。

## Azure 傳統入口網站中的 Rights Management 狀態值和說明
除了 **[使用中]** 狀態 (指出已啟用 Rights Management 服務並準備好可供使用) 之外，您可能也會看到 **[非使用中]**、 **[無法使用]**或 **[未授權]**。

|狀態值|描述|
|----------------|---------------|
|**[作用中]**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已啟用並準備好可供使用。|
|**[非使用中]**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 已停用，而且必須在組織可以保護檔案之前啟動。|
|**[無法使用]**|已關閉 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務。 請稍後再試一次。|
|**[未授權]**|您沒有檢視 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務狀態的權限。 例如，已鎖定您的帳戶，或您不是所選取租用戶的全域管理員。|

## 後續步驟
回到[啟用 Azure Rights Management](activate-service.md)。


<!--HONumber=Sep16_HO4-->


