---
title: "Azure RMS 需求：Azure AD 目錄 | Azure RMS"
description: "識別使用 Azure Rights Management (Azure RMS) 的 Azure AD 需求，以便能順利驗證使用者。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 81426cf43f31625c6e83d443fa925f6426eb89da
ms.openlocfilehash: b4ac71492ba9ad883d481149a248b919973d7386


---

# Azure RMS 需求：Azure AD 目錄

>*適用於︰Azure Rights Management、Office 365*


您必須有 Azure AD 目錄才能使用 Azure Rights Management (Azure RMS)。 您可為此目錄使用您的組織帳戶來登入 Azure 傳統入口網站，例如，您可設定和管理 Rights Management 範本。

如果您的組織尚無 Azure 訂用帳戶，您可以註冊免費試用以取得訂用帳戶：移至 [Azure 快速入門](https://account.windowsazure.com/organization) 頁面，並依照指示進行。

如需詳細資訊，請參閱 Azure Active Directory 文件的下列資源：

-   [什麼是 Azure AD 目錄？](/active-directory/active-directory-whatis)

-   [Azure 訂閱與 Azure Active Directory 的關聯方式](/active-directory/active-directory-how-subscriptions-associated-directory)

若要整合 Azure AD 目錄與內部部署 AD 樹系，請參閱[整合內部部署身分識別與 Azure Active Directory](/active-directory/active-directory-aadconnect)。

> [!NOTE]
> 如果您擁有的行動裝置或 Mac 電腦使用 AD FS 或同等的驗證提供者來驗證內部部署：
> 
> -   您必須使用在最低伺服器版本的 **Windows Server 2012 R2** 上運作的 AD FS，或使用支援 OAuth 2.0 通訊協定的替代驗證提供者。

## Multi-Factor Authentication (MFA) 和 Azure RMS
若要使用 Multi-Factor Authentication (MFA) 與 Azure RMS，至少需要下列其中一項：

-   Office 2013 (最低版本)：

    -   如果您有 Office 2013，您也必須安裝 [Office 2013 更新 2015 年 6 月 9 日 (KB3054853)](https://support.microsoft.com/kb/3054853)。 如需有關此更新以及現代化驗證如何將 Active Directory Authentication Library (ADAL) 引進 Office 2013 的詳細資訊，請參閱 Office 部落格上的[宣布 Office 2013 現代化驗證公用預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。

-   適用於 Windows 的 Rights Management 共用應用程式：

    -   您必須已安裝最低版本 1.0.1908.0，可使用 [控制台]、[程式和功能] 來確認。 如需有關適用於 Windows 之 Rights Management 共用應用程式的詳細資訊，請參閱[適用於 Windows 的 Rights Management 共用應用程式](../rms-client/sharing-app-windows.md)。

-   還有適用於行動裝置和 Mac 電腦的 Rights Management 共用應用程式：

    -   確定您已安裝最新版本。 RMS 共用應用程式 2015 年 9 月份版本引進 MFA 支援。

然後，設定 MFA 解決方案：

-   Microsoft 管理的租用戶 (您有 Azure Active Directory 或 Office 365)：

    -   設定 Azure MFA 對使用者強制執行 MFA。 如需相關指示，請參閱多因素驗證文件中的[開始在雲端中使用 Azure Multi-Factor Authentication](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。

        如需 Azure MFA 的詳細資訊，請參閱[什麼是 Azure Multi-Factor Authentication？](/multi-factor-authentication/multi-factor-authentication)

-   同盟租用戶 (您操作內部部署的同盟伺服器)：

    -   為 Azure Active Directory 或 Office 365 設定同盟伺服器。 例如，如果您使用 AD FS，請參閱 TechNet 上的[設定 AD FS 的其他驗證方法](https://technet.microsoft.com/library/dn758113.aspx)。

        如需此案例的詳細資訊，請參閱 Office 部落格上的[使用 Office 365 – 身分識別計畫現在已簡化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)。

## 後續步驟
若要檢查其他需求，請參閱 [Azure Rights Management 的需求](requirements-azure-rms.md)。




<!--HONumber=Aug16_HO4-->


