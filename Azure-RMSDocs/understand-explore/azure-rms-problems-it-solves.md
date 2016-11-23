---
title: "Azure RMS 可以解決哪些問題 | Azure Information Protection"
description: "識別組織可能會有的資訊保護需求或問題，並了解 Azure RMS 技術如何解決這些需求或問題。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f1fff17f76361f8236974c6aeb21ed317c7d9883
ms.openlocfilehash: fda0a8bbbcc0a4b09cb7098d719bb10e431e1622


---


# <a name="what-problems-does-azure-rms-solve"></a>Azure RMS 可以解決哪些問題？

>*適用對象︰Azure 資訊保護、Office 365*

使用下表來識別組織在保護文件和電子郵件時可能會有的業務需求或問題，以及 Azure RMS 技術如何解決這些需求或問題。

Azure RMS 是 [Azure Information Protection](what-is-information-protection.md) 所使用的保護技術。

|需求或問題|透過 Azure RMS 解決|
|--------------------------|-----------------------|
|保護所有檔案類型|√ 在初期的 Rights Management 實作中，使用原生保護時只有 Office 檔案會受到保護。 現在，[一般保護](../rms-client/sharing-app-dialog-box.md#whats-the-difference-between-generic-protection-and-built-in-native-protection)表示支援所有檔案類型。|
|隨時隨地保護檔案|√ 當檔案儲存至位置時 ([就地保護](../rms-client/sharing-app-protect-in-place.md))，檔案便可持續受到保護，即使它複製到不受 IT 控制的儲存體中也是一樣，例如雲端儲存體服務。|
|透過電子郵件以安全的方式共用檔案|√ 透過電子郵件共用檔案時 ([共用保護](../rms-client/sharing-app-protect-by-email.md))，檔案是以電子郵件訊息的附件形式受到保護，具有如何開啟受保護的附件的指示。 電子郵件文字不會進行加密，所以收件者一定可以讀取這些指示。 不過，因為附加的文件會受到保護，即使將該電子郵件或文件轉寄給其他人，只有授權的使用者才能夠開啟附件。|
|稽核與監視|√ 您可以對於受保護的檔案[稽核與監視使用量](../deploy-use/log-analyze-usage.md)，即使這些檔案離開您的組織範圍也不例外。<br /><br />例如，您效力於 Contoso, Ltd。 您與 3 位來自 Fabrikam, Inc 的人員合作聯合專案。您透過電子郵件將您保護且限制為唯讀的文件傳送給這 3 位人員。 Azure RMS 稽核可提供下列資訊：<br /><br />- 您指定的 Fabrikam 人員是否已開啟文件，以及何時開啟。<br /><br />- 您未指定的其他人是否嘗試開啟文件 (且沒有成功)。這或許是因為文件轉寄或儲存到其他人可以存取的共用位置。<br /><br />- 任何指定的人員是否嘗試列印或變更文件 (且沒有成功)。|
|支援所有常見的裝置，不僅是 Windows 電腦|√ [支援的裝置](../get-started/requirements-client-devices.md)包括：<br /><br />- Windows 電腦和手機<br /><br />- Mac 電腦<br /><br />- iOS 平板電腦和手機<br /><br />- Android 平板電腦和手機|
|支援企業對企業的共同作業|√ 因為 Azure RMS 屬於雲端服務，所以在與其他組織共用受保護的內容之前，您無需明確設定與其他組織的信任。 如果他們已經有 Office 365 或 Azure AD 目錄，則會自動支援跨組織的共同作業。 如果沒有的話，使用者可以註冊免費的[個人版 RMS](rms-for-individuals.md) 訂用帳戶。|
|支援內部部署服務以及 Office 365|√  除了 [順暢地搭配 Office 365](office-apps-services-support.md) 之外，您也可以在部署 [RMS 連接器](../deploy-use/deploy-rms-connector.md) 時使用具有下列內部部署服務的 Azure RMS：<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- 執行檔案分類基礎結構的 Windows Server|
|輕鬆啟用|√ 只需要在 Azure 傳統入口網站中按幾下，就能為使用者[啟用 Rights Management 服務](../deploy-use/activate-service.md)。|
|視需要調整組織的能力|√ 因為 Azure RMS 會在 Azure 中以雲端服務的方式彈性執行以向上擴充和向外擴充，您無需佈建或部署其他內部部署伺服器。|
|建立簡單且彈性原則的能力|√ [自訂的權限原則範本](../deploy-use/configure-custom-templates.md) 提供了一個快速簡易的解決方案，可讓系統管理員套用原則，讓使用者為每份文件套用正確的保護層級，並限制組織內部人員的存取權。<br /><br />例如，若要將全公司策略白皮書與所有員工分享，您可以對所有內部員工套用唯讀原則。 但若是更為敏感的文件 (例如財務報告)，您可以限制只有高層主管才能存取。|
|廣泛的應用程式支援|√ Azure RMS 與 Microsoft Office 應用程式和服務緊密整合，並使用 RMS 共用應用程式來延伸對其他應用程式的支援。<br /><br />√ [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) 為您的內部開發人員和軟體廠商，提供了可撰寫自訂應用程式以支援 Azure RMS 的 API。<br /><br />如需詳細資訊，請參閱[其他支援 RMS API 的應用程式](api-support.md)。|
|IT 必須維護資料的控制權|√ 組織可以選擇管理他們自己的租用戶金鑰，並使用「[整合您自己的金鑰](../plan-design/plan-implement-tenant-key.md)」(BYOK) 解決方案，將其租用戶金鑰儲存在硬體安全性模組 (HSM)。<br /><br />√ 支援稽核和[使用量記錄](../deploy-use/log-analyze-usage.md)，如此您就可以分析商業見解、監督濫用情形，以及 (如果有發生資訊外洩) 執行蒐證分析。<br /><br />√ 即使文件之前是由已離開組織的員工進行保護，委派存取可以藉由使用[進階使用者功能](../deploy-use/configure-super-users.md)確保 IT 永遠可存取受保護的內容。 對照之下，對等加密解決方案會有遺失公司資料存取權的風險。<br /><br />√ 使用 [目錄同步處理工具](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison) (例如 Azure AD Connect)，僅同步處理 Azure RMS 為您的內部部署 Active Directory 帳戶支援通用識別身分 [所需的目錄屬性](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)。<br /><br />√ 使用 AD FS 啟用單一登入，但不將密碼複寫至雲端。<br /><br />√ 組織永遠可以選擇停止使用 Azure RMS 而不會遺失先前受 Azure RMS 保護的內容的存取權。 如需解除委任選項的相關資訊，請參閱[解除委任並停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。 此外，已部署 Active Directory Rights Management Services (AD RMS) 的組織可以[移轉至 Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md)，且不會失去先前受 AD RMS 保護之資料的存取權。|
> [!TIP]
> 如果您熟悉內部部署版本的 Rights Management、Active Directory Rights Management Services (AD RMS)，您可能會對[比較 Azure Rights Management 與 AD RMS](compare-azure-rms-ad-rms.md) 中的比較表格有興趣。

## <a name="security-compliance-and-regulatory-requirements"></a>安全性、規範和法規要求
Azure RMS 支援下列安全性、規範和法規要求：

√ 使用產業標準的密碼編譯，並支援 FIPS 140-2。 如需詳細資訊，請參閱 [Azure RMS 使用的密碼編譯控制項：演算法和金鑰長度](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths)資訊。

√ 支援 Thales 硬體安全性模組 (HSM)，以便將您的租用戶金鑰儲存在 Microsoft Azure 資料中心內。 Azure RMS 對其在北美、EMEA (歐洲、中東和非洲) 和亞洲的資料中心使用不同的安全園地，因此您的金鑰只能用在您的地區。

√ 獲得下列項目的認證：

-   ISO/IEC 27001:2013 (包括 [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   SOC 2 SSAE 16/ISAE 3402 認證

-   HIPAA BAA

-   EU 模型條款

-   FedRAMP 是 Office 365 憑證中 Azure Active Directory 的一部分，由 HHS 營運的 FedRAMP 機構發行

-   PCI DSS 層級 1

如需有關這些外部認證的詳細資訊，請參閱＜ [Azure 信任中心](http://azure.microsoft.com/support/trust-center/compliance/)＞。

## <a name="next-steps"></a>後續步驟

若要查看 Azure RMS 對於系統管理員和使用者的外觀，請參閱 [Azure RMS 運作方式](what-admins-users-see.md)。

如果您對 Azure RMS 運作方式的其他技術資訊有興趣，請參閱 [Azure RMS 如何運作？](how-does-it-work.md) 


<!--HONumber=Nov16_HO1-->


