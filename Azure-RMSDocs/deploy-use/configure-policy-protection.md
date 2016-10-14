---
title: "如何設定標籤以套用 Rights Management 保護 | Azure 資訊保護"
description: "您可以透過使用 Rights Management 服務來保護您最敏感的文件與電子郵件，它會使用加密、身分識別與授權原則來協助防止資料遺失。 此保護會在您設定標籤以使用 Rights Management 範本時套用。"
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: f17cf257607b0f74ca8bdaef13130da2f62dd587
ms.openlocfilehash: 830e982fc1f0443545942c1deb1a2fc93431be17


---

# 如何設定標籤以套用 Rights Management 保護

>*適用於：Azure 資訊保護*

您可以透過使用 Rights Management 服務來保護您最敏感的文件與電子郵件，它會使用加密、身分識別與授權原則來協助防止資料遺失。 此保護會在您設定標籤以使用 Rights Management 範本時套用。 

此範本可以是您啟用 Azure Rights Management 或自訂範本時，會自動建立的其中一個預設範本。 Azure Rights Management 的部門範本受到支援，但只在文件或電子郵件作者位於範本設定的範圍內時才套用保護。 如果使用者不在範圍內，他們會看到一則顯示 Azure 資訊保護無法套用標籤的訊息。

## 保護的運作方式

當文件或電子郵件受 Azure Rights Management 保護時，它會在靜止狀態和傳輸過程中加密，且只能由授權的使用者進行解密。 即使文件或電子郵件已重新命名，仍然會保持此加密。 此外，您可以設定使用權限與限制，如下列範例︰

- 只有您的組織內的使用者可以開啟公司機密文件或電子郵件。

- 只有行銷部門的使用者可以編輯和列印促銷公告文件或電子郵件，組織中的所有其他使用者將只能讀取文件或電子郵件。

- 使用者無法轉寄其中包含內部重組消息的電子郵件。

- 傳送給商務合作夥伴的目前價格清單於指定日期之後將無法開啟。

如需 Azure Rights Management 範本的詳細資訊，以及設定這些使用權限和限制的方式，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

如需 Azure Rights Management 及其運作方式的詳細資訊，請參閱[什麼是 Azure Rights Management？](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Azure Rights Management 服務必須已針對您的組織啟用，才能設定標籤以套用 Azure Rights Management 保護。 如果您尚未這樣做，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。


## 設定標籤以套用 Rights Management 保護

1. 如果您尚未這樣做，請開啟新的瀏覽器視窗並以全域管理員身分登入 [Azure 入口網站](https://portal.azure.com)，然後巡覽至 [Azure 資訊保護] 刀鋒視窗。 

    例如，在中樞功能表按一下 [更多服務] 開始在 [篩選] 方塊中輸入**資訊**。 選取 [Azure 資訊保護]。

2. 在 [Azure 資訊保護] 刀鋒視窗上，選取您要設定以套用 Rights Management 保護的標籤。

3. 在 [標籤] 刀鋒視窗中，請在 [Set RMS template for protecting documents and emails containing this label] (設定 RMS 範本，以保護包含此標籤的文件及電子郵件) 區段中的 [Select RMS template from] (自下列項目選取 RMS 範本) 之下，請選取 [Azure RMS] 或 [AD RMS (PREVIEW)] (AD RMS (預覽))。
    
    在大部分情況下，您將選取 [Azure RMS]。 請勿選取 AD RMS，除非您已閱讀並瞭解隨附於此設定的必要條件和限制，有時也稱為 「*保存您自己的金鑰*(HYOK)。 如需詳細資訊，請參閱 [Hold your own key (HYOK) requirements and restrictions for AD RMS protection](configure-adrms-restrictions.md) (AD RMS 保護的保存您自己的金鑰 (HYOK) 需求和限制)。
    
4. 如果您選取 Azure RMS：針對 [選取 RMS 範本]，按一下下拉式方塊，然後選取您想要用來保護具有此標籤的文件與電子郵件的[範本](../deploy-use/configure-custom-templates.md)或版權管理選項。
    
    選項的詳細資訊：
    
    - 您在開啟 [標籤] 刀鋒視窗後曾建立新範本嗎？ 請關閉此刀鋒視窗並返回步驟 2，讓系統從 Azure 擷取新建立的範本以供您選取。
    
    - 如果您選取**部門範本**，或者已設定[登入控制項](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)：
    
        - 範本設定範圍外的使用者，或是排除在套用 Azure Rights Management 保護外的使用者仍會看到標籤，但無法加以套用。 這類使用者會在選取標籤時看見下列訊息︰**Azure 資訊保護無法套用此標籤。若此問題持續發生，請連絡系統管理員。**
        
    - 如果您選取 [移除保護]：
        
        - 使用者必須有權限移除 Rights Management 保護，才能套用具有此選項的標籤。 這個選項要求使用者具備**匯出** (適用於 Office 文件) 或**完整控制**的[使用權限](../deploy-use/configure-usage-rights.md)，或身為 Rights Management 擁有者 (自動授與完整控制使用權限) 或 [Azure Rights Management 的進階使用者](../deploy-use/configure-super-users.md)。 預設版權管理範本不包括可讓使用者移除保護的使用權限。 

            如果使用者沒有權限移除 Rights Management 保護及使用 [移除保護] 選項選取這個標籤，就會看到下列訊息：**Azure 資訊保護無法套用此標籤。若此問題持續發生，請連絡系統管理員。**

5. 如果您選取 AD RMS︰提供範本 GUID 和您的 AD RMS 叢集的授權 URL。 [詳細資訊](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. 按一下 **[儲存]**。

7. 若要讓變更可供使用者使用，請按一下 [Azure 資訊保護] 刀鋒視窗上的 [發佈]。

## 後續步驟

如需關於設定 Azure 資訊保護原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  



<!--HONumber=Oct16_HO1-->


