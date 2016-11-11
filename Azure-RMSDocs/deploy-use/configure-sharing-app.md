---
title: "Rights Management 共用應用程式：用戶端的安裝和組態 | Azure Information Protection"
description: "適用於系統管理員，關於在 Windows 電腦及行動裝置上部署 Rights Management (RMS) 共用應用程式的資訊。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: f96641355da46eee85a828a6e5e417282883bac7


---

# <a name="rights-management-sharing-application-installation-and-configuration-for-clients"></a>Rights Management 共用應用程式：用戶端的安裝和設定

>*適用對象︰Azure Information Protection、Office 365*

用戶端電腦需要 Rights Management (RMS) 共用應用程式才能搭配使用 Azure Rights Management Service 與 Office 2010，並建議支援 Azure Information Protection 之 Azure Rights Management Service 的所有電腦和行動裝置使用。 RMS 共用應用程式藉由安裝 Office 增益集來整合 Office 應用程式，讓使用者得以從功能區直接且輕易地保護檔案和電子郵件。 它也會提供一般保護，來保護 Azure Rights Management Service 原本未支援的檔案類型，以及提供文件追蹤網站，供使用者追蹤和撤銷他們所保護的檔案。

## <a name="the-rms-sharing-application-for-windows-installation-and-configuration"></a>適用於 Windows 的 RMS 共用應用程式：安裝和設定
若要針對企業部署安裝及設定適用於 Windows 的 RMS 共用應用程式，請參閱 [Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。

> [!TIP]
> 如果您想要快速地為單一電腦安裝和測試 RMS 共用應用程式，請參閱 [Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)的[下載及安裝 Rights Management 共用應用程式](../rms-client/install-sharing-app.md)。

## <a name="the-rms-sharing-application-for-mobile-platforms-installation-and-management"></a>行動平台的 RMS 共用應用程式：安裝和管理
若要安裝行動平台的 RMS 共用應用程式，請可以使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)的連結下載相關應用程式。 無需設定即可搭配使用 Azure Rights Management Service 與此應用程式。

> [!NOTE]
> 適用於 iOS 和 Android 的 RMS 共用應用程式現在已由 Azure Information Protection 應用程式取代。

**如果您有 Microsoft Intune**︰由於 Azure Information Protection 應用程式包含 Microsoft Intune 應用程式軟體開發套件，因此當 iOS 和 Android 裝置是由 Intune 註冊時，您可以部署及管理這些裝置的 Azure Information Protection 應用程式。 如需詳細資訊，請參閱 Intune 文件的[在 Microsoft Intune 主控台中設定及部署行動應用程式管理原則](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 在步驟 2，使用指示以發行原則管理應用程式。






<!--HONumber=Nov16_HO2-->


