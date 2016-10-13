---
title: "了解使用限制 | Azure RMS"
description: "RMS 啟用的所有應用程式必須強制使用限制。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 1d1433eb4468fd74689243c1ca63134a406e0f96


---

# 了解使用限制

RMS 啟用的所有應用程式必須強制使用限制。 使用限制是一種情況，會在使用者嘗試執行某個動作 (例如， 列印文件)，但該文件的 RMS 原則沒有授予他們執行該動作的權限 (例如 「列印」權限) 時發生。

使用者對文件的權限可使用 [**IpcAccessCheck**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) 函式查詢。

## 了解使用限制

-   熟悉標準 RMS 權限

    應用程式可能會強制使用的 RMS 權限完整清單，請參閱[使用限制參考](usage-restriction-reference.md)。

    請注意，可以建立應用程式為您的情況定義、且超出標準 RMS 權限的特定權限。

-   識別使用限制強制點

    *使用限制強制點*是應用程式的控制流程中您必須強制使用限制的位置。 [使用限制參考](usage-restriction-reference.md)主題提供數個常見的強制點範例。

    評估您自己的應用程式，判斷哪些使用限制強制點較適用。

    您的應用程式可能不需要[使用限制參考](usage-restriction-reference.md)中所述的所有強制點。 例如，如果應用程式不允許使用者列印內容，就不需要檢查 **IPC\_GENERIC\_PRINT** 權限。

-   更新您的程式碼，在每個強制點執行存取檢查

    如需有關如何強制特定權限的指引，請參閱[使用限制參考](usage-restriction-reference.md)。

## 相關的主題

* [**IpcAccessCheck**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [使用限制參考](usage-restriction-reference.md)
 

 



<!--HONumber=Oct16_HO1-->


