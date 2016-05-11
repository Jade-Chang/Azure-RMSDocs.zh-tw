---
# required metadata

title: AD RMS 伺服器 | Azure RMS
description: Rights Management Services (RMS) 的伺服器元件是由一組執行 Microsoft Internet Information Services 的 Web 服務實作。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a7f11e25-9d27-4083-b604-a2d437671d91

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# AD RMS 伺服器

本主題說明 RMS 伺服器的目的和功能。

Rights Management Services (RMS) 的伺服器元件是由一組執行 [Microsoft Internet Information Services](http://www.iis.net/overview) (IIS) 的 Web 服務實作。 您也可以透過 Azure 使用在雲端實作的 RMS。 如需使用Azure Rights Management 服務的詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

內部部署的伺服器請從 Windows Server 2008 開始，您可以將 RMS 服務加入做為角色，藉此安裝和設定它。 若要在更舊版的作業系統上安裝服務，請從 Microsoft 下載中心 [Microsoft Windows Rights Management Services 含 Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909) 下載。

在安裝的許多 Web 服務之中，以下幾個對應用程式開發很重要。

管理 - 裝載可讓您管理 RMS 的系統管理網站。 服務會在根憑證伺服器和授權伺服器上執行。 您可以使用 [Active Directory Rights Management Services Scripting API](https://msdn.microsoft.com/library/Bb968797) 撰寫系統管理指令碼。

帳戶憑證 - 建立的機器憑證可用來從 RMS 憑證階層和權限帳戶憑證中，識別與特定電腦關聯的使用者的電腦。 如需詳細資訊，請參閱[啟用使用者](https://msdn.microsoft.com/library/Cc530378)。

此服務會在根憑證伺服器上執行。

授權 - 發出的使用者授權讓使用者可以使用受保護的內容。 服務會在根憑證伺服器和授權伺服器上執行。

發佈 - 建立[建立發行授權](https://msdn.microsoft.com/library/Aa362355)。 服務會在根憑證伺服器和授權伺服器上執行。

預先憑證 - 讓伺服器可以代表使用者要求權限帳戶憑證 (RAC)。 RAC 使用來自 RMS 啟用的電腦憑證將使用者帳戶繫結至特定電腦或電腦群組，RAC 是用來讓取用者使用受保護的內容。 服務會在根憑證伺服器和授權伺服器上執行。

Service Locator - 將帳戶憑證、授權以及發佈服務的 URL 提供給 Active Directory，讓 RMS 用戶端可以找到它們。 服務會在根憑證伺服器和授權伺服器上執行。

 

## 相關主題 ##
* [概觀](ad-rms-overview.md)
* [Microsoft Internet Information Services](http://www.iis.net/overview)
* [啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management Services 含 Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API](https://msdn.microsoft.com/library/Bb968797)
* [啟用電腦](https://msdn.microsoft.com/library/Cc530377)
* [啟用使用者](https://msdn.microsoft.com/library/Cc530378)
* [建立發行授權](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Apr16_HO3-->


