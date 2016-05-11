---
# required metadata

title: 取得生產前授權 | Azure RMS
description: 使用 RMS SDK 2.1 發行開發的應用程式需要生產授權合約。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013f9d75-0b66-44a8-9b01-d05b44a5ea0c

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 取得生產授權

在您可以釋出使用 Rights Management Services SDK 2.1 開發的應用程式之前，您必須套用生產授權合約以取得生產憑證。

> [!IMPORTANT]
> 如果您將利用以 Azure 為基礎的 RMS 執行用戶端應用程式，您必須要求 Azure RMS 租用戶。 透過租用戶要求傳送郵件給 <rmcstbeta@microsoft.com>。

如需利用 Azure RMS 執行的詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。


生產憑證和生產前憑證執行類似的功能，但目的是在不同的環境中使用。 兩者都包含憑證鏈結以及在信任的根包含 Microsoft 憑證授權單位 (CA) 憑證，但是只有在開發 RMS 應用程式時才使用生產前憑證。 生產憑證用於發行後的環境中。 生產憑證和相關聯的私密金鑰可用來建立和簽署資訊清單，識別可以或必須載入到應用程式處理序空間的檔案，以及不得載入的檔案。

如需金鑰的詳細資訊，請參閱[測試具備權限的應用程式](running-your-first-application.md)。

您可以藉由套用生產授權合約來取得憑證。

## 要求生產授權合約

![](../media/wedge.gif)

-   傳送電子郵件訊息至 [RMLA@microsoft.com](mailto:rmla@microsoft.com) 並包含下列資訊︰

    -   完整公司名稱

    -   實際公司地址 (包含縣市、州、國家或地區和郵遞區號)
    -   公司郵寄地址 (包含縣市、州、國家或地區和郵遞區號)
    -   公司電話及傳真號碼
    -   公司 URL
    -   公司的國家或地區
    -   應用程式或產品名稱
    -   要求者的名字和姓氏
    -   要求者的職稱或位置
    -   要求者的電子郵件地址

    雖然電子郵件帳戶不是絕對必要，但是應用程式處理序通常依賴電子郵件進行通訊。 您可以在 Microsoft Outlook.com 取得免費的電子郵件帳戶。 如果您沒有帳戶而且不想要，您可以傳送打字輸入的應用程式至下列位址︰

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    要求合約時，請執行下列動作：

    -   以英文提交資訊，如同合約中一般。
    -   傳送所有要求的資訊。 遺失或不完整的資訊可能會延遲要求的處理。

    Active Directory Rights Management 授權合約 (ADRMLA) 小組將在三個工作天內回應您透過電子郵件傳送的要求，如果您使用郵遞服務傳送要求，需要更長的時間。 回應將包含授權合約表格及進一步的指示。 讀取、簽署合約的所有頁面並傳回給 ADRMLA 小組。 請勿變更字型或變更授權合約中的段落格式。

    請務必遵循您從 ADRMLA 小組收到的指示。 指示會列出滿足憑證要求所需的數位資訊項目。 遵循逐步指示，您就會減少延遲。

    ADRMLA 小組會在建立生產憑證之後將其轉送給您。 此憑證根據您提供的授權合約和數位資訊 (包括公開金鑰) 建立。 請注意，ADRMLA 小組可能要花最多 15 個工作天才能回應透過電子郵件傳送的憑證，透過郵遞服務的通訊需要更長的時間。

## 相關主題

* [如何使用](how-to-use-msipc.md)
* [測試具備權限的應用程式](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO3-->


