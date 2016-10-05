---
title: "準備 Azure Rights Management 保護 | Azure Information Protection"
description: "檢查使用 Azure Rights Management Service 的所有項目皆已就緒，讓貴組織可以保護文件和電子郵件。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 46db6ef6f65a06c42909252cf99884cc5eaaefe4
ms.openlocfilehash: 5a3df821c70b8cd308f8fb8cc94ee0cff069a3d9


---

# 準備 Azure Information Protection

>*適用於︰Azure Information Protection、Office 365*

為貴組織部署 Azure Information Protection 之前，請確定下列事項皆已就緒︰

-   您手動建立，或者從 Active Directory 網域服務 (AD DS) 自動建立和同步的雲端中使用者帳戶和群組。

    當您將內部部署帳戶和群組進行同步時，並不是所有的屬性皆需要同步。 如需 Azure Information Protection 所使用之 Azure Rights Management Service 的必要同步屬性清單，請參閱 Azure Active Directory 文件中的 [Azure RMS](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) 一節。 為了便於部署，我們推薦您使用 [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) 來連接您的內部部署目錄與 Azure Active Directory，但你也可以使用可達到相同結果的任何目錄同步方法。

-   您將在雲端中擁有郵件功能的群組中使用 Azure Information Protection。 這些可以是內建群組或手動建立的群組，後者包含將使用受保護文件及電子郵件的使用者。

    如果您有 Exchange Online，您可以使用 Exchange 系統管理中心，建立和使用擁有郵件功能的群組。 如果您有 AD DS 且正在同步處理至 Azure AD，您可以建立和使用屬於安全性群組或通訊群組之擁有郵件功能的群組。

## 啟用 Rights Management Service 來保護資料
當您準備好開始保護文件和電子郵件時，請啟動 Rights Management Service 以啟用這項技術。 如需詳細資訊，請參閱[啟用 Azure Rights Management](../deploy-use/activate-service.md)。






<!--HONumber=Sep16_HO4-->


