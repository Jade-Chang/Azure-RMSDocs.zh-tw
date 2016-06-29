---
# required metadata

title: Azure Rights Management 術語 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management 術語

*適用於︰Azure Rights Management、Office 365*

因為單字、片語或與 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 有關的縮寫而感到困惑嗎？ 請在此尋找專屬於 Azure RMS 或在 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的內容中使用時有特定意義之詞彙和縮寫的定義。

|詞彙|定義|
|--------|--------------|
|AADRM|Azure Rights Management 的 Windows PowerShell 模組名稱，衍生自 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 先前命名為 (Windows) Azure Active Directory Rights Management 時的非官方縮寫。|
|啟動|啟用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服務，可讓組織將資訊保護加入文件和電子郵件中。 這個動作也會啟用 Exchange Online 和 SharePoint Online 中的版權管理。|
|Active Directory Rights Management Services|經常縮寫為 *Azure RMS*。<br /><br />一種 Windows Server 角色，其可使用加密和原則來保護文件、檔案及電子郵件，進而提供資訊保護。|
|Azure RMS|請參閱 *Active Directory Rights Management Services*。|
|Azure Rights Management|經常縮寫為 *Azure RMS*。<br /><br />透過使用加密和原則來保護文件、檔案及電子郵件的安全，進而提供資訊保護的一項 Azure 服務。  也稱為 *Azure Rights Management 服務*。 先前的名稱已包含：<br /><br />*Windows Azure Active Directory Rights Management*：通常縮寫為 Windows Azure AD Rights Management 服務。<br /><br />*RMS Online*：原始、建議的名稱，您有時可能會在錯誤訊息和記錄檔項目中看到。|
|Azure RMS|請參閱 *Azure Rights Management*。|
|BYOK|請參閱 *整合您自己的金鑰*。|
|整合您自己的金鑰|常用的縮寫為 *BYOK*。<br /><br />一種組態選項，想要產生並管理自己擁有之 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租用戶金鑰的組織會選擇此選項。|
|內容金鑰|受 RMS 啟發之應用程式對每個以 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 保護之文件或電子郵件建立的唯一金鑰，其有助於限制資訊洩露的風險。|
|取用|檔案受到 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 保護的情況下，將檔案解除封鎖以進行讀取或使用。|
|停用|停用 Rights Management Service，可讓組織不再使用 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]。|
|部門範本|您所建立 (自訂範本) 且設定為對選取的使用者 (而非組織中的所有使用者) 顯示的權限原則範本。|
|啟發的應用程式|以原生方式支援 Rights Management 的應用程式，包括 Word 和 Excel 等 Office 應用程式。 獨立軟體廠商 (ISV) 和開發人員也會撰寫以原生方式支援 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的應用程式。|
|企業版權管理|業界標準的通用詞彙，通常用來描述使用加密和原則授權工具的組合，協助組織保護敏感或珍貴資訊的產品和解決方案。 Microsoft Rights Management 即是企業版權管理 (ERM) 解決方案的範例之一。|
|ERM|請參閱 *企業版權管理*。|
|一般保護|一種保護層級，它能加密任何類型的檔案，避免未經授權的人員開啟檔案。 在開啟檔案後，檔案便已解密並可用於未以原生方式支援 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的應用程式。|
|資訊保護|有時縮寫為 *IP*。<br /><br />業界標準的通用詞彙，意指保護資料和檔案以避免未經授權的人員存取 (即使當資料和檔案已藉由電子郵件或文件共用離開組織邊界)。 Microsoft Rights Management 即是資訊保護 (IP) 解決方案的範例之一。|
|資訊版權管理|常用的縮寫為 *IRM*。<br /><br />用於 Office 服務 (如 Exchange Server、Word 及 SharePoint Online) 的詞彙，其描述 Rights Management 的支援能力。|
|IRM|請參閱 *資訊版權管理*。|
|MSDRM|有時被視為是 RMS 用戶端 1.0 的參照；新版本的 RMS 用戶端 (MSIPC) 已取代該版本的用戶端。 舊版用戶端支援以 RMS SDK 1.0 開發的應用程式，亦支援 Office 2010 和 Office 2007、Exchange 2010 和 Exchange 2013，以及 SharePoint 2010 和 SharePoint 2007。|
|MSIPC|有時被視為是 RMS 用戶端 2.0 的參照，其取代舊版本的 RMS 用戶端 (MSDRM)。 新版用戶端支援以 RMS SDK 2.0 開發的應用程式，亦支援 Office 2016、Office 2013、SharePoint 2013 及 RMS 共用應用程式。|
|原生保護|所有啟發應用程式皆具備的保護層級，期可避免未經授權的人員開啟檔案，也能強制執行更嚴格的原則 (如唯讀和禁止列印)。 此外，這項保護機制會與檔案共存，即便是使用者已將檔案轉寄給其他人員或將檔案儲存在其他人員可存取的公開位置，保護機制依然可以生效。|
|。pfile|一種副檔名，通常所有受 Rights Management 保護的檔案會有此副檔名。|
|。ppdf|Rights Management 自動建立檔案 (Word、Excel、PowerPoint 或 PDF) 的 PDF 複本 (供您以電子郵件分享) 時所建立的副檔名，以便在所有裝置上都能讀取 (但不是編輯) 該檔案。|
|權限層級|使用權限的邏輯群組，讓使用者和系統管理員可以更輕鬆地選擇以角色為基礎的組態選項。 例如，檢閱者和共同作者。|
|保護|使用加密、身分識別和存取控制原則協助保護您的資料，以將 Rights Management 控制項套用至檔案或電子郵件訊息。|
|publish|保護檔案以避免未經授權的存取和使用。|
|Rights Management 連接器|一種傳出 Proxy 轉送機制，您可為 Exchange Server 和 SharePoint 等內部部署服務部署，以使用 Azure Rights Management 保護資料。|
|Rights Management Services|適用於雲端版本之 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) 和內部部署版本之 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS) 兩者的通用詞彙。|
|Rights Management 共用應用程式|適用於 Windows 和大部分熱門行動裝置的選用可下載應用程式，它支援以就地和電子郵件等方式安全地共用檔案。|
|RMS|請參閱 *Rights Management Services*。|
|RMS 連接器|請參閱 *Rights Management 連接器*。|
|個人版 RMS|當組織未訂閱 Office 365 或 Azure Active Directory 時，供使用者使用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的免費訂閱。|
|RMS 共用應用程式|請參閱 *Rights Management 共用應用程式*。|
|進階使用者|受到高度信任的系統管理員群組，其能解密及存取組織以 Rights Management 保護的檔案。 一般說來，法務 eDiscovery 和稽核團隊需要這個階層的存取權限。|
|租用戶金鑰|亦稱為伺服器授權人憑證 (SLC) 金鑰。<br /><br />此租用戶金鑰是組織中的唯一金鑰，其根本目的在於保護所有與此金鑰鏈結的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 編譯功能。|
|取消保護|從檔案或電子郵件訊息，將使用加密、身分識別和存取控制原則協助保護您的資料的 Rights Management 控制項移除。|
|使用授權|個別文件的憑證，授與開啟由 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 保護之檔案或電子郵件的使用者。 此憑證包含該使用者對於檔案或電子郵件訊息的權限，還有用來加密內容的加密金鑰，以及文件原則中定義的額外存取限制。|





<!--HONumber=May16_HO2-->


