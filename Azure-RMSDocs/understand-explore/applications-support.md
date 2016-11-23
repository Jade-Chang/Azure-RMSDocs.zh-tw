---
title: "應用程式如何支援 Azure Rights Management Service | Azure Information Protection"
description: "了解最常使用的使用者應用程式 (例如 Office 應用程式、Word、Excel、PowerPoint 及 Outlook) 和服務 (例如 Exchange 和 SharePoint) 如何使用 Azure Information Protection 的 Microsoft Azure Rights Management Service 來協助保護貴組織的文件和電子郵件。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9dee9e7c925258ffd3cd9e783582733e9518d3fa
ms.openlocfilehash: 3d2f95f2a20782897be293162d901ae0ffac421a


---

# 應用程式如何支援 Azure Rights Management Service

>*適用於︰Azure Information Protection、Office 365*

使用下列資訊協助您了解最常使用的使用者應用程式 (例如 Office 應用程式、Word、Excel、PowerPoint 及 Outlook) 和服務 (例如 Exchange 和 SharePoint) 如何使用 Azure Information Protection 的 Microsoft Azure Rights Management Service 來協助保護貴組織的文件和電子郵件。 
> [!NOTE]
> 若要確認 Azure Rights Management Service 支援的應用程式和版本，請參閱[支援 Azure Rights Management 資料保護的應用程式](../get-started/requirements-applications.md)。

在某些情況下，Azure Rights Management Service 會根據系統管理員設定的原則自動套用保護。 例如，SharePoint 文件庫、分類的檔案及 Exchange 傳輸規則就是這樣的情況。 在其他情況下，使用者則必須藉由選取範本或選取特定的選項，從他們的應用程式自行套用資訊保護。 例如，當使用者以電子郵件分享檔案，或對選取的使用者或組織外的使用者限制存取或使用以就地保護檔案時，就是這種情況。

範本可讓使用者 (和設定原則的系統管理員) 更容易套用正確的保護層級，以及對貴組織內部的人員限制存取。 雖然 Azure Rights Management Service 隨附兩個預設範本，但是您可能會想要建立自訂範本以縮減必須指定個別選項的時間。 如需詳細資訊，請參閱[設定 Azure Rights Management Service 的自訂範本](../deploy-use/configure-custom-templates.md)。

針對使用者必須自行套用資訊保護的情況，請務必提供他們如何及何時套用資訊保護的指示和指導。 指示應該要針對他們所使用的應用程式和版本及使用方式，而何時及如何套用資訊保護的指導應該要適用於您的業務。 如需詳細資訊，請參閱[協助使用者使用 Azure Rights Management Service 來保護檔案](../deploy-use/help-users.md)。

如需如何設定 Azure Information Protection 之 Azure Rights Management Service 應用程式的資訊，請參閱[設定 Azure Rights Management 的應用程式](../deploy-use/configure-applications.md)。

> [!TIP]
> 如需使用 Azure Rights Management Service 之應用程式的範例和螢幕擷取畫面，請參閱 [Azure RMS 運作方式：系統管理員和使用者看到的內容](what-admins-users-see.md)。

搜尋服務可以透過不同的方式與 Rights Management 整合。 例如： 

- Exchange Online 和 Exchange Server 使用服務端編製索引，因此使用者的受 RMS 保護電子郵件會自動顯示在其搜尋結果中。 

- SharePoint Online 和 SharePoint Server 只在下載時才會將 Rights Management 保護套用到檔案，這表示此文件保護解決方案不會影響 SharePoint 上的編製索引和搜尋結果。 不過，如果您有一份文件想要儲存在 SharePoint 中，而且不應該傳回到搜尋結果中，則會先透過 RMS 保護檔案，再將它上傳至 SharePoint。

- Windows 桌面搜尋在裝置的不同使用者之間使用共用的索引；因此，若要保持受保護文件中資料的安全，則不會對受 RMS 保護的檔案編製索引。 這表示，雖然您的搜尋結果不會包括您已保護的檔案，但是您可以確保包含機密資料的檔案不會顯示在可能登入或連接到您電腦之其他使用者的搜尋結果中。 



## 後續步驟

深入了解下列每個項目如何支援 Azure Rights Management Service：

-   [適用於 Windows 和行動平台的 RMS 共用應用程式](sharing-app-support.md)

-   [Office 應用程式和服務](office-apps-services-support.md)

-   [執行 Windows Server 並使用檔案分類基礎結構 (FCI) 的檔案伺服器](file-server-support.md)

-   [其他支援 RMS API 的應用程式](api-support.md)




<!--HONumber=Sep16_HO5-->


