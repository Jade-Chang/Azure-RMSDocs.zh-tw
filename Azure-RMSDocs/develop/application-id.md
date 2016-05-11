---
# required metadata

title: 作法：取得 Azure 應用程式識別碼 | Azure RMS
description: 使用 Microsoft Rights Management SDK 4.2 建立 RMS 啟用應用程式需要與 RMS 小組建立協議。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834c5943-a724-4322-9035-060c1112fe22

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
# 作法：取得 Azure 應用程式識別碼

使用 Microsoft Rights Management SDK 4.2 建立 RMS 啟用應用程式需要與 RMS 小組建立協議。

## 概觀

使用 MS RMS SDK 4.2 建立與發行 RMS 啟用應用程式時也需要與 RMS 小組建立服務使用協議。 這份合約，又稱為 Rights Management 授權合約 (RMLA)，會引導您接受內容保護的合約，您將會代表使用者及/或內容擁有者支援該合約的應用程式行為 (遵循商務規則)。 身為 RMS 啟用應用程式的建立者，您和 RMS 小組的合約會因為代表此合約之「Azure 應用程式識別碼」的存在而強制執行，並可讓您的應用程式連接到 Azure AD 驗證服務。

## 處理

使用下列步驟來建立您的應用程式識別碼並簽署您與 RMS 小組的使用合約。

-   遵循[如何在 Azure 上建立應用程式識別碼](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx)主題中的指引來建立您的應用程式識別碼。
-   寫入至 RMS 小組以起始 RMLA 程序，傳送您的「應用程式識別碼」至 <askipteam@microsoft.com>。
-   簽署 RMLA 並將它傳回至 RMS 小組。
-   簽署 RMLA 之後，您應該在透過 clientID 參數呼叫驗證程式庫時傳遞應用程式識別碼。

    這是驗證呼叫在 [iOS/OS X 程式碼範例](ios-os-x-code-examples.md)主題中的外觀。


    // Retrieve token using ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



注意  如果 RMS 小組在 60 天內未收到您簽署的 RMLA，您的應用程式將會封鎖，無法驗證 Azure 驗證系統。

 

 

 


<!--HONumber=Apr16_HO3-->


