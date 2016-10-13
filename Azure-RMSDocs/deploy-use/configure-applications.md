---
title: "設定 Azure Rights Management Service 的應用程式 | Azure Information Protection"
description: "適用於系統管理員將應用程式和服務設定為支援 Azure Information Protection 之 Azure Rights Management 保護服務的指示。 例如，Word 2013 和 Word 2010 等 Office 應用程式和 Exchange Online 等服務 (傳輸規則、資料外洩防護、不可轉寄，以及訊息加密)，以及 SharePoint Online (受保護的文件庫)。"
author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9dee9e7c925258ffd3cd9e783582733e9518d3fa
ms.openlocfilehash: d141bf56515853f7b6fddda1ddf150b8d3730b78


---

# 設定 Azure Rights Management 的應用程式

>*適用於︰Azure Information Protection、Office 365*

> [!NOTE]
> 本資訊適用於已部署 Azure Information Protection 的 IT 系統管理員和顧問。 如果您要尋找如何對特定的應用程式使用 Rights Management 功能，或如何開啟權限受保護之檔案的使用者說明及資訊，請使用應用程式隨附的說明及指引。
>
> 例如，在 Office 應用程式中，按一下 [說明] 圖示，然後輸入搜尋詞彙，例如 **Rights Management** 或 **IRM**。 針對適用於 Windows 的 RMS 共用應用程式，請參閱[Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)。

在為您的組織部署了 Azure Information Protection 之後，請使用下列資訊來設定應用程式和服務以支援 Azure Information Protection 的 Azure Rights Management Service。 這些包括 Word 2013 和 Word 2010 等 Office 應用程式和 Exchange Online 等服務 (傳輸規則、預防外洩防護、不可轉寄，以及訊息加密)，以及 SharePoint Online (受保護的程式庫)。 如需這些應用程式和服務如何支援 Rights Management 的資訊，請參閱[應用程式如何支援 Azure Rights Management Service](../understand-explore/applications-support.md)。

> [!IMPORTANT]
> 如需支援的版本和其他需求的詳細資訊，請參閱 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)。

-   [Office 365：用戶端和線上服務的設定](configure-office365.md)

    -   [Exchange Online：IRM 設定](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online 和商務用 OneDrive：IRM 設定](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Office 應用程式︰用戶端的設定](configure-office-apps.md)

    -   [Office 2016 和 Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Rights Management 共用應用程式：用戶端的安裝和設定](configure-sharing-app.md)

    -   [適用於 Windows 的 RMS 共用應用程式：安裝和設定](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [行動平台的 RMS 共用應用程式：安裝和管理](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


若要設定內部部署伺服器 (例如 Exchange Server 和 SharePoint Server)，請參閱[部署 Azure Rights Management 連接器](deploy-rms-connector.md)。

> [!TIP]
> 如需設定為使用 Azure Rights Management Service 之應用程式的高階範例和螢幕擷取畫面，請參閱 [Azure RMS 運作方式：系統管理員和使用者看到的內容](../understand-explore/what-admins-users-see.md)。


除了這些應用程式和服務，還有一些其他支援 Rights Management API 的應用程式。 此類別包含使用 Rights Management SDK 在內部撰寫的企業營運系統應用程式，及使用 Rights Management SDK 所撰寫的軟體廠商應用程式。 針對這些應用程式，請遵循應用程式提供的指示。

## 後續步驟
設定應用程式支援 Azure Rights Management Service 後，請使用 [Azure Information Protection 部署藍圖](../plan-design/deployment-roadmap.md)來檢查將 Azure Information Protection 轉出給使用者和系統管理員之前，是否還需要執行其他組態步驟。 如果沒有，您可能會發現下列操作資訊很有用︰

- [確認 Azure Rights Management Service](verify.md)

- [協助使用者使用 Azure Rights Management Service 來保護檔案](help-users.md)

- [記錄和分析 Azure Rights Management Service](log-analyze-usage.md)

- [Azure Information Protection 租用戶金鑰的作業](operations-tenant-key.md)





<!--HONumber=Sep16_HO5-->


