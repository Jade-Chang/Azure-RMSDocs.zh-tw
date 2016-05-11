---
# required metadata

title: 測試具備權限的應用程式 | Azure RMS
description: 描述完成 RMS SDK 2.1 具備權限的應用程式測試所需的步驟。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 43b611a8-2cc0-49a8-9db9-e81321c38f7a

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
# 測試具備權限的應用程式

本主題描述完成 Rights Management Services SDK 2.1 具備權限的應用程式測試所需的步驟。

為了發行和取用受保護的內容，Rights Management Services (RMS) 應用程式使用許多不同類型的憑證和授權，其中每個包含憑證鏈結，最終導致傳回 Microsoft 憑證授權單位。 Microsoft 提供下列階層︰

-   生產前階層可用於開發和測試應用程式。
-   生產階層必須由發行的應用程式使用

我們建議您在開發應用程式時使用生產前階層。 如此一來，您不必與 Microsoft 簽署生產前授權合約即可運作。

> [!IMPORTANT]
> 建議的最佳作法是先針對 RMS 伺服器，使用 RMS 生產前環境來測試 RMS SDK 2.1 應用程式。 然後，如果您希望客戶能夠搭配使用您的應用程式與 Azure RMS 服務，請移至測試該環境。 如需詳細資訊，請參閱[啟用您的服務應用程式以使用以雲端為基礎的 RMS](how-to-use-file-api-with-aadrm-cloud.md)。

 

### 先決條件

-   RMS SDK 2.1 開發環境設定。 如需詳細資訊，請參閱[設定生產前開發環境](how-to-set-up-the-pre-production-development-environment.md)。
-   如需範例應用程式，請參閱 [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)。

指示

### 步驟 1：

建立並建置具備權限的應用程式。 請參閱上述的＜必要條件＞一節的選項。

### 步驟 2︰產生使用生產前憑證鏈結的應用程式資訊清單

執行之前，您必須為應用程式產生資訊清單。

注意：如果應用程式使用伺服器 API 模式 (IPC\_API\_MODE\_SERVER)，您不需要使用應用程式資訊清單。 您可以對生產 AD RMS 伺服器測試應用程式，而且不需要在切換到生產環境時取得生產授權。 如需伺服器模式應用程式的詳細資訊，請參閱[應用程式類型](application-types.md)。

 

這個程序也稱為簽署您的應用程式。 您可以使用生產憑證鏈結或與 SDK 一起安裝的生產前憑證鏈結來產生資訊清單。 我們建議您在開發期間使用生產前憑證鏈結。

如需金鑰和憑證鏈結的詳細資訊，請參閱[了解憑證鏈結](understanding-certificate-chains.md)。

如需有關如何簽署應用程式與生產憑證鏈結的資訊，請參閱[切換到生產環境](switching-to-the-production-environment.md)。

若要使用生產前憑證鏈結來產生應用程式資訊清單，請在您的開發電腦上執行下列步驟︰

1.  從安裝目錄將下列檔案複製到應用程式的相同資料夾中。

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\YourAppName.isv.mcf

2.  在應用程式資料夾中，將資訊清單組態檔 YourAppName.isv.mcf 重新命名為您的應用程式名稱 (包含 .mcf 副檔名)。 例如，若應用程式稱為 MyApp.exe，請將 YourAppName.isv.mcf 重新命名為 MyApp.exe.mcf。

3.  使用文字編輯器，將您的應用程式新增至資訊清單組態檔。 若要這樣做，請以您的應用程式名稱取代 .mcf 檔案內模組清單中的 &lt;YourAppName&gt;.exe 預留位置文字，例如，MyApp.exe。

    如果不修改使用 .mcf 檔案，簽署程序會產生錯誤。

4.  執行 Genmanifest.exe 來產生應用程式資訊清單。 這個程序也稱為簽署您的應用程式。 這項作業的輸出應該是 .man 檔案。 例如，如果應用程式稱為 MyApp.exe，且資訊清單組態檔稱為 MyApp.exe.mcf，請執行下列命令︰

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MyApp.exe.mcf MyApp.exe.man**

### 步驟 3︰執行您的應用程式

您可以從任何目錄中執行應用程式，但應用程式資訊清單 (MyApp.exe.man) 必須與可執行檔 (MyApp.exe) 位於相同的目錄。

-   **使用 RMS 整合環境**

    如果使用 RMS 整合環境來測試應用程式，請將應用程式可執行檔和應用程式資訊清單複製到整合環境上的任何目錄，然後執行應用程式。

    如需 RMS 整合環境的相關資訊，請參閱[設定測試環境](how-to-set-up-your-test-environment.md)。

-   **使用生產前伺服器組態**

    如果正在針對生產前設定的 RMS 伺服器測試應用程式，請確定您已在將執行應用程式的電腦上設定 Active Directory Rights Management Services Client 2.1，例如在開發電腦。 然後確認應用程式可執行檔和應用程式資訊清單位於該電腦的相同目錄，並執行您的應用程式。

    如需有關如何在電腦上設定用戶端的資訊，請參閱[設定用戶端](how-to-configure-the-ad-rms-client-2-0.md)。 如需安裝 RMS 伺服器的相關資訊，請參閱[安裝並設定伺服器](how-to-install-and-configure-an-rms-server.md)。

### 相關主題

* [如何使用](how-to-use-msipc.md)
* [設定用戶端](how-to-configure-the-ad-rms-client-2-0.md)
* [安裝及設定伺服器](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - 範例應用程式](how-to-build-your-first-application.md)
* [設定生產前開發環境](how-to-set-up-the-pre-production-development-environment.md)
* [切換至生產環境](switching-to-the-production-environment.md)
* [設定測試環境](how-to-set-up-your-test-environment.md)
* [了解憑證鏈結](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


