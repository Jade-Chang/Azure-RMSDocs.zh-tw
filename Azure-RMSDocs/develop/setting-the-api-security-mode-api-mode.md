---
# required metadata

title: 設定 API 安全性模式 | Azure RMS
description: 選擇檔案 API 應用程式執行的安全性模式。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定 API 安全性模式

您可以使用 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函式選擇檔案 API 應用程式執行的安全性模式。

若要啟動您的應用程式並在*伺服器模式*中執行，呼叫 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函式，並將安全性模式設為 [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)。 根據預設，應用程式會以*用戶端模式* 執行(**IPC\_API\_MODE\_CLIENT**)。

如需*伺服器模式*的詳細資訊，請參閱[應用程式類型](application-types.md)。

**重要**  應該先設定安全性模式，再呼叫其他Rights Management Services SDK 2.1 函式。 設定安全性模式之後，便無法在目前的處理程序中變更。

 

## 相關主題

* [應用程式類型](application-types.md)
* [開發人員概念](ad-rms-concepts-nav.md)
* [**API 模式值**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 





<!--HONumber=Apr16_HO4-->


