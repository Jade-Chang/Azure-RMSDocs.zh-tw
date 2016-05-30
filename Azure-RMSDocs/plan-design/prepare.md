---
# required metadata

title: 準備 Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 準備 Azure Rights Management

*適用於︰Azure Rights Management、Office 365*

在您申請雲端訂閱，並使用 [!INCLUDE[o365_1](../includes/o365_1_md.md)] 或 Azure Active Directory 的帳戶建立您的組織後，您即準備好啟用 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 服務。

不過，在您這麼做之前，請確定已備妥下列條件：

-   您手動建立，或者從 Active Directory 網域服務 (AD DS) 自動建立和同步的雲端中使用者帳戶和群組。

    當您將內部部署帳戶和群組進行同步時，並不是所有的屬性皆需要同步。 關於 Azure RMS 必須同步的屬性清單，請參閱 Azure Active Directory 文件中的 [Azure RMS 一節](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)。 為了便於部署，我們推薦您使用 [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) 來連接您的內部部署目錄與 Azure Active Directory，但你也可以使用可達到相同結果的任何目錄同步方法。

-   您將在雲端中擁有郵件功能的群組中使用 Rights Management。 這些可以是內建群組或手動建立的群組，後者包含將使用 Rights Management 的使用者。

    如果您有 Exchange Online，您可以使用 Exchange 系統管理中心，建立和使用擁有郵件功能的群組。 如果您有 AD DS 且正在同步處理至 Azure AD，您可以建立和使用屬於安全性群組或通訊群組之擁有郵件功能的群組。

## 啟用 Rights Management
依預設，當您申請 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 或 Azure AD 帳戶時會停用 [!INCLUDE[o365_2](../includes/o365_2_md.md)] 。 若要啟用組織的 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]，則您必須啟動服務。 如需詳細資訊，請參閱 [啟用 Azure Rights Management](../deploy-use/activate-service.md)。.





<!--HONumber=Apr16_HO4-->


