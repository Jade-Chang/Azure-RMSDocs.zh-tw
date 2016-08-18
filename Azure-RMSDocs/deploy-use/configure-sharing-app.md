---
title: "Rights Management 共用應用程式：用戶端的安裝和組態 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: d3f923cf6f140c2caa75b7b0c8ac90a42be962a7


---

# Rights Management 共用應用程式：用戶端的安裝和設定

*適用於︰Azure Rights Management、Office 365*

用戶端電腦需要 Rights Management (RMS) 共用應用程式才能搭配使用 Azure RMS 與 Office 2010，並建議支援 Azure RMS 的所有電腦和行動裝置使用。 RMS 共用應用程式藉由安裝 Office 增益集來整合 Office 應用程式，讓使用者得以從功能區直接且輕易地保護檔案和電子郵件。 它也會提供一般保護，來保護 Azure Rights Management 並未原生支援的檔案類型，以及提供文件追蹤網站，供使用者追蹤和撤銷他們所保護的檔案。

## 適用於 Windows 的 RMS 共用應用程式：安裝和設定
若要針對企業部署安裝及設定適用於 Windows 的 RMS 共用應用程式，請參閱 [Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)。

> [!TIP]
> 如果您想要快速地為單一電腦安裝和測試 RMS 共用應用程式，請參閱 [Rights Management 共用應用程式使用者指南](../rms-client/sharing-app-user-guide.md)的[下載及安裝 Rights Management 共用應用程式](../rms-client/install-sharing-app.md)。

## 行動平台的 RMS 共用應用程式：安裝和管理
若要安裝行動平台的 RMS 共用應用程式，請可以使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)的連結下載相關應用程式。 無需設定即可搭配使用 Azure RMS 與此應用程式。

**如果您有 Microsoft Intune**：由於 RMS 共用應用程式包括 Microsoft Intune 應用程式軟體開發套件，因此您擁有下列選項︰

-   對於 Intune 所註冊的裝置，您可以針對執行 iOS 和 Android 的裝置部署和管理 RMS 共用應用程式。 如需詳細資訊，請參閱 Intune 文件的[在 Microsoft Intune 主控台中設定及部署行動應用程式管理原則](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)。 在步驟 2，使用指示以發行原則管理應用程式。

-   對於非 Intune 所註冊的裝置，您可以為執行 Android 的裝置管理 RMS 共用應用程式。 如需詳細資訊，請參閱[使用 Microsoft Intune 建立及部署行動應用程式管理原則](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)。




<!--HONumber=Jul16_HO3-->


