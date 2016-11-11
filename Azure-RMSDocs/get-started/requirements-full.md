---
title: "Azure 資訊保護的需求 - 完整文章 | Azure 資訊保護"
description: "識別為貴組織部署 Azure 資訊保護的必要條件。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 10cf9371-a61b-495f-9d42-898448806994
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 68b3d74d32b98f44cfdf9cf78b7a9151f16124ce
ms.openlocfilehash: b4afd639439f0549ce38de1e63a1798d30680066


---


# <a name="requirements-for-azure-information-protection"></a>Azure 資訊保護需求

>*適用於︰Azure 資訊保護、Office 365*


為貴組織部署 Azure 資訊保護之前，請確定已具備下列必要條件。 

|需求|詳細資訊|
|---------------|--------------------|
|Azure 資訊保護訂用帳戶|檢閱 Azure 資訊保護網站上的[訂用帳戶資訊](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)和[功能清單](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)，確認組織的訂用帳戶有您想使用的 Azure 資訊保護功能。|
|Azure Active Directory|您的組織必須具備 Azure Active Directory (Azure AD) 才能支援 Azure 資訊保護的使用者驗證。 此外，若要從內部部署目錄 (AD DS) 使用您的使用者帳戶，您也必須設定目錄整合。<br /><br />如果是同盟帳戶 (例如，您使用 AD FS)，它們必須使用 Windows 整合式驗證。 Azure 資訊保護不支援表單型驗證。<br /><br />當您有必要的用戶端軟體且正確設定 MFA 支援基礎結構時，Multi-Factor Authentication (MFA) 就支援 Azure 資訊保護。<br /><br />如需詳細資訊，請參閱 [Azure 資訊保護的 Azure Active Directory 需求](requirements-azure-ad.md)。|
|用戶端裝置|使用者必須擁有執行支援 Azure 資訊保護作業系統的用戶端裝置 (電腦或行動裝置)。<br /><br />下列裝置支援 Azure 資訊保護用戶端，讓使用者分類和標記 Office 文件和電子郵件︰<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />當此用戶端使用 Azure Rights Management Service 保護資料時，即可供支援 Azure Rights Management Service 的相同裝置 (Windows、Mac、iOS、Android) 使用。 <br /><br />如需支援 Azure Rights Management Service 裝置的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的用戶端裝置](../get-started/requirements-client-devices.md)。|
|應用程式|Azure 資訊保護用戶端支援標記及保護以下列 Office 應用程式建立的檔案和電子郵件︰**Word**、**Excel**、**PowerPoint** 和 **Outlook**，來自下列 Office 套件︰<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />如需支援 Azure Rights Management Service 的應用程式資訊，請參閱[支援 Azure Rights Management 資料保護的應用程式](requirements-applications.md)。|
|支援連線至網際網路和相依雲端服務的基礎結構|如果你具有必須設定為允許特定連接的防火牆或類似的中介網路裝置，請參閱下列 Office 文章：[Office 365 URL 與 IP 位址範圍](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)，[Office 365 入口網站與共用](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)一節的 **Azure Rights Management (RMS)** 的資訊。<br /><br />使用本 Office 文章的指示，藉由訂閱 RSS 摘要追蹤此資訊的最新變更。<br /><br />除了 Office 文章中的資訊，還有 Azure 資訊保護特有資訊：<br /><br />- 允許從 TCP 443 至 **api.informationprotection.azure.com** 的 HTTPS 流量。<br /><br />- 請勿終止 TLS 用戶端對服務連線 (例如，為了執行封包層級檢查)。 這麼做會中斷 RMS 用戶端為了保護自己與 Azure RMS 的通訊，而對 Microsoft 所管理的 CA 進行的憑證偵測。<br /><br />- 如果您使用需要驗證的 Web Proxy，必須將其設定為透過使用者的 Active Directory 登入認證使用整合式 Windows 驗證。|

若要在內部部署伺服器使用 Azure 資訊保護的 Azure Rights Management Service，要支援下列產品：

-   Exchange Server

-   SharePoint Server

-   支援檔案分類基礎結構的 Windows Server 檔案伺服器

如需此案例其他需求的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的內部部署伺服器](requirements-servers.md)。

> [!IMPORTANT]
> 除非您使用的是 AD RMS 保護和 Azure 資訊保護 (「保存您自己的金鑰」(HYOK) 組態)，否則不支援下列部署案例：
> 
> -   在相同組織中同時執行 AD RMS 和 Azure RMS (移轉期間除外)，如[從 AD RMS 移轉至 Azure 資訊保護](../plan-design/migrate-from-ad-rms-to-azure-rms.md)所述。
> 
> 支援[從 AD RMS 移轉至 Azure 資訊保護](http://technet.microsoft.com/library/Dn858447.aspx) 以及從 [Azure 資訊保護移轉至 AD RMS](http://msdn.microsoft.com/library/azure/dn629429.aspx) 的路徑。 如果您部署 Azure 資訊保護，然後決定您再不想要使用此雲端服務，請參閱[解除委任並停用 Azure 資訊保護](../deploy-use/decommission-deactivate.md)。

## <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure Information Protection 的 Azure Active Directory 需求

您必須有 Azure AD 目錄才能使用 Azure Information Protection。 您可為此目錄使用您的組織帳戶來登入 Azure 傳統入口網站，例如，您可設定和管理 Rights Management 範本。

如果您的組織尚無 Azure 訂用帳戶，您可以註冊免費試用以取得訂用帳戶：移至 [Azure 快速入門](https://account.windowsazure.com/organization) 頁面，並依照指示進行。

如需詳細資訊，請參閱 Azure Active Directory 文件的下列資源：

-   [什麼是 Azure AD Directory？](/active-directory/active-directory-whatis)

-   [Azure 訂用帳戶與 Azure Active Directory 建立關聯的方式](/active-directory/active-directory-how-subscriptions-associated-directory)

若要整合 Azure AD 目錄與內部部署 AD 樹系，請參閱[整合內部部署身分識別與 Azure Active Directory](/active-directory/active-directory-aadconnect)。

> [!NOTE]
> 如果您擁有的行動裝置或 Mac 電腦使用 AD FS 或同等的驗證提供者來驗證內部部署：
> 
> -   您必須使用在最低伺服器版本的 **Windows Server 2012 R2** 上運作的 AD FS，或使用支援 OAuth 2.0 通訊協定的替代驗證提供者。

### <a name="multifactor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) 和 Azure Information Protection
若要使用 Multi-Factor Authentication (MFA) 與 Azure Information Protection，至少需要下列其中一項：

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

        如需此案例的詳細資訊，請參閱 Office 部落格上的 [The Works with Office 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) (使用 Office 365 - 身分識別計畫現已經過簡化)。

## <a name="client-devices-that-support-azure-rights-management-data-protection"></a>支援 Azure Rights Management 資料保護的用戶端裝置

請使用下列各節找出支援 Azure Rights Management Service 的裝置，提供 Azure Information Protection 資料保護。

### <a name="computers"></a>電腦
下列電腦作業系統支援 Azure Rights Management Service：

-   **Windows 7** (x86、x64)

-   **Windows 8** (x86、x64)

-   **Windows 8.1** (x86、x64)

-   **Windows 10** (x86、x64)

-   **Mac OS X**：Mac OS X 10.8 的最低版本 (Mountain Lion)

### <a name="mobile-devices"></a>行動裝置
下列行動裝置作業系統支援 Azure Rights Management Service：

-   **Windows Phone**：Windows Phone 8.1

-   **Android 手機和平板電腦**：Android 4.0.3 的最低版本

-   **iPhone 和 iPad**：iOS 7.0 的最低版本

-   **Windows 平板電腦**：Windows 10 Mobile 和 Windows 8.1 RT

## <a name="applications-that-support-azure-rights-management-data-protection"></a>支援 Azure Rights Management 資料保護的應用程式

請使用下表找出以原生方式支援提供 Azure 資訊保護資料保護之 Azure Rights Management Service (Azure RMS) 的應用程式。 

這些應用程式使用 Rights Management API 緊密整合 Rights Management 支援，來支援使用限制。 這些應用程式也稱為 RMS 創新。

除非另外註明，否則支援的功能適用於 Azure RMS 與 AD RMS 兩者。 此外，在 iOS、Android、OS X 和 Windows Phone 8.1 上的 AD RMS 支援需要 [Active Directory 權限管理服務行動裝置延伸模組](https://technet.microsoft.com/library/dn673574.aspx)。

表格欄位的相關資訊：

-   **受保護的 PDF**：這些檔案具有 .ppdf 副檔名，而且會在您使用 RMS 共用應用程式來透過電子郵件共用 Office 檔案和 PDF 檔案時自動建立。 RMS 共用應用程式和 iOS 與 Android 的 Azure 資訊保護應用程式包含受保護 PDF 檔案的讀取器。 如果您之前使用 Azure RMS 或 AD RMS 建立保護的 PDF 檔案，您可以繼續在 Windows、iOS 和 Android 裝置上，使用 Foxit Reader 和 Nitro Pro 讀取這些檔案。

-   **電子郵件：**列出的電子郵件用戶端可以保護電子郵件訊息本身，這樣會自動保護任何附加檔案。 在此情況下，用戶端的預覽功能可讓授權收件者看見受保護的內容 (訊息和附件)。 不過，若電子郵件訊息本身未受保護，但附件受到保護，用戶端預覽功能則無法讓授權收件者看見受保護的附件。

-   **其他檔案類型**：文字和影像檔包含副檔名為 .txt、.xml、.jpg 和 .jpeg 的檔案。 這些檔案在受到 Rights Management 原生保護後會變更其副檔名並成為唯讀狀態。 無法受到原生保護的檔案在 Rights Management 對其進行一般保護後，會有 .pfile 副檔名。 如需詳細資訊，請參閱[Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。


|**裝置作業系統**|Word、Excel、PowerPoint|受保護的 PDF|電子郵件|其他檔案類型|
|-------------------------------|---------------------------|-----------------|---------|--------------------|
|**Windows**|Office 2010<br /><br />Office 2013<br /><br />Office 2016 <br /><br />Office Mobile 應用程式 (僅適用於 Azure RMS) [[1]](#footnote-1)<br /><br />Office Online [[2]](#footnote-2)|Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF 閱讀程式<br /><br />RMS 共用應用程式|Outlook 2010<br /><br />Outlook 2013<br /><br />Office 2016 <br /><br />Outlook Web App (OWA) [[3]](#footnote-3)<br /><br />Windows Mail [[4]](#footnote-4)|適用於 Windows 的 RMS 共用應用程式：文字、影像、pfile<br /><br />Siemens JT2Go：JT 檔案 (僅限 Windows 10)|
|**iOS**|Office for iPad and iPhone [[5]](#footnote-5)<br /><br />Office Online [[2]](#footnote-2)<br /><br />TITUS 文件|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br /> Foxit Reader<br /><br />TITUS 文件|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for iPad and iPhone [[4]](#footnote-4)<br /><br />OWA for iOS [[3]](#footnote-3)<br /><br />TITUS Mail|Azure 資訊保護應用程式 [[1]](#footnote-1)：文字、影像<br /><br />TITUS 文件︰Pfile|
|**Android**|GigaTrust App for Android<br /><br />Office Online [[2]](#footnote-2)<br /><br />Office Mobile (僅限 Azure RMS) [[1]](#footnote-1)|Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />GigaTrust App for Android<br /><br />Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|9Folders [[4]](#footnote-4)<br /><br />Azure 資訊保護應用程式 [[1]](#footnote-1)<br /><br />GigaTrust App for Android [[4]](#footnote-4)<br /><br />Citrix WorxMail [[6]](#footnote-6)<br /><br />NitroDesk [[4]](#footnote-4)<br /><br />Outlook for Android [[4]](#footnote-4)<br /><br />OWA for Android [[3]](#footnote-3) 和 [[7]](#footnote-7)<br /><br />Samsung Email (S3 和更新版本) [[7]](#footnote-7)<br /><br />TITUS Classification for Mobile|Azure 資訊保護應用程式 [[1]](#footnote-1)：文字、影像|
|**OS X**|Office 2011 (僅適用於 AD RMS)<br /><br />Office 2016 for Mac<br /><br />Office Online [[2]](#footnote-2)|Foxit Reader<br /><br />RMS 共用應用程式 [[1]](#footnote-1)|Outlook 2011 (僅適用於 AD RMS)<br /><br />Outlook 2016 for Mac<br /><br />Outlook for Mac|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Windows 10 行動裝置版**|Office Mobile 應用程式(僅適用於 Azure RMS) [[1]](#footnote-1)|不支援|Citrix WorxMail [[6]](#footnote-6)<br /><br />Outlook Mail|不支援|
|**Windows RT**|Office 2013 RT<br /><br />Office Online [[2]](#footnote-2)|不支援|Outlook 2013 RT<br /><br />Windows 郵件應用程式<br /><br />Windows Mail [[4]](#footnote-4)|Siemens JT2Go：JT 檔案|
|**Windows Phone 8.1**|Office Mobile (僅適用於 AD RMS)|RMS 共用應用程式 [[1]](#footnote-1)|Outlook Mobile [[4]](#footnote-4)|RMS 共用應用程式 [[1]](#footnote-1)︰文字、影像、pfile|
|**Blackberry 10**|不支援|不支援|Blackberry 電子郵件 [[4]](#footnote-4)|不支援|


##### <a name="footnote-1"></a>註腳 1
支援檢視受保護的內容。

##### <a name="footnote-2"></a>註腳 2 
當未受保護的文件上傳至 SharePoint Online 及商務用 OneDrive 中受保護的文件庫時，可以檢視受保護的文件。 

##### <a name="footnote-3"></a>註腳 3
如果收件者收到受保護電子郵件，但並未使用 Exchange 作為郵件伺服器，或寄件者屬於其他組織，收件者就只能在豐富型電子郵件用戶端 (如 Outlook) 中開啟此內容。 不能從 Outlook Web Access 開啟此內容。

##### <a name="footnote-4"></a>註腳 4
使用 Exchange ActiveSync IRM，必須由 Exchange 系統管理員啟用。 使用者可以檢視、回覆和全部回覆受保護的電子郵件訊息，但使用者本身無法保護新的電子郵件訊息。

如果收件者收到受保護電子郵件，但並未使用 Exchange 作為郵件伺服器，或寄件者屬於其他組織，收件者就只能在豐富型電子郵件用戶端 (如 Outlook) 中開啟此內容。 收件者無法從 Outlook Web Access 或使用 Exchange Active Sync IRM 的行動郵件用戶端開啟此內容。

##### <a name="footnote-5"></a>註腳 5
支援檢視和編輯受保護的文件。 如需詳細資訊，請參閱下列 Office 部落格文章︰[Azure Rights Management 支援已適用 Office for iPad and iPhone](https://blogs.office.com/2015/07/22/azure-rights-management-support-comes-to-office-for-ipad-and-iphone-2/)

##### <a name="footnote-6"></a>註腳 6
如需詳細資訊，請參閱 [WorxMail 的 Citrix 產品文件集](http://docs.citrix.com/en-us/worx-mobile-apps/10/xmob-worx-mail.html)。

##### <a name="footnote-7"></a>註腳 7
如需詳細資訊，請參閱下列 Office 部落格文章︰[OWA for Android 目前可在選取的裝置上使用](http://blogs.office.com/2014/06/11/owa-for-android-now-available-on-select-devices/)

## <a name="more-information-about-azure-rms-support-for-office"></a>Office 的 Azure RMS 支援的詳細資訊

Azure RMS 與 Word、Excel、PowerPoint 及 Outlook 應用程式緊密整合；這些應用程式通常稱此功能為資訊版權管理 (IRM)。 下列 Office 用戶端版本支援使用 Azure RMS 保護檔案和電子郵件︰

- Office Professional Plus 2016

- Office Professional Plus 2013

- Office Professional Plus 2010

所有版本的 Office (不包括 Office 2007) 都支援取用受保護的內容。

Azure RMS 與 Office Professional Plus 2010 或 Office Professional 2010：

- 需要適用於 Windows 的 Rights Management 共用應用程式

- 不支援 Windows 10

### <a name="more-information-about-the-azure-information-protection-app-for-ios-and-android"></a>iOS 與 Android 的 Azure 資訊保護應用程式詳細資訊

iOS 與 Android 的 Azure 資訊保護應用程式現在已取代這些裝置的 RMS 共用應用程式。 它除提供相同的功能，另支援受權限保護的電子郵件訊息以及 SharePoint Online 上受權限保護的 PDF 檔案。

如果您的 iOS 和 Android 裝置是由 Microsoft Intune 註冊，您可以使用原則管理的應用程式來部署及管理此應用程式。 如需詳細資訊，請參閱 Intune 文件的[在 Microsoft Intune 主控台中設定及部署行動應用程式管理原則](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 在此 Intune 文件的步驟 2 中，使用發行原則管理應用程式的指示。

如需詳細資訊，請參閱[適用於 iOS 和 Android 的 Microsoft Azure 資訊保護應用程式常見問答集](../rms-client/mobile-app-faq.md)。


### <a name="more-information-about-the-rights-management-sharing-application"></a>Rights Management 共用應用程式的詳細資訊

如需有關適用於 Windows 之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   [Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)

如需有關行動平台之 Rights Management 共用應用程式的詳細資訊，請參閱下列資源：

-   使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)上的連結，下載相關的應用程式

-   [FAQ for Microsoft Rights Management Sharing Application for Mobile Platforms](https://technet.microsoft.com/dn451248) (行動裝置平台的 Microsoft Rights Management 共用應用程式常見問題集)

> [!NOTE]
> 適用於 iOS 和 Android 的 RMS 共用應用程式現在已由 Azure 資訊保護應用程式取代。

### <a name="more-information-about-other-applications-that-support-azure-rms"></a>其他支援 Azure RMS 之應用程式的詳細資訊

除了資料表中的應用程式，任何支援 RMS API 的應用程式都可以和 Azure RMS 整合，包括︰

- 使用 RMS SDK 在內部撰寫的企業營運系統應用程式

- 使用 RMS SDK 撰寫之軟體廠商的應用程式。

如需有關 SDK 的詳細資訊，請參閱 [Microsoft Rights Management SDK](../develop/developers-guide.md)。

### <a name="applications-that-are-not-supported-by-azure-rms"></a>Azure RMS 不支援的應用程式

Azure RMS 目前不支援下列應用程式，包括：

-   Microsoft Office for Mac 2011

-   Microsoft OneDrive for Business for SharePoint Server 2013

-   XPS 檢視器
 
此外，RMS 共用應用程式具有下列限制：

-   對於 Windows 電腦：需要 Windows 7 Service Pack 1 的最低版本

## <a name="onpremises-servers-that-support-azure-rights-management-data-protection"></a>支援 Azure Rights Management 資料保護的內部部署伺服器

當您使用 Azure Rights Management 連接器時，下列內部部署伺服器產品支援 Azure Information Protection。 此連接器作用如同內部部署伺服器與 Azure Information Protection 用以保護 Office 文件和電子郵件的 Azure Rights Management Service 之間的通訊介面 (轉送)。 

若要使用此連接器，您必須設定 Active Directory 樹系與 Azure Active Directory 之間的目錄同步處理。

-   **Exchange Server**：

    -   Exchange Server 2016

    -   Exchange Server 2013

    -   Exchange Server 2010

-   **Office SharePoint Server**：

    -   Office SharePoint Server 2016

    -   Office SharePoint Server 2013

    -   Office SharePoint Server 2010

-   **執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器**：

    -   Windows Server 2012 R2

    -   Windows Server 2012

    > [!NOTE]
    > 因為執行 Windows Server 2008 R2 的檔案伺服器沒有內建的檔案管理工作動作可套用 Rights Management 保護，所以您在此情況下無法使用 Rights Management 連接器。 不過，若您設定自訂檔案管理工作來執行可執行檔或指令檔，而這些檔案可使用 Azure RMS 來保護檔案，則您可以在這些作業系統上使用檔案分類基礎結構和 Azure RMS。 例如，使用 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx) 的 Windows PowerShell 指令碼。
    > 
    > 您也可以對執行較新版本 Windows Server 的伺服器使用這些 Cmdlet，好處是這些 Cmdlet 可以保護所有檔案類型。 RMS 連接器只保護 Office 檔案。 如需做法指示，請參閱[具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護](../rms-client/configure-fci.md)。

Rights Management 連接器在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 上受到支援。

如需如何為這些內部部署伺服器設定 Rights Management 連接器的詳細資訊，請參閱[部署 Azure Rights Management 連接器](../deploy-use/deploy-rms-connector.md)。




<!--HONumber=Nov16_HO1-->


