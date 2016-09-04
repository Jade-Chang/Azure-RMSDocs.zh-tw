---
title: "如何對已啟用權限的應用程式偵錯 | Azure RMS"
description: "下列主題說明如何偵錯應用程式及使用 Windows 事件記錄檔。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 31b2fe22bbbb31b991bdf88e408c943e6d2ba685


---

# 如何：對已啟用權限的應用程式偵錯

下列主題說明如何偵錯應用程式及使用 Windows 事件記錄檔。

## 偵錯您的應用程式

在 Rights Management Services SDK 2.1 中，會停用我們的執行階段的開發人員版本中的反偵錯檢查。

您可以使用下列登錄機碼來開啟偵錯追蹤。 (若要關閉偵錯追蹤，請將此值變更為 0。)不需要為此版本中的偵錯採取任何行動。


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### 使用 Windows 事件記錄檔的應用程式記錄

事件記錄檔的名稱是 "Microsoft-RMS-MSIPC/Debug"。 這表示在 Windows 事件檢視器中，您的記錄檔會顯示為 "Application and Services Logs\\Microsoft\\RMS\\MSIPC\\Debug"。

**注意**：記錄檔預設會啟用並設為詳細層級 3。

 

若要變更記錄功能的設定，您可以使用 Windows 事件檢視器或 Wevtutil (內建於 Windows 中的命令列工具) 的任一 UI。

透過 Wevtutil 介面，您可以控制記錄檔的詳細資訊層級。

此時，我們支援 3 個記錄層級︰

-   層級 2—錯誤
-   層級 3—警告
-   層級 4—資訊

例如，下列命令會啟用 MSIPC 事件記錄檔，並將詳細資訊層級設為資訊。

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**注意**：在 Windows 事件檢視器的 [檢視] 功能表上，選取 [顯示分析和偵錯記錄檔] 以顯示 MSIPC 偵錯記錄檔。

 

## 相關的主題

 

 



<!--HONumber=Aug16_HO4-->


