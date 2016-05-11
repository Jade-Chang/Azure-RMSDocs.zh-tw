---
# required metadata

title: 設定測試環境 | Azure RMS
description: 具備權限的應用程式可以使用不同的伺服器選項進行測試。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4d32682c-754d-4e30-977d-95b08e0662cc

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 設定測試環境

具備權限的應用程式可以使用不同的伺服器選項進行測試。

重要  建議的最佳作法是先針對 AD RMS 伺服器，使用 AD RMS 生產前環境來測試 Rights Management Services SDK 2.1 應用程式。 然後，如果您希望客戶能夠搭配使用您的應用程式與 Azure RMS 服務，請移至測試該環境。 如需詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

 

### 先決條件

-   [安裝 SDK](create-your-first-rights-aware-application.md)

指示

### 步驟 1︰設定您的測試環境

若要測試具備權限的應用程式，您必須對專為生產前設定的 RMS 伺服器執行應用程式。 生產前 RMS 伺服器使用生產前/ISV 憑證階層來加密和解密檔案。

如需 AD RMS 憑證階層的詳細資訊，請參閱[了解憑證鏈結](understanding-certificate-chains.md)。

有兩個選項可用來針對 RMS 伺服器測試您的應用程式︰

-   您可以在 AD RMS ISV 整合環境上執行您的應用程式。 如果您正在執行 Windows Server 2012、Windows Server 2008 R2 或 Windows Server 2008，且已安裝 Hyper-V，您可以藉由建置使用 AD RMS 整合 VHD 的虛擬機器來部署 AD RMS ISV 整合環境。 AD RMS ISV 整合環境提供專為生產前設定的 RMS 伺服器，而且也安裝了 Active Directory Rights Management Services Client 2.1。 已設定 RMS 伺服器和用戶端的登錄設定。 若要測試您的應用程式，您要在部署整合環境的虛擬機器上執行應用程式。
-   您可以針對專為生產前設定且部署在網路上的 RMS 伺服器執行您的應用程式。 在此情況下，您也必須在執行應用程式的電腦上安裝並設定您 AD RMS Client 2.1。 如需如何完成此動作的資訊，請參閱[設定用戶端](how-to-configure-the-ad-rms-client-2-0.md)。 如需如何部署 RMS 伺服器，並針對生產前設定它的資訊，請參閱[安裝並設定伺服器](how-to-install-and-configure-an-rms-server.md)。

### 相關主題

* [如何使用](how-to-use-msipc.md)
* [AD RMS SDK 網路研討會附屬下載頁面](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [設定用戶端](how-to-configure-the-ad-rms-client-2-0.md)
* [安裝 SDK](create-your-first-rights-aware-application.md)
* [安裝及設定伺服器](how-to-install-and-configure-an-rms-server.md)
* [了解憑證鏈結](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


