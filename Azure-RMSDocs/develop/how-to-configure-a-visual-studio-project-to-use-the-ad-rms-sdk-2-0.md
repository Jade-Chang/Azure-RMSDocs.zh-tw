---
title: "設定 Visual Studio | Azure RMS"
description: "有關如何設定 Visual Studio 專案以使用 RMS SDK 2.1 的指示。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 28286a4c8a5fcc602afba5975cfe5133e8b6c55b


---

# 設定 Visual Studio

本主題包含如何設定 Visual Studio 專案以使用 Rights Management Services SDK 2.1 的相關指示。

## 必要條件

-   [安裝 SDK](install-the-rms-sdk.md)

**指示**

### 步驟 1︰設定 Visual Studio 專案以使用 RMS SDK 2.1

這些指示專屬於 Microsoft Visual Studio 2010。 如果您使用不同版本的 Microsoft Visual Studio，您的 [設定] 對話方塊外觀可能會稍有不同。

這些指示會套用至建置原生 32 位元應用程式。

1.  新增 RMS SDK 2.1 包含 Visual Studio 2010 專案的目錄。

    在 **[組態屬性]** 下，選取 **[VC++ 目錄]** 並將 RMS SDK 2.1 包含目錄 **$(MSIPCSDKDIR)\\inc** 加入 **[包含目錄]** 欄位中。

    ![組態屬性包含目錄欄位](../media/include_directories.png)

2.  將 RMS SDK 2.1 程式庫目錄新增至 Visual Studio 2010 專案。

    在 [組態屬性] 下，選取 [VC++ 目錄] 並將 RMS SDK 2.1 程式庫目錄新增至平台的 [程式庫目錄] 欄位。

    -   若為 Win32，請使用 **$(MSIPCSDKDIR)\\lib**
    -   若為 x64，請使用 **$(MSIPCSDKDIR)\\lib\\x64**

    ![組態屬性程式庫目錄欄位](../media/library_directories.png)

3.  新增 RMS SDK 2.1 程式庫檔案做為 Visual Studio 2010 相依性。

    在 **[連結器]** 下，選取 **[輸入]** 並將 RMS SDK 2.1 程式庫檔 **Msipc.lib** 和 **Msipc\_s.lib** 加入 **[其他相依性]** 欄位中。

    ![連結器程式庫相依性欄位](../media/additional_dependencies.png)

4.  新增 RMS SDK 2.1 動態連結程式庫 (DLL) 做為延遲載入 DLL。

    在 [連結器] 下，選取 [輸入] 並將 RMS SDK 2.1 DLL 檔案 **Msipc.dll** 新增至 [延遲載入 Dll] 欄位。

    ![連結器延遲載入程式庫欄位](../media/delay_loaded.png)

5.  建立產生的二進位版本資訊。

    在 [方案總管] 下，選取 [資源檔案] 並將您的二進位名稱新增至 [OriginalFileName] 欄位。

    ![方案總管資源檔案欄位](../media/original_file_name.png)

## 相關的主題

* [安裝 SDK](install-the-rms-sdk.md)
 

 



<!--HONumber=Oct16_HO1-->


