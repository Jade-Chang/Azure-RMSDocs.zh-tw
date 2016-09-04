---
title: "Azure Rights Management 的需求 | Azure RMS"
description: "若要在組織中部署 Microsoft Azure Rights Management (Azure RMS)，請確定您具備下列必要條件。 然後，您可以使用 Azure Rights Management 部署藍圖為您的組織部署 Rights Management。"
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c7b194493073bcd76fa7a7d06bb31a7811e8cc3e
ms.openlocfilehash: d56eb077ef76e1869c7d90141f1b35c1bdbfe9fa


---

# Azure Rights Management 的需求

>*適用於︰Azure Rights Management、Office 365*


若要在組織中部署 Microsoft Azure Rights Management (Azure RMS)，請確定您具備下列必要條件。 然後，您可以使用 [Azure Rights Management 部署藍圖](../plan-design/deployment-roadmap.md)為您的組織部署 Rights Management。

|需求|詳細資訊|
|---------------|--------------------|
|RMS 的雲端訂閱|您的組織必須具有支援 RMS 的雲端訂閱。<br /><br />如需授權資訊，請參閱[支援 Azure RMS 的雲端訂閱](requirements-subscriptions.md)。|
|Azure AD 目錄|您的組織必須具備 Azure AD 目錄才能支援 RMS 的使用者驗證。 此外，若要從內部部署目錄 (AD DS) 使用您的使用者帳戶，您也必須設定目錄整合。<br /><br />當您有必要的用戶端軟體且正確設定 MFA 支援基礎結構時，Azure RMS 就支援 Multi-Factor Authentication (MFA)。<br /><br />如需詳細資訊，請參閱 [Azure AD 目錄](requirements-azure-ad.md)。|
|用戶端裝置|使用者必須擁有執行支援 RMS 作業系統的用戶端裝置 (電腦或行動裝置)。<br /><br />如需詳細資訊，請參閱[支援 Azure RMS 的用戶端裝置](requirements-client-devices.md)。|
|應用程式|使用者必須執行支援 RMS 的應用程式。<br /><br />如需詳細資訊，請參閱[支援 Azure RMS 的應用程式](requirements-applications.md)。|
|支援連線至網際網路和相依雲端服務的基礎結構|如果你具有必須設定為允許特定連接的防火牆或類似的中介網路裝置，請參閱下列 Office 文章：[Office 365 URL 與 IP 位址範圍](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)，[Office 365 入口網站與共用](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)一節的 **Azure Rights Management (RMS)** 的資訊。<br /><br />使用本 Office 文章的指示，藉由訂閱 RSS 摘要追蹤此資訊的最新變更。<br /><br />除了 Office 文章中的資訊，還有 Azure RMS 特有資訊：<br /><br />- 請勿終止 TLS 用戶端對服務連線 (例如，為了執行封包層級檢查)。 這麼做會中斷 RMS 用戶端為了保護自己與 Azure RMS 的通訊，而對 Microsoft 所管理的 CA 進行的憑證偵測。<br /><br />- 如果您使用需要驗證的 Web Proxy，您必須將它設定為使用整合式 Windows 驗證 (具有使用者的 Active Directory 登入認證)。|

若要搭配使用 Azure RMS 與內部部署伺服器，則會支援下列產品：

-   Exchange Server

-   SharePoint Server

-   支援檔案分類基礎結構的 Windows Server 檔案伺服器

如需此案例的其他 Azure RMS 需求的詳細資訊，請參閱[支援 Azure RMS 的內部部署伺服器](requirements-servers.md)。

> [!IMPORTANT]
> 不支援下列部署案例：
> 
> -   在相同組織中同時執行 AD RMS 和 Azure RMS (移轉期間除外)，如[從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md) 所述。
> 
> 支援[從 AD RMS 到 Azure RMS](http://technet.microsoft.com/library/Dn858447.aspx)，以及從 [Azure RMS 到 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) 的移轉路徑。 如果您部署 Azure RMS，然後決定您不再想要使用此雲端服務，請參閱[解除委任並停用 Azure Rights Management](../deploy-use/decommission-deactivate.md)。






<!--HONumber=Aug16_HO4-->


