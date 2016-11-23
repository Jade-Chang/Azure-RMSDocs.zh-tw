---
title: "HYOK 限制 |Azure 資訊保護"
description: Identify the limitations, prerequisites, and recommendations if you select AD RMS protection with Azure Information Protection. This solution is sometimes referred to as "hold your own key" (HYOK).
manager: mbaldwin
ms.date: 10/10/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: 821f4c0bfbad4c88bea0fbe26807f8e50677069b
ms.openlocfilehash: 44a7dc786b678844e58f2a60204853d86c8750a7


---

# AD RMS 保護的保存您自己的金鑰 (HYOK) 需求和限制

>*適用於：Azure 資訊保護*

**[ 這項功能仍為初步資訊而且可能隨時變更。 ]**

當您保護最機密的文件和電子郵件時，您通常會套用 Azure Rights Management 保護來獲取下列權益︰

- 不需要任何伺服器基礎結構，這可讓解決方案更快速，且部署和維護比內部部署解決方案更符合成本效益。

- 使用雲端式驗證，更輕易地與合作夥伴和其他組織的使用者共用。

- 與 Office 365 服務，例如搜尋、Web 檢視器、樞紐檢視、反惡意程式碼、eDiscovery 和 Delve 的緊密整合。

- 文件追蹤、撤銷並以電子郵件通知您已共用機密文件。

Azure RMS 使用由 Microsoft (預設)，或您所管理的組織使用的私用金鑰 (「自備金鑰」或 BYOK 案例)，保護貴組織的文件和電子郵件。 您使用 Azure RMS 保護的資訊永遠不會傳送至雲端；受保護的文件和電子郵件不會儲存在 Azure 中，除非您明確地將其儲存於該處，或使用另一個將其儲存在 Azure 中的雲端服務。 如需租用戶金鑰選項的詳細資訊，請參閱[規劃及實作 Azure 資訊保護租用戶金鑰](../plan-design/plan-implement-tenant-key.md)。 

不過，少數客戶可能需要以裝載於內部部署的金鑰保護特定的文件和電子郵件。 例如，這種需要可能來自法規和相容性因素。 

這項設定有時稱為「保存您自己的金鑰」(HYOK)，若您有使用中且具有下一節所述需求的 Active Directory Rights Management Services (AD RMS) 部署，則 Azure 資訊保護會支援 HYOK。 這項功能仍在預覽中。

在此 HYOK 案例中，權限原則以及保護這些原則之組織的私用金鑰由內部部署管理及保留，而用於標記和分類的 Azure 資訊保護原則仍然由 Azure 管理和儲存。 如同 Azure RMS 保護，您使用 AD RMS 保護的資訊永遠不會傳送至雲端。

> [!NOTE]
> 請只在必要的時候使用此設定，並且只針對需要的文件和電子郵件使用之。 AD RMS 保護並不提供您使用 Azure RMS 保護時所列的優點，且其目的為「不計代價的資料不透明度」。

當標籤使用 AD RMS 保護，而非 Azure RMS 保護時，使用者並不會察覺。 由於 AD RMS 保護的限制，請確定您提供清楚的指南，告知使用者何時應選取套用 AD RMS 保護的標籤。

## 使用 HYOK 時的限制

透過 Azure 資訊保護使用 AD RMS 保護，除了不支援使用 Azure RMS 保護時所享的列出權益，同時具有下列限制︰

- 不支援 Office 2010 及 Office 2007。

- 若您同時也使用 Azure RMS 保護︰設定 Azure RMS 保護的標籤時，不要使用 [不可轉寄] 選項。 您也必須指示使用者不要在 Outlook 中手動選取此選項。 

    如果經由標籤或使用者手動套用 [不可轉寄] 選項，選項可能由 AD RMS 部署套用，而不是預期的 Azure Rights Management 服務。 在此案例中，您外部共用的人員將無法開啟套用此 [不要轉寄] 選項的電子郵件訊息。

## HYOK 的需求

請確認您的 AD RMS 部署符合下列需求，以便為 Azure 資訊保護提供 AD RMS 保護。

- AD RMS 設定︰
    
    - Windows Server 2012 R2 的最低版本︰需用於生產環境但作為測試或評估用途，您可以使用的最低版本為 Windows Server 2008 R2 Service Pack 1。
    
    - 單一 AD RMS 根叢集。
    
    - [密碼編譯模式 2](https://technet.microsoft.com/library/hh867439.aspx)︰您可以使用 [RMS Analyzer 工具](https://www.microsoft.com/en-us/download/details.aspx?id=46437) 確認AD RMS 叢集的密碼編譯模式版本，以及其整體健康狀態。   
    
    - AD RMS 伺服器設定為搭配連線的用戶端所信任的有效 x.509 憑證使用 SSL/TLS︰需用於生產環境，但作為測試或評估用途則不需要。
    
    - 設定權限範本。

- 目錄同步作業於您的內部部署 Active Directory 和 Azure Active Directory 之間設定，並將使用 AD RMS 保護的使用者設定為單一登入。

- 如果您將與組織外部的其他人員共用 AD RMS 所保護的文件或電子郵件︰AD RMS 使用信任使用者網域 (TUD) 或使用 Active Directory 同盟服務 (AD FS) 所建立的同盟信任，以明確定義的信任，設定與其他組織直接的點對點關係。

- 使用者擁有的 Office 版本是在 Windows 7 Service Pack 1 或更新版本上執行的 Office 2013 Pro Plus Service 1 或 Office 2016 Pro Plus。 請注意，此案例不支援 Office 2010 和 Office 2007。

> [!IMPORTANT]
> 為了滿足這種案例所提供的高度保證，建議您 AD RMS 伺服器不要位於您的 DMZ 內，且只有完善管理的電腦可以加以使用 (例如，非行動裝置或工作群組電腦)。 
> 
> 同時建議您的 AD RMS 叢集應使用硬體安全性模組 (HSM)，如此在 AD RMS 部署遭到入侵或洩露時，您的伺服器授權人憑證 (SLC) 的私密金鑰便不會公開或遭竊。 

如需 AD RMS 的部署資訊及指示，請參閱 Windows Server 文件庫中的 [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) (Active Directory Rights Management 服務)。 


## 尋找以 Azure 資訊保護標籤指定 AD RMS 保護的詳細資訊

當您設定 AD RMS 保護的標籤時，您必須指定 AD RMS 叢集的授權 URL 及範本 GUID。 您可以在 Active Directory Rights Management Services 主控台找到這兩個值︰

- 找出範本 GUID︰展開叢集，然後按一下 [權限原則範本]。 接著您可以從 [散佈的權限原則範本] 資訊，從想要使用的範本複製 GUID。 例如︰82bf3474-6efe-4fa1-8827-d1bd93339119

- 若要找出授權 URL︰按一下叢集名稱。 從 [叢集詳細資料] 資訊中，複製 [授權] 值，並減去 **/_wmcs/licensing** 字串。 例如︰https://rmscluster.contoso.com 
    
    如果您有外部網路的授權值與內部網路授權值，而兩者不同︰只有當您將與您以明確點對點信任定義的合作夥伴共用受保護的文件或電子郵件時，才指定外部網路的值。 否則，請使用內部網路值，並確定所有使用 Azure 資訊保護之 AD RMS 保護的用戶端電腦連線都使用內部網路連線 (例如，遠端電腦使用 VPN 連線)。

## 後續步驟

如需閱讀有關這項預覽功能的詳細資訊，請參閱部落格文章公告 [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) (Azure 資訊保護與 HYOK (保存您自己的金鑰))。

如需設定 AD RMS 保護的標籤，請參閱 [How to configure a label to apply Rights Management protection](../deploy-use/configure-policy-protection.md) (如何設定標籤，以套用 Rights Management 保護)。 



<!--HONumber=Oct16_HO2-->


