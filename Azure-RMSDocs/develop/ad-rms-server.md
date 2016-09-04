---
title: "AD RMS 伺服器 | Azure RMS"
description: "Rights Management Services (RMS) 的伺服器元件是由一組執行 Microsoft Internet Information Services 的 Web 服務實作。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: 609a507335cea4a0a12e3652366961526d348c33


---

# Server

本主題說明 RMS 伺服器的目的和功能，適用於 Azure 及 Windows Server。

**Azure RMS** - 如需使用 Azure Rights Management 服務的詳細資訊，請參閱[允許您的服務應用程式使用雲端式 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

> [!IMPORTANT] 
> 建議您透過 Azure RMS 開發及測試應用程式。

**Windows Server** - 若是內部部署伺服器，從 Windows Server 2008 開始，您可以將 RMS 服務新增為角色，藉此加以安裝和設定。 若要在更舊版的作業系統上安裝服務，請從 Microsoft 下載中心 [Microsoft Windows Rights Management Services 含 Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909) 下載。

在安裝的許多 Web 服務之中，以下幾個對 Windows Server 上 RMS Server 的應用程式開發很重要。

| Service | 描述 |
|---------|-------------|
| 系統管理 | 裝載可讓您管理 RMS 的管理網站。 服務會在根憑證伺服器和授權伺服器上執行。 您可以使用 Active Directory Rights Management Services Scripting API 撰寫系統管理指令碼。|
| 帳戶憑證 |建立機器憑證，以識別在 RMS 憑證階層中的機器，以及在使用者與特定電腦間建立關聯的權限帳戶憑證。 如需詳細資訊，請參閱＜啟用電腦＞及＜啟用使用者＞。<p><p>此服務會在根憑證伺服器上執行。 |
|授權 | 發行*使用授權*。 服務會在根憑證伺服器和授權伺服器上執行。|
|發行 | 建立*發行授權*，定義可在使用授權中列舉的原則。 如需詳細資訊，請參閱 [Creating an Issuance License](https://msdn.microsoft.com/library/Aa362355) (建立發行授權)。<p><p>服務會在根憑證伺服器和授權伺服器上執行。|
|預先憑證 | 允許伺服器代表使用者要求*權限帳戶憑證*。 服務會在根憑證伺服器和授權伺服器上執行。|
|服務定位器 | 向 Active Directory 提供帳戶憑證、授權及發行服務的 URL，以便 RMS 用戶端加以探索。 服務會在根憑證伺服器和授權伺服器上執行。|

## 相關的主題 ##
* [概觀](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services 含 Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API](https://msdn.microsoft.com/library/Bb968797)
* [啟用電腦](https://msdn.microsoft.com/library/Cc530377)
* [啟用使用者](https://msdn.microsoft.com/library/Cc530378)
* [建立發行授權](https://msdn.microsoft.com/library/Aa362355)

 

 



<!--HONumber=Aug16_HO4-->


