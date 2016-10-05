---
title: "Azure Information Protection 的需求 | Azure Information Protection"
description: "識別為貴組織部署 Azure Information Protection 的必要條件。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a809edc63801912e836878e9205643d7d52188f1
ms.openlocfilehash: 1239b1abe0ab720ef52ecce6c2bc948eb60fba18


---

# Azure Information Protection 需求

>*適用於︰Azure Information Protection、Office 365*


為貴組織部署 Azure Information Protection 之前，請確定已具備下列必要條件。 

|需求|詳細資訊|
|---------------|--------------------|
|Azure Information Protection 訂用帳戶|檢閱 Azure Information Protection [定價頁面](https://go.microsoft.com/fwlink/?LinkId=827589)的訂用帳戶資訊，確認貴組織的訂用帳戶有您想使用的 Azure Information Protection 功能。|
|Azure AD 目錄|您的組織必須具備 Azure AD 目錄才能支援 Azure Information Protection 的使用者驗證。 此外，若要從內部部署目錄 (AD DS) 使用您的使用者帳戶，您也必須設定目錄整合。<br /><br />當您有必要的用戶端軟體且正確設定 MFA 支援基礎結構時，Multi-Factor Authentication (MFA) 就支援 Azure Information Protection。<br /><br />如需詳細資訊，請參閱 [Azure Information Protection 的 Azure Active Directory 需求](requirements-azure-ad.md)。|
|用戶端裝置|使用者必須擁有執行支援 Azure Information Protection 作業系統的用戶端裝置 (電腦或行動裝置)。<br /><br />下列裝置支援 Azure Information Protection 用戶端，讓使用者分類和標記 Office 文件和電子郵件︰<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />當此用戶端使用 Azure Rights Management Service 保護資料時，即可供支援 Azure Rights Management Service 的相同裝置 (Windows、Mac、iOS、Android) 使用。 <br /><br />如需支援 Azure Rights Management Service 裝置的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的用戶端裝置](../get-started/requirements-client-devices.md)。|
|應用程式|Azure Information Protection 用戶端支援標記及保護以下列 Office 應用程式建立的檔案和電子郵件︰**Word**、**Excel**、**PowerPoint** 和 **Outlook**，來自下列 Office 套件︰<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />如需支援 Azure Rights Management Service 的應用程式資訊，請參閱[支援 Azure Rights Management 資料保護的應用程式](requirements-applications.md)。|
|支援連線至網際網路和相依雲端服務的基礎結構|如果你具有必須設定為允許特定連接的防火牆或類似的中介網路裝置，請參閱下列 Office 文章：[Office 365 URL 與 IP 位址範圍](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)，[Office 365 入口網站與共用](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)一節的 **Azure Rights Management (RMS)** 的資訊。<br /><br />使用本 Office 文章的指示，藉由訂閱 RSS 摘要追蹤此資訊的最新變更。<br /><br />除了 Office 文章中的資訊，還有 Azure Information Protection 特有資訊：<br /><br />- 允許從 TCP 443 至 **api.informationprotection.azure.com** 的 HTTPS 流量。<br /><br />- 請勿終止 TLS 用戶端對服務連線 (例如，為了執行封包層級檢查)。 這麼做會中斷 RMS 用戶端為了保護自己與 Azure RMS 的通訊，而對 Microsoft 所管理的 CA 進行的憑證偵測。<br /><br />- 如果您使用需要驗證的 Web Proxy，您必須將它設定為使用整合式 Windows 驗證 (具有使用者的 Active Directory 登入認證)。|

若要在內部部署伺服器使用 Azure Information Protection 的 Azure Rights Management Service，要支援下列產品：

-   Exchange Server

-   SharePoint Server

-   支援檔案分類基礎結構的 Windows Server 檔案伺服器

如需此案例其他需求的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的內部部署伺服器](requirements-servers.md)。

> [!IMPORTANT]
> 除非您使用的是 AD RMS 保護和 Azure Information Protection (「保存您自己的金鑰」(HYOK) 組態)，否則不支援下列部署案例：
> 
> -   在相同組織中同時執行 AD RMS 和 Azure RMS (移轉期間除外)，如[從 AD RMS 移轉至 Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md) 所述。
> 
> 支援[從 AD RMS 移轉至 Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) 以及從 [Azure Information Protection移轉至 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) 的路徑。 如果您部署 Azure Information Protection，然後決定您再不想要使用此雲端服務，請參閱[解除委任並停用 Azure Information Protection](../deploy-use/decommission-deactivate.md)。






<!--HONumber=Sep16_HO5-->


