---
# required metadata

title: 為什麼此 SDK 是更好的方式 | Azure RMS
description: 本主題說明 RMS SDK 2.1 如何對原始 Active Directory Rights Management Services SDK 進行重大改良。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 622D5C6E-07D5-4C71-A99D-9823C1FE6936
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 為什麼此 SDK 是更好的方式
本主題說明 Rights Management Services SDK 2.1 如何執行必要的開發人員工作來建立具備權限的應用程式，從而對原始 [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) 進行重大改良。

**API 介面** - API 介面已透過抽象概念大幅降低，使您免於探索眾多後端實作詳細資料。 從 RMS SDK 的一個內含 84 個函式的 API 介面，RMS SDK 2.1 僅包含 20 個 API 函式。 大部分的應用程式只需要使用此 API 介面的一小部分。

**加快時間** - 使用 RMS SDK 2.1，您將能夠遵循逐步指示來識別哪些應用程式的資源為機密，以及如何加以保護。 這與 RMS SDK 不同，您必須深入瞭解憑證、格式和拓撲，並撰寫複雜的程式碼來進行多執行緒處理。

**多重拓樸支援** - RMS SDK 2.1 可幫助您減少程式碼重寫；您的應用程式應該使用所有拓撲，因為我們已針對開發人員抽離拓樸複雜性。 使用 RMS SDK，您必須了解所有支援的拓撲，然後撰寫和測試每個拓撲的特定程式碼。

**未來的使用期限** - RMS SDK 2.1 可協助您盡量避免重寫您的權限提升程式碼；您的應用程式應該在任何 RMS 環境中使用，並在發行更新的核心 RMS 功能時自動利用新功能。 這與 AD RMS SDK 不同，您需要更新應用程式才能明確地利用任何新功能。

**重要注意事項**  
MSDN Library 的原始 [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379) 中的所有主題現在皆以下列支援聲明開頭：

AD RMS SDK 運用 Msdrm.dll 中的用戶端所公開的功能，適用於 Windows Server 2008、Windows Vista、Windows Server 2008 R2、Windows 7、Windows Server 2012 和 Windows 8。 它在後續版本中可能會變更或無法使用。 請改用 [Active Directory Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)，此版本是利用用戶端在 *Msipc.dll* 中公開的功能。

 

## 相關主題 ##
* [概觀](ad-rms-overview.md)
* [Active Directory Rights Management Services SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management Services SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Apr16_HO4-->


