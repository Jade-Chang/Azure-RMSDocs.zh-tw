---
title: "比較 Azure Rights Management 與 AD RMS | Azure RMS"
description: "如果您知道或先前已部署 Active Directory Rights Management Services (AD RMS)，您可能會想要知道 Azure RMS 在功能和需求方面與其比較起來如何。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 43429b44c019144744f39a1f92f144d315c2024c
ms.openlocfilehash: 2de89be11a45e3d1e53afc667a6cf65fcb69c690


---

# 比較 Azure Rights Management 與 AD RMS

>*適用於︰Active Directory Rights Management Services、Azure Rights Management、Office 365*

如果您知道或先前已部署 Active Directory Rights Management Services (AD RMS)，您可能會想要知道 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 在功能和需求方面與其比較起來如何。 

Azure RMS 的一些主要差異：

- **不需要伺服器基礎結構**：Azure RMS 不需要其他伺服器以及 AD RMS 所需的 PKI 憑證，因為 Microsoft Azure 會自動為您進行這項作業。 這可讓此雲端解決方案更快速地部署且更輕鬆地維護。

- **雲端驗證**：Azure RMS 使用 Azure AD 進行驗證 - 適用於內部使用者以及其他組織的使用者。 這表示可以驗證您的行動使用者，即使它們未連接到您的內部網路也是一樣，而且更容易與其他組織的使用者共用受保護內容。 許多組織正在執行 Azure 服務或有 Office 365，因此在 Azure AD 中已有使用者帳戶。 但是，如果沒有的話，個人版 RMS 可讓使用者建立免費帳戶。 若要與另一個組織共用 AD RMS 受保護內容，需要您設定與每個組織的明確信任。

- **行動裝置的內建支援**：不需要進行部署變更，Azure RMS 就能支援行動裝置和 Mac 電腦。 若要使用 AD RMS 來支援這些裝置，您必須安裝行動裝置擴充功能、設定 AD FS 同盟，以及建立公用 DNS 服務的額外記錄。

- **預設範本**︰Azure RMS 在啟用服務之後即會建立兩個預設範本，這樣很容易就可以立即開始保護重要資料。 AD RMS 沒有預設範本。

- **部門範本**：Azure RMS 支援將部門範本作為您建立之其他範本的組態設定。 此設定可讓您指定哪些使用者會在其用戶端應用程式 (例如 Office 應用程式) 中看到範本，讓他們可以更輕鬆地選取您為不同使用者群組所定義的正確原則。 AD RMS 不支援部門範本。

- **文件追蹤、撤銷和電子郵件通知**：Azure RMS 透過 RMS 共用應用程式支援這些功能，而 AD RMS 則否。


此外，Azure RMS 是雲端服務，因此提供新功能和修正程式的速度會比內部部署伺服器解決方案還要快。 Windows Server 2016 中未規劃 AD RMS 的新功能。

如需詳細資訊和其他差異，請使用下表並排比較 Azure RMS 與 AD RMS 的功能和優點。 如果您有安全性特定的比較問題，請參閱本文的[進簽署和加密的密碼編譯控制](compare-azure-rms-ad-rms.md#cryptographic-controls-for-signing-and-encryption)一節。

> [!NOTE]
> 為了更容易進行這項比較，這裡的部分資訊是重複取自 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)。 如需更特定的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 支援和版本資訊，請參考該來源。

|Azure RMS|Azure RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|支援 Microsoft Online Services (例如 Exchange Online 和 SharePoint Online 以及 Office 365) 中的資訊版權管理 (IRM) 功能。<br /><br />也支援內部部署 Microsoft 伺服器產品 (例如 Exchange Server、SharePoint Server 以及執行 Windows Server 和檔案分類基礎結構 (FCI) 的檔案伺服器)。|支援內部部署 Microsoft 伺服器產品 (例如 Exchange Server、SharePoint Server 以及執行 Windows Server 和檔案分類基礎結構 (FCI) 的檔案伺服器)。|
|啟用組織之間和任何組織內使用者之間的隱含信任。 這表示受保護的內容可以在同組織的使用者之間共用，或是當使用者具有 [!INCLUDE[o365_1](../includes/o365_1_md.md)]、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 或使用者註冊使用個人用 RMS 時，也可以跨組織共用。|必須使用信任的使用者網域 (TUD) 或您使用 Active Directory Federation Services (AD FS) 建立的同盟信任，在兩個組織之間的直接點對點關係中明確定義信任。|
|提供兩個將內容存取限制在您自己組織的預設權限原則範本；一個範本提供受保護內容的唯讀檢視，另一個範本提供受保護內容的寫入或修改權限。<br /><br />您也可以建立自己的自訂範本， 其中包括只有部份使用者可以看到的部門範本。 如需詳細資訊，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。<br /><br />此外，如果範本無法滿足使用目的，使用者也可以定義自己的一組權限。|沒有預設權限原則範本，您必須建立範本再散佈範本。 如需詳細資訊，請參閱＜ [AD RMS 原則範本考量](http://go.microsoft.com/fwlink/?LinkId=154765)＞。<br /><br />此外，如果範本無法滿足使用目的，使用者也可以定義自己的一組權限。|
|支援的 Microsoft Office 最低版本是 Office 2010，其需要 [RMS 共用應用程式](../rms-client/sharing-app-windows.md)。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：支援<br /><br />- Microsoft Office for Mac 2011：不支援|支援的 Microsoft Office 最低版本是 Office 2007。<br /><br />Microsoft Office for Mac：<br /><br />- Microsoft Office for Mac 2016：支援<br /><br />- Microsoft Office for Mac 2011：支援|
|支援適用於 Windows、Mac 電腦和行動裝置的 [RMS 共用應用程式](../rms-client/sharing-app-windows.md)。<br /><br />此外，RMS 共用應用程式支援以下功能：<br /><br />- 與另一個組織中的人員共用。<br /><br />- 電子郵件通知，可讓寄件者知道有人嘗試開啟受保護的附件。<br /><br />- 使用者的文件追蹤網站，包括能夠撤銷文件。|支援適用於 Windows、Mac 電腦和行動裝置的 [RMS 共用應用程式](../rms-client/sharing-app-windows.md)。 不過，共用並不支援與另一個組織中的人員共用、電子郵件通知，或文件追蹤網站和可讓使用者撤銷文件。|
|當您使用 RMS 共用應用程式時，所有檔案類型都可以受到 [原生或一般保護](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)。<br /><br />若為其他應用程式，請參閱 [Azure RMS 需求︰應用程式](../get-started/requirements-applications.md)中的資料表。|當您使用 RMS 共用應用程式時，所有檔案類型都可以受到 [原生或一般保護](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)。<br /><br />若為其他應用程式，請參閱 [Azure RMS 需求︰應用程式](../get-started/requirements-applications.md)中的資料表。|
|支援的 Windows 用戶端最低版本是 Windows 7。|支援的 Windows 用戶端最低版本是 Windows Vista Service Pack 2。|
|行動服務支援包括 Windows Phone、Android、iOS 及 Windows RT。<br /><br />在支援 Exchange ActiveSync IRM 的所有行動裝置平台上，也支援使用此通訊協定提供電子郵件支援。|行動裝置支援包括 Windows Phone、Android、iOS 和 Windows RT，而且需要 [Active Directory 權限管理服務行動裝置延伸模組](http://technet.microsoft.com/library/dn673574.aspx)。<br /><br />透過使用 Exchange ActiveSync IRM 所提供的電子郵件支援，在支援這個通訊協定的所有行動裝置平台上也支援。|
|支援電腦和行動裝置使用 Multi-Factor Authentication (MFA)。<br /><br />如需詳細資訊，請參閱 [Multi-Factor Authentication (MFA) 和 Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms)。|如果 IIS 設定為要求憑證，支援智慧卡驗證。|
|不須額外的組態設定即可支援密碼編譯模式 2，這個模式針對金鑰長度和加密演算法提供更強的安全性。<br /><br />如需詳細資訊，請參閱本文的[簽署和加密的密碼編譯控制](#cryptographic-controls-for-signing-and-encryption)一節，和 [AD RMS 密碼編譯模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|預設支援密碼編譯模式 1，並且需要額外的組態設定才能支援密碼編譯模式 2 以獲得更強的安全性。<br /><br />如需詳細資訊，請參閱本文的[簽署和加密的密碼編譯控制](#cryptographic-controls-for-signing-and-encryption)一節，和 [AD RMS 密碼編譯模式](http://go.microsoft.com/fwlink/?LinkId=266659)。|
|支援從 AD RMS 移轉和移轉至 AD RMS (如有需要)：<br /><br />- [從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [解除委任並停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)|支援從 Azure RMS 移轉和移轉 Azure RMS 的遷移：<br /><br />- [解除委任並停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)<br /><br />- [從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)|
|需要 RMS 授權來保護內容。 不需要 RMS 授權，即可取用受到 Azure RMS 保護的內容(包括來自另一個組織的使用者)。<br /><br />如需詳細資訊，請參閱[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。|需有 RMS 授權才能保護內容，並取用受到 AD RMS 保護的內容。<br /><br />如需 AD RMS 授權的詳細資訊，請參閱 [用戶端存取授權和管理授權](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) ，以取得一般資訊，但連絡您的 Microsoft 合作夥伴或微軟代表，以取得特定資訊。|

## 簽署和加密的密碼編譯控制
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 一律使用 RSA 2048 進行所有公用金鑰密碼編譯，以及使用 SHA 256 進行簽署操作。 相較之下，AD RMS 則支援 RSA 1024 和 RSA 2048，以及 SHA 1 或 SHA 256 進行簽署操作。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 和 AD RMS 都使用 AES 128 進行對稱式加密。

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 當您的租用戶金鑰是由 Microsoft 所建立並管理 (預設) 時，或是如果您自行管理租用戶金鑰 (稱為 BYOK)，會符合 FIPS 140-2 規範。 如需管理租用戶金鑰的詳細資訊，請參閱[規劃及實作 Azure Rights Management 租用戶金鑰](../plan-design/plan-implement-tenant-key.md)。

## 後續步驟
如果您想要從 AD RMS 移轉至 Azure RMS，請參閱[從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)





<!--HONumber=Aug16_HO4-->


