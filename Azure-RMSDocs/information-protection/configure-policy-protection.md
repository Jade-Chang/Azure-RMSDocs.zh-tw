---
title: "如何設定標籤以套用 Rights Management 保護 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 00b4cd2b1e7b1196cedd39d7052db534e781bb13
ms.openlocfilehash: 7a20b59c404959c4ec209e8c29ac61ab71233e87


---

# 如何設定標籤以套用 Rights Management 保護

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

您可以透過使用 Azure Rights Management 來保護您最敏感的文件與電子郵件，它會使用加密、身分識別與授權原則來協助防止資料遺失。 此保護會在您設定標籤以使用 Rights Management 範本時套用。 

此範本可以是您啟用 Azure Rights Management 或自訂範本時，會自動建立的其中一個預設範本。 支援部門範本，但是只有在文件或電子郵件作者位於範本設定範圍內時，才會套用保護。 如果使用者不在範圍內，他們會看到一則顯示 Azure Information Protection 無法套用標籤的訊息。

## 保護的運作方式

當文件或電子郵件受 Azure Rights Management 保護時，它會在靜止狀態和傳輸過程中加密，且只能由授權的使用者進行解密。 即使文件或電子郵件已重新命名，仍然會保持此加密。 此外，您可以設定使用權限與限制，如下列範例︰

- 只有您組織內的使用者可以開啟文件或電子郵件。

- 只有行銷部門的使用者可以編輯和列印文件或電子郵件，組織中的所有其他使用者將只能檢視文件或電子郵件。

- 使用者無法轉寄電子郵件。

- 傳送給商務合作夥伴的文件或電子郵件，在指定日期後將無法開啟。

如需有關範本的詳細資訊，以及設定這些使用權限和限制的方式，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

如需 Azure Rights Management 及其運作方式的詳細資訊，請參閱[什麼是 Azure Rights Management？](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> 若要設定標籤以套用 Rights Management 保護，Azure Rights Management 服務必須已針對您的組織啟用。 如果您尚未這樣做，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。


## 設定標籤以套用 Rights Management 保護

1. 登入 [Azure 入口網站](https://portal.azure.com)。
 
2. 在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 [Information]。 選取 [Azure Information Protection]。

3. 在 [Azure Information Protection] 刀鋒視窗上，選取您要設定以套用 Rights Management 保護的標籤。

4. 在 [標籤] 刀鋒視窗上的 [設定 RMS 範本以保護包含此標籤的文件與電子郵件] 區段中，設定下列各項︰

    - 如果您看到 [選取 RMS 範本來源]：選取 [Azure RMS]。 
    
        請勿在沒有 Microsoft 協助的情況下，選取 [AD RMS] 與相關聯的設定選項。 如果您對搭配 Active Directory Rights Management Services 測試 Azure Information Protection 有興趣，請傳送電子郵件至 askipteam@microsoft.com。 
    
    - 針對 [選取 RMS 範本]：按一下下拉式方塊，然後選取您想要用來保護包含此標籤之文件和電子郵件的範本。

        > [!NOTE] 如果您在開啟 [標籤] 刀鋒視窗之後建立了新的範本，請關閉此刀鋒視窗並返回步驟 3，來使系統從 Azure 擷取新建立的範本以供您選取。

5. 按一下 **[儲存]**。

6. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  



<!--HONumber=Jul16_HO5-->


