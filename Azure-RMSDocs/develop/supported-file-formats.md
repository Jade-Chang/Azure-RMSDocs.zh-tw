---
title: "支援的檔案格式 | Azure RMS"
description: "檔案 API 目前的版本支援 MS Office 檔案、PDF 的原生保護，以及所有其他檔案格式版本的 PFile 保護。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: e41d8d697d7c35beef84277bc5b9fd497d79cc10


---

# 支援的檔案格式

檔案 API 支援原生與 Pfile 格式。

## 支援的檔案格式

檔案 API 目前的版本支援 Microsoft Office 檔案、可攜式文件檔案 (PDF) 的原生保護，以及所有其他檔案格式版本的 PFile 保護。 PDF 檔案可以選擇性地套用 PFile 保護。

-   **原生保護**。 在原生保護中，會將檔案加密為基於 MIME 類型 (副檔名) 的 AD RMS 檔案格式。 使用檔案 API 原生保護的檔案，與使用原生保護的 AD RMS 啟用的應用程式預期的格式一致；例如，Office 2013、Office 2010 及 FoxIt PDF 閱讀程式。 原生保護僅支援 Office 檔案、PDF 檔案以及特定數量的其他檔案類型。 如需支援原生保護的檔案類型的詳細資訊，請參閱[檔案 API 組態](file-api-configuration.md)。
-   **PFile 保護**。 在 PFile 保護中，檔案會使用 AD RMS 保護的檔案 (PFile) 格式來加密。 檔案會加密為具有副檔名 .pfile 的檔案。 對 Office 檔案以外的所有檔案格式支援 PFile 保護。

系統管理員可以設定登錄機碼，設定是否以及應如何根據檔案的副檔名來保護檔案。 如需使用檔案 API 時如何設定檔案保護的詳細資訊，請參閱[檔案 API 組態](file-api-configuration.md)。

## 相關的主題

* [開發人員注意事項](developer-notes.md)
* [檔案 API 組態](file-api-configuration.md)
 

 



<!--HONumber=Aug16_HO4-->


