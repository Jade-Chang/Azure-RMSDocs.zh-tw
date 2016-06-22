---
# required metadata

title: 如何使用加密設定 | Azure RMS
description: 這篇文章會將您導向我們的加密封裝
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何：使用加密設定

本主題會將您導向我們的加密套件，並顯示其部分程式碼使用片段。

## 支援 AES 256，新的預設值

假設您是對 RMS SDK 2.1 2015 年 3 月更新或更新版本進行建置，則使用 *AES 256* 式加密不需額外的程式碼，因為它是新的預設值。 我們鼓勵您慎重考慮將您的應用程式更新為此版本，以獲得額外的 *AES 256* 安全性優勢。

> [!IMPORTANT]
> 自 [2014 年 10 月版本](release-notes-rtm.md)起已提供 *AES 256* 受保護檔案的支援。 如果您正在執行使用早於 2014 年 10 月的 SDK 版本建置的應用程式，此更新會中斷您的應用程式。 請確定您要建置之應用程式的客戶正使用更新後的 SDK，或願意立即更新為您的應用程式的最新版本。

 
## API 加密支援

從 [2015 年 3 月更新](release-notes-rtm.md)開始，我們已經在我們的 API 和其相關聯的加密封裝中納入下列三個旗標︰

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (也就是已過時的演算法)

加密封裝旗標 (請參閱[**慣用的加密**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption)) 可搭配我們新的授權內容旗標 **IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE** 使用。

以下是一些簡單的程式碼片段，示範如何使用新的授權屬性。

## 已過時的演算法

我們將不再於 API 公開 **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** 旗標。 這表示如果未來的應用程式參考這個旗標，它們將不再編譯，但已使用它建置的應用程式仍將繼續運作，因為我們將會私下在 API 程式碼中採用旗標。

我們仍然可以藉由變更一個旗標來達成取得已被取代之舊加密演算法旗標的優點。 如需範例，請參閱下列程式碼片段。

## 使用 AES 256 CBC4K 保護檔案

不需要變更程式碼，*AES 256* CBC4K 是預設值。

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## 使用 AES-128 CBC4K 保護檔案

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## 使用 AES 128 ECB 保護檔案 (已過時的演算法)

這個範例也示範支援*已過時的演算法*的新方式。

    C++
    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

 

 


<!--HONumber=Jun16_HO2-->


