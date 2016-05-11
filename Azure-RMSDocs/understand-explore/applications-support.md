---
# required metadata

title: 應用程式如何支援 Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 應用程式如何支援 Azure Rights Management
使用下列資訊可協助您了解最常使用的使用者應用程式 (例如 Office 應用程式、Word、Excel、PowerPoint 及 Outlook) 和服務 (例如 Exchange 和 SharePoint) 如何使用 Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 來協助保護貴組織的資料。 
> [!NOTE]
> 若要確認 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) 支援的應用程式和版本，請參閱 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)。

在某些情況下，會根據您設定的原則自動套用資訊保護。 例如，SharePoint 文件庫、分類的檔案及 Exchange 傳輸規則就是這樣的情況。 在其他情況下，使用者則必須藉由選取範本或選取特定的選項，從他們的應用程式自行套用資訊保護。 例如，當使用者以電子郵件分享檔案，或對選取的使用者或組織外的使用者限制存取或使用以就地保護檔案時，就是這種情況。

範本可讓使用者 (和設定原則的系統管理員) 更容易套用正確的保護層級，以及對貴組織內部的人員限制存取。 雖然 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 隨附兩個預設範本，但是您可能會想要建立自訂範本以縮減必須指定個別選項的時間。 如需詳細資訊，請參閱[設定 Azure Rights Management 的自訂範本](../deploy-use/configure-custom-templates.md)。

針對使用者必須自行套用資訊保護的情況，請務必提供他們如何及何時套用資訊保護的指示和指導。 指示應該要針對他們所使用的應用程式和版本及使用方式，而何時及如何套用資訊保護的指導應該要適用於您的業務。 如需詳細資訊，請參閱[協助使用者使用 Azure Rights Management 來保護檔案](../deploy-use/help-users.md)。

如需如何設定 Azure RMS 應用程式的詳細資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

> [!TIP]
> 如需使用 Azure RMS 之應用程式的範例和螢幕擷取畫面，請參閱 [Azure RMS 運作方式：系統管理員和使用者看到的內容](what-admins-users-see.md)。


## 後續步驟

深入了解下列每個項目如何支援 Azure RMS:

-   [適用於 Windows 和行動平台的 RMS 共用應用程式](sharing-app-support.md)

-   [Office 應用程式和服務](office-apps-services-support.md)

-   [執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器](file-server-support.md)

-   [其他支援 RMS API 的應用程式](api-support.md)



<!--HONumber=Apr16_HO4-->


