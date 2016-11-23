---
title: "部署您的應用程式 | Azure RMS"
description: "本主題概要說明並引導您完成啟用權限的應用程式的部署選項"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: e47c5331f49c62a00617f40b1af7ffdc4a89dcfd


---

# 部署到生產環境


本主題概要說明並引導您完成啟用權限的應用程式的部署選項。

## 要求生產授權合約

 在您可以釋出使用 Rights Management Services SDK 2.1 開發的應用程式之前，您必須套用生產授權合約以取得生產憑證。

您可以藉由套用生產授權合約來取得憑證。

傳送電子郵件訊息至 [RMLA@microsoft.com](mailto:rmla@microsoft.com) 並包含下列資訊︰

- 完整公司名稱
- 實際公司地址 (包含縣市、州、國家或地區和郵遞區號)
- 公司郵寄地址 (包含縣市、州、國家或地區和郵遞區號)
- 公司電話及傳真號碼
- 公司 URL
- 公司的國家或地區
- 應用程式或產品名稱
- 要求者的名字和姓氏
- 要求者的職稱或位置
- 要求者的電子郵件地址

雖然電子郵件帳戶不是絕對必要，但是應用程式處理序通常依賴電子郵件進行通訊。 您可以在 Microsoft Outlook.com 取得免費的電子郵件帳戶。 如果您沒有帳戶而且不想要，您可以傳送打字輸入的應用程式至下列位址︰

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

要求合約時，請執行下列動作：
- 以英文提交資訊，如同合約中一般。
- 傳送所有要求的資訊。 遺失或不完整的資訊可能會延遲要求的處理。

Active Directory Rights Management 授權合約 (ADRMLA) 小組將在三個工作天內回應您透過電子郵件傳送的要求，如果您使用郵遞服務傳送要求，需要更長的時間。 回應將包含授權合約表格及進一步的指示。 讀取、簽署合約的所有頁面並傳回給 ADRMLA 小組。 請勿變更字型或變更授權合約中的段落格式。

請務必遵循您從 ADRMLA 小組收到的指示。 指示會列出滿足憑證要求所需的數位資訊項目。 遵循逐步指示，您就會減少延遲。

ADRMLA 小組會在建立生產憑證之後將其轉送給您。 請注意，ADRMLA 小組可能要花最多 15 個工作天才能回應透過電子郵件傳送的憑證，透過郵遞服務的通訊需要更長的時間。


## Rights Management Service Client 2.1 的安裝選項與需求

假設您使用 RMS SDK 2.1，您需要在使用者電腦上部署 Active Directory Rights Management Services Client 2.1。

### RMS Client 2.1

RMS Client 2.1 是專為您的用戶端電腦設計的軟體，可透過使用 RMS 的應用程式協助保護資訊流通的存取和使用，不論是安裝在內部部署或 Microsoft 資料中心皆然。

RMS Client 2.1 不是 Windows 作業系統元件。 RMS Client 2.1 以選用下載的形式發行，可透過確認並接受其授權合約，與協力廠商軟體一起自由發佈，以啟用透過在環境中使用與部署 RMS 伺服器保護權限的用戶端存取內容。


> [!IMPORTANT]
> AD RMS Client 2.1 是特定的架構，而且必須符合目標作業系統的架構。


## RMS Client 2.1 安裝選項

-   **轉散發 RMS Client 2.1**

    建議的方法是使用您慣用的安裝技術，組合 RMS 用戶端安裝程式套件與您的應用程式或解決方案。 RMS 用戶端可以免費轉散發，並與其他應用程式和 IT 解決方案組成套件。

    您可以選擇從 RMS Client 2.1 安裝程式以互動方式安裝 RMS Client 2.1，或以無訊息方式予以安裝。 整合步驟會是︰

    -   下載 RMS Client 2.1 安裝程式
    -   整合執行 RMS Client 2.1 安裝程式與您的應用程式安裝程式

    整合 RMS Client 2.1 與您的應用程式有兩個很好的例子，即 RMS SDK 2.1 安裝程式套件和權限受保護資料夾總管套件。 自行嘗試安裝它們以了解方法。

-   **讓 RMS Client 2.1 成為應用程式安裝的必要條件**

    在此案例中，您將會建立必要條件，如此當 RMS Client 2.1 未出現在使用者電腦時，您的應用程式安裝將會失敗。

    如果用戶端不存在則提供錯誤訊息，告知使用者下載 RMS Client 2.1 複本的位置

    如果出現用戶端，則繼續進行應用程式安裝。

## 使用您的應用程式啟用 Azure Rights Management Services

> [!NOTE]
> 如果您已移轉至新的 ADAL 模型進行驗證，您不需要安裝 SIA。 如需詳細資訊，請參閱 [ADAL authentication for your RMS enabled application](adal-auth.md) (已啟用 RMS 應用程式的 ADAL 驗證)。
> 此外，您可以**為 Windows 10 認證您的應用程式**，方法是更新應用程式以使用 ADAL 驗證，而非 Microsoft Online 登入小幫手，您與您的客戶將能夠：利用多重要素驗證、不需要求電腦的系統管理權限即可安裝 RMS Client 2.1


為了讓您的使用者利用 Azure Rights Management 服務，您必須部署 *Online Services 登入小幫手 (SIA)*。 身為應用程式開發人員，您不知道使用者要使用 RMS (內部部署) 或 Azure Rights Management 服務 (雲端服務)。


> [!IMPORTANT]
> 如果您將利用以 Azure 為基礎的 RMS 執行用戶端應用程式，必須建立自己的租用戶。 如需詳細資訊，請參閱 [Azure RMS requirements: Cloud subscriptions that support Azure RMS](../get-started/requirements-subscriptions.md) (Azure RMS 需求：支援 Azure RMS 的雲端訂閱)。
> 如需利用 Azure RMS 執行的詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

-   從 Microsoft 下載中心下載 [Microsoft Online Services 登入小幫手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)。
-   請確定您的權限啟用應用程式部署，包含此服務選項的必要條件檢查。
-   如需您自己的測試，和您的使用者的線上服務使用等詳細資訊，請參閱 TechNet 主題，[設定 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)。

如需有關啟用應用程式以使用 Azure Rights Management 服務的 RMS，請參閱[啟用您的應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

## 相關的主題

* [Microsoft Online Services 登入小幫手](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [設定 Rights Management](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [啟用您的應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
 

 



<!--HONumber=Oct16_HO1-->


