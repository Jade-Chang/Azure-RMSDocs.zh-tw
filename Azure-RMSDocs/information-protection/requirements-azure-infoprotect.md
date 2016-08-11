---
title: "Azure Information Protection 需求 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/29/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fe19726959bc16384120b610183c392031519813
ms.openlocfilehash: ff322e4ff0914ca29c7fe937a41936cb15d9a913


---

# Azure Information Protection 需求

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

若要評估 Azure Information Protection 的預覽版本，請確定您具備下列必要條件。 

|需求|詳細資訊|
|---------------|--------------------|
|包含 Azure RMS 的雲端訂閱|您的組織必須具有支援 Rights Management 的雲端訂閱。<br /><br />如需詳細資訊和免費試用連結，請參閱[支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。|
|Azure AD 目錄|您的組織必須具備 Azure AD 目錄才能支援 Azure RMS 和 Azure Information Protection 的使用者驗證。 此外，若要從內部部署目錄 (AD DS) 使用您的使用者帳戶，您也必須設定目錄整合。<br /><br />當您有必要的用戶端軟體且正確設定 MFA 支援基礎結構時，Azure RMS 就支援 Multi-Factor Authentication (MFA)。<br /><br />如需詳細資訊，請參閱 [Azure AD 目錄](../get-started/requirements-azure-ad.md)，其中 Azure RMS 的資訊也適用於 Azure Information Protection。|
|用戶端裝置|此預覽版本支援下列用戶端裝置︰<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />當您保護資料時，它可由支援 Azure Rights Management 的相同裝置 (Windows、Mac、iOS、Android) 來取用。 如需這些裝置的詳細資訊以及支援的版本，請參閱 [Azure RMS 需求：支援 Azure RMS 的用戶端裝置](../get-started/requirements-client-devices.md)。|
|應用程式|在預覽版本和公開上市 (GA) 版本中，Azure Information Protection 支援標記及保護以下列 Office 應用程式建立的檔案和電子郵件︰**Word**、**Excel**、**PowerPoint** 和 **Outlook**，來自下列 Office 套件︰<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />在公開上市之後，請在 [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Enterprise Mobility and Security 部落格) 上尋找公告，以得知 Azure Information Protection 何時將支援其他檔案類型，例如 PDF、音訊、視訊和影像檔。|
|支援連線至網際網路和相依雲端服務的基礎結構|如果你具有必須設定為允許特定連接的防火牆或類似的中介網路裝置，請參閱下列 Office 文章：[Office 365 URL 與 IP 位址範圍](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)，[Office 365 入口網站與共用](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)一節的 **Azure Rights Management (RMS)** 的資訊<br /><br />此外：<br /><br />- 允許 TCP 443 上對 **rmsibizaapiprod.cloudapp.net** 的 HTTPS 流量。<br /><br />- 請勿終止 TLS 用戶端對服務連線 (例如，為了執行封包層級檢查)。 <br /><br />- 如果您使用需要驗證的 Web Proxy，您必須將它設定為使用整合式 Windows 驗證 (具有使用者的 Active Directory 登入認證)。|

## 後續步驟

如果您符合這些需求，請嘗試我們的自我引導式示範，以親自設定及體驗 Azure Information Protection︰[Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)。




<!--HONumber=Jul16_HO5-->


