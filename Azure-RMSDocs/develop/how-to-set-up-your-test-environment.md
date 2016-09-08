---
title: "測試您的應用程式 | Azure RMS"
description: "有關如何設定應用程式以供測試的指示。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 9cc96c7f4d75969ec75b1372a4a49499709b0d32


---

# 測試您的應用程式

本主題包含如何進行應用程式測試設定的指示。

## 指示

### 步驟 1︰安裝以進行測試

您可以使用在 Windows Server 上執行的 Azure RMS 或 RMS 伺服器進行測試，建議您先在 Azure RMS 上進行測試，若您的部署需要 RMS 伺服器，才使用 RMS 伺服器進行測試。

1. 若要使用 Azure RMS 進行測試，請參閱[如何：使用 ADAL 驗證](how-to-use-adal-authentication.md)。
2. 若要使用 RMS 伺服器進行測試，請參閱[如何︰安裝和設定 RMS 伺服器](how-to-install-and-configure-an-rms-server.md)。
3. 以下說明如何安裝開發人員執行階段。

   您必須在將要測試應用程式的電腦上安裝 Rights Management Service Client 2.1。
   - 如果您要在開發電腦以外的其他電腦上測試應用程式，可以從 [AD RMS Client 下載頁面](http://www.microsoft.com/en-us/download/details.aspx?id=38396)在該電腦上安裝 RMS Client 2.1。
   - 如果您將在開發電腦上測試您的應用程式，您應該已安裝 Rights Management Services SDK 2.1。 RMS Client 2.1 此時會以無訊息模式安裝。

    如需如何安裝 RMS SDK 2.1 的資訊，請參閱[安裝 SDK](install-the-rms-sdk.md)。

## 備註

本主題中的指引並不完整。 如需如何設定 RMS Client 2.1 的詳細資訊，請參閱 [RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx) (RMS Client 2.1 部署注意事項)。

### 相關的主題

* [如何安裝和設定 RMS 伺服器](how-to-install-and-configure-an-rms-server.md)
* [如何︰使用 ADAL 驗證](how-to-use-adal-authentication.md)
* [安裝 SDK](install-the-rms-sdk.md)
* [RMS Client 2.1 部署注意事項](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 



<!--HONumber=Aug16_HO4-->


