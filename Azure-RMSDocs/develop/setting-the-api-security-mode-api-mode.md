---
title: "如何設定 API 安全性模式 | Azure RMS"
description: "選擇檔案 API 應用程式執行的安全性模式。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: f10129cb907cafa0e0c717b02153bbcdea012959


---

# 如何：設定 API 安全性模式

您可以使用 [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函式選擇檔案 API 應用程式執行的安全性模式。

若要將您的應用程式初始化，以在*伺服器模式*中執行，請呼叫 [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 函式，並將安全性模式設為 [**IPC\_API\_MODE\_SERVER**](/information-protection/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)。 根據預設，應用程式會以*用戶端模式*執行 (**IPC\_API\_MODE\_CLIENT**)。

如需*伺服器模式*的詳細資訊，請參閱[應用程式類型](application-types.md)。

**重要**  應該先設定安全性模式，再呼叫其他Rights Management Services SDK 2.1 函式。 設定安全性模式之後，便無法在目前的處理程序中變更。

## 相關的主題

* [應用程式類型](application-types.md)
* [**API 模式值**](/information-protection/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 



<!--HONumber=Oct16_HO1-->


