---
title: "安裝 Azure Information Protection 用戶端 | Azure Information Protection"
description: "安裝會新增 Information Protection 列到您 Office 應用程式的用戶端，以便您可以針對文件和電子郵件選擇分類標籤的指示。"
manager: mbaldwin
ms.date: 08/29/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: f8d4b7f154ab8b47cded0dd2f315dba33664c7ff


---

# 安裝 Azure Information Protection 用戶端

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

若要使用 Azure Information Protection 分類文件和電子郵件訊息，您必須安裝 Azure Information Protection 用戶端。 安裝此用戶端，除了會將 Information Protection 列新增到您的 Office 應用程式 (Word、Excel、PowerPoint、Outlook) 以顯示您組織的分類標籤之外，也會在 Word、Excel、PowerPoint 的 [常用] 索引標籤上新增新的 [保護] 群組，並具有名稱為 [保護] 的按鈕：

下圖顯示此 Information Protection 列，以及來自[預設原則](configure-policy-default.md)的標籤：

![具有預設原則的 Azure Information Protection 列](../media/info-protect-bar-default.png)

從 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=53018)下載 Azure Information Protection 用戶端。

在安裝用戶端之前，請先檢查您是否具備必要的作業系統版本和應用程式：[Azure Information Protection 需求](requirements-azure-infoprotect.md)。


## 手動安裝 Azure Information Protection 用戶端

1. [下載此用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)之後，請執行 **AZInfoProtection.exe**，並遵循提示安裝用戶端。 此安裝需要本機系統管理員權限。

    如果您無法連線到 Office 365 或 Azure Active Directory，但想基於示範用途使用本機原則來查看和體驗 Azure Information Protection 的用戶端，請選取安裝示範原則的選項。 當您的用戶端連線到 Azure Information Protection 服務時，您組織的 Azure Information Protection 原則將會取代此示範原則。 

2. 若要開始使用 Azure Information Protection 用戶端：如果您的電腦是執行 Office 2010，請重新啟動您的電腦。 針對其他版本的 Office，請重新啟動任何 Office 應用程式。

## 為使用者安裝 Azure Information Protection 用戶端

- 您可以使用命令列選項編寫指令碼並自動化 Azure Information Protection 用戶端的安裝。 若要查看安裝選項，請執行 `AzInfoProtection.exe /help`。

    例如，若要以無訊息方式安裝用戶端： `AzInfoProtection.exe /passive | quiet`


## 將 Azure Information Protection 用戶端解除安裝

您可以使用下列任一選項︰

- 使用 [控制台] 將程式解除安裝：按一下 [Microsoft Azure Information Protection]  >  [解除安裝]

- 重新執行 **AzInfoProtection.exe**，然後在 [修改安裝] 頁面上，按一下 [解除安裝]。 

- 執行 `AzInfoProtection.exe /uninstall`


## 驗證安裝、連線狀態或報告問題

1. 開啟 Office 應用程式，並於 [常用] 索引標籤的 [保護] 群組中，按一下 [保護]，然後按一下 [說明與意見反應]。

2. 在 [Microsoft Azure Information Protection] 對話方塊中，請注意下列事項：

    - [上次連線] 值可識別用戶端上一次連線到您組織的 Azure Information Protection 的時間。 用戶端在連線到服務的時候，如果發現目前的原則和最新的原則之間有所變更，便會自動下載最新的原則。 如果您在所顯示的時間之後有變更原則，請將 Office 應用程式關閉再重新開啟。

    - 系統會使用可識別帳戶的使用者名稱，來針對 Azure Information Protection 進行驗證。 此使用者名稱必須符合您用於 Office 365 或 Azure Active Directory 的帳戶。

    - Azure Information Protection 用戶端的版本。

    - 您可以使用 [傳送意見反應] 連結，將用戶端記錄檔自動附加到電子郵件訊息，以傳送給 Information Protection 團隊進行調查。

    - [執行診斷] 連結：此功能目前尚未實作。

## 檔案位置

用戶端檔案：   

- 針對 64 位元作業系統：**\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 針對 32 位元作業系統：**\Program Files\Microsoft Azure Information Protection**

用戶端記錄檔和目前安裝的原則檔：

- 針對 64 位元和 32 位元作業系統：**%localappdata%\Microsoft\MSIP**


## 後續步驟

若要變更 Information Protection 列上的標籤，您必須設定 Azure Information Protection 原則。 如需詳細資訊，請參閱[設定 Azure Information Protection 原則](configure-policy.md)。

如需如何自訂預設原則的範例，以及在 Office 應用程式中查看產生的行為，請嘗試 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)。 



<!--HONumber=Sep16_HO1-->


