---
title: "快速入門教學課程步驟 3 | Azure Information Protection"
description: "簡介教學課程的步驟 3，可讓貴組織快速試用 Microsoft Azure Information Protection，需時約 30 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: b5c87669c965d1e67b47dcfbd8ba97f1da41d104
ms.openlocfilehash: 042e168452d2b5cbc1eeec4fc06a3b0f137a5caf


---

# 步驟 3︰安裝用戶端和應用程式 

>*適用於：Azure Information Protection*

在此步驟中，您將先安裝 Azure Information Protection 用戶端，讓您剛才設定的原則下載至 Windows 電腦上，並在 Office 應用程式中顯示標籤。

其次，您將安裝 Rights Management 共用應用程式，以便安全地透過電子郵件共用文件，然後追蹤文件的使用狀況。 

這兩種安裝都會與 Office 應用程式整合，而且目前必須分開安裝。


## 安裝 Azure Information Protection 用戶端

1. 在已安裝 Office (但目前未開啟 Word) 的電腦上，從 Microsoft 下載中心[下載 Azure Information Protection 用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 

2. 執行 **AzInfoProtection.exe** 並依照提示安裝用戶端。

    在本教學課程中，您是否選取安裝示範原則的選項並不重要，因為我們剛才設定的原則將會從 Azure 下載，並取代示範原則，如果已安裝的話。 不過，如果您只想要體驗預設標籤而不連線到 Azure Information Protection，可以使用示範原則選項。 

## 安裝 Rights Management 共用應用程式 

1. 移至 Microsoft 網站上的 [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) 頁面。

2. 在 [電腦] 區段中，按一下 [適用於 Windows 的 RMS 應用程式] 的圖示並儲存 Setup.exe 檔案，以安裝 Microsoft Rights Management 共用應用程式。

3. 在 [安裝 Microsoft RMS]  頁面上，按 [下一步] ，並等候安裝完成。 如果系統提示您重新啟動電腦則按一下 [重新啟動]，否則請按一下 [關閉] 完成安裝。


## 確認安裝

請開啟 Word 和新的空白文件 (目前不要儲存)，確認安裝成功。 如果提示您輸入使用者名稱和密碼，請輸入全域系統管理員帳戶的詳細資料。 

文件載入時，您應該會看到三個新項目：

- 在 [首頁] 索引標籤上，有新的 [保護] 群組，以及一個標籤為 [保護] 的按鈕。

    按一下 [保護] > [說明與意見反應]，然後在 [Microsoft Azure Information Protection] 對話方塊中，確認您的用戶端狀態。 它應該會顯示 [已安裝 Information Protection 原則] 和最近的連線時間。 確認顯示的使用者名稱對您的租用戶而言正確。

- 此外，在 [常用] 索引標籤上，有新的 [RMS] 群組，以及一個標示為 [共用保護] 的按鈕。

- 功能區下會出現一個新的列：Information Protection 列。 它會顯示標題 [敏感度]，以及我們設定的預設標籤 [內部]。 
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 已安裝用戶端](../media/word2013-callouts2.png)

現在即可查看 Azure Information Protection 的運作方式。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於安裝 Azure Information Protection 用戶端|[安裝 Azure Information Protection 用戶端](../rms-client/info-protect-client.md)|
|關於安裝 Rights Management 共用應用程式和使用者指示|[Rights Management 共用應用程式使用者指南 (英文)](../rms-client/sharing-app-user-guide.md)|
|關於適用於 Windows 的 Rights Management 共用應用程式的指令碼式安裝以及更多技術資訊|[Rights Management 共用應用程式系統管理員指南 (英文)](../rms-client/sharing-app-admin-guide.md)|


>[!div class="step-by-step"]
[&#171; 步驟 2](infoprotect-tutorial-step2.md)
[步驟 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Sep16_HO4-->


