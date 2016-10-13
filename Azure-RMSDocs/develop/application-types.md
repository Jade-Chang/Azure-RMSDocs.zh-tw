---
title: "應用程式類型 | Azure RMS"
description: "本主題涵蓋您可能會選擇建立為具備權限的應用程式類型。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: dac322fedd1ac23660abb3b79261e8339ffd81ca


---

# 應用程式類型


本主題涵蓋您可能會選擇建立為具備權限的應用程式類型。

Rights Management Services SDK 2.1 目前支援下列應用程式類型

## 簡單的應用程式

簡單的應用程式可能是建置來加密提供之檔案的命令列工具。 如需簡單具備權限應用程式的範例，請參閱 [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)。

### 伺服器模式應用程式

*伺服器模式*的目標為取用、保護或處理 RMS 保護內容的非互動式應用程式。 其中一個範例是*資料外洩防護*應用程式，執行做為檔案伺服器上的服務，並且自動保護機密文件。 如需此應用程式類型的範例，請參閱 [IpcDlp 範例](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)。

如果您的應用程式使用*伺服器模式*，它應該以無訊息方式向 RMS 伺服器驗證。 不同於*用戶端模式*，RMS SDK 2.1 在無法以無訊息模式驗證時，它將不會開啟認證提示。 此外，以*伺服器模式*執行時，不需要任何應用程式資訊清單。

如需設定 API 安全性模式的詳細資訊，請參閱[設定 API 安全性模式](setting-the-api-security-mode-api-mode.md)。

### 豐富的用戶端應用程式

豐富的用戶端應用程式可讓使用者透過圖形化使用者介面 (GUI) 檢視和管理資料。 通常，出現在 GUI 中的資料是高價值和機密的，須慎防竊盜或意外揭露。 資訊保護支援通常會增強現有的案例，但不是開發應用程式的主要動機。

使用 RMS SDK 2.1 搭配豐富的用戶端應用程式可協助您︰

-   確定這項資料一律加密。

-   防止使用者擷取資料至未受保護的格式 (例如，避免使用剪貼簿複製並貼上)。

Microsoft 記事本是一個簡單的豐富用戶端應用程式。 Microsoft Office 是更複雜的豐富用戶端應用程式。

如需保護應用程式的詳細資訊，請參閱[了解使用限制](understanding-usage-restrictions.md)。

## 相關的主題

* [IpcDlp 範例](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)
* [設定 API 安全性模式](setting-the-api-security-mode-api-mode.md)
* [了解使用限制](understanding-usage-restrictions.md)



<!--HONumber=Oct16_HO1-->


