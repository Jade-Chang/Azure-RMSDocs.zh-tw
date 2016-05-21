---
# required metadata

title: 針對生產簽署應用程式 | Azure RMS
description: 本主題將引導您完成針對運作模式簽署應用程式的程序。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c73fde39-6e16-470c-800e-59ab04c78f5f

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
# 針對生產簽署應用程式

本主題將引導您完成針對運作模式簽署應用程式的程序。

## 簽署具備權限的應用程式

這些步驟假設您已經針對生產前階層簽署您的應用程式。 如果您尚未這麼做，請進行[測試具備權限的應用程式](running-your-first-application.md)中所述的程序。

一旦您從 Microsoft 收到生產憑證，您便具有下列檔案︰

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

將它們放在與 GenManifest.exe 和您的應用程式二進位檔 (.exe) 的相同目錄。

-   下列程序將逐步引導您完成使用生產憑證來建立新 MCF 檔案的程序︰

    -   在該新目錄中建立新的目錄並放置檔案。 使用 Notepad.exe 來為您的應用程式建立 MCF 檔案。 該檔案應該具有下列內容。

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   執行下列命令來簽署應用程式︰

        genmanifest.exe -chain ProductionCertificate.xml YourAppName.mcf YourAppName.exe.man

        如果 Genmanifest 成功，您只會看到下列文字︰

        如果 Genmanifest 失敗，您會看到錯誤訊息。

    -   您的 YourAppName.exe.man 應該一律放在與 YourAppName.exe 相同的目錄。

### 相關主題

* [如何使用](how-to-use-msipc.md)
* [測試具備權限的應用程式](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO3-->


