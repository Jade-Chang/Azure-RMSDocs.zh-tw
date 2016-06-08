---
# required metadata

title: 了解憑證鏈結 | Azure RMS
description: 具備權限的應用程式需要公開金鑰組，以及可回到根信任之 Microsoft 憑證的憑證鏈結。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6AEA2162-82BF-4867-9285-111CD3FCD2F6
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 這個 SDK 內容不是最新版本。 很快就可以在 MSDN 上找到文件的[目前版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)。 **
# 了解憑證鏈結

開發具備權限的應用程式需要公開金鑰組，以及可回到根信任的 Microsoft 憑證的憑證鏈結。

## 憑證類型

Rights Management Services (RMS) 環境中使用的每個授權和憑證包含憑證鏈結，其可回到 Microsoft 憑證授權單位 (CA) 憑證。 Microsoft 提供兩個鏈結 (在其中的授權或憑證可以是巢狀)，即生產前憑證鏈結和生產鏈結。 我們建議您在開發應用程式時使用生產前憑證階層，讓您可以操作但不需與 Microsoft 簽署*生產授權合約*。 請注意，您也必須針對生產前環境設定 RMS 伺服器。

釋出您的應用程式之前，您必須切換為生產鏈結。 生產前憑證所保護的內容是較生產憑證更不安全。

公用和私用金鑰和生產前憑證隨附於 SDK，位於 `%MsipcSDKDir%\Bin` 資料夾的下列檔案中。

- **ISVTier5AppSigningPrivKey.dat** 包含私密金鑰，用來簽署應用程式開發期間所使用的資訊清單。
- **ISVTier5AppSigningPubKey.dat** 包含公開金鑰，其已簽署至生產前憑證階層。
- **ISVTier5AppSignSDK_Client.xml** 包含生產前憑證，用來產生應用程式開發期間所使用的資訊清單。

 

您可以使用憑證和私密金鑰來建立和簽署資訊清單，識別可以或必須載入到您的應用程式處理序空間的檔案，以及不得載入的檔案。 然後平台會載入資訊清單。

在應用程式開發期間，無論您是否已使用生產前憑證，準備好要釋出應用程式時，您必須產生新的金鑰組、向 Microsoft 取得生產憑證，並使用新的私密金鑰和憑證來建立和簽署應用程式資訊清單。

如需有關使用憑證鏈結以及應用程式簽署的詳細資訊，請參閱[切換至生產環境](switching-to-the-production-environment.md)。

## 相關主題

* [開發人員概念](ad-rms-concepts-nav.md)
* [切換至生產環境](switching-to-the-production-environment.md)
 

 


<!--HONumber=Jun16_HO1-->


