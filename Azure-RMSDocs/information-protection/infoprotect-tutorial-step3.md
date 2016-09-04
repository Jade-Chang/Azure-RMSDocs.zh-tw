---
title: "Azure Information Protection 快速入門教學課程步驟 3 | Azure Rights Management"
description: "簡介教學課程的步驟 3，可為組織快速試用 Microsoft Azure Information Protection，只有 4 個步驟，花費時間不超過 15 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 209815b9-81c9-430c-a82f-32cac991449b
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 320cd688ba5aabcb966009907d568033149953e3


---

# 步驟 3：安裝 Azure Information Protection 用戶端 

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

在此步驟中，您將安裝 Azure Information Protection 用戶端，讓您剛才設定的原則下載至 Windows 電腦上，並在 Office 應用程式中顯示標籤。 

1. 在已安裝 Office (但目前未開啟 Word) 的電腦上，從 Microsoft 下載中心[下載 Azure Information Protection 用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)。 

2. 執行 **AZInfoProtection.exe** 並遵循提示來安裝用戶端。

    在本教學課程中，您是否選取安裝示範原則的選項並不重要，因為我們剛才設定的原則將會從 Azure 下載，並取代示範原則，如果已安裝的話。 不過，如果您只想要體驗預設標籤而不連線到 Azure Information Protection，可以使用示範原則選項。 

3. 請開啟 Word 和新的空白文件 (目前不要儲存)，確認已安裝用戶端。 如果提示您輸入使用者名稱和密碼，請輸入全域系統管理員帳戶的詳細資料。 文件載入時，您應該會看到兩個新項目︰

    - 在 [首頁] 索引標籤上，有新的 [保護] 群組，以及一個標籤為 [保護] 的按鈕。

        按一下 [保護] > [說明與意見反應]，然後在 [Microsoft Azure Information Protection] 對話方塊中，確認您的用戶端狀態。 它應該會顯示 [已安裝 Information Protection 原則] 和最近的連線時間。 確認顯示的使用者名稱對您的租用戶而言正確。

    - 新的列會顯示在功能區下；Information Protection 列。 它會顯示標題 [敏感度]，以及我們設定的預設標籤 [內部]。 
    
        ![Azure Information Protection 快速入門教學課程步驟 3 - 已安裝用戶端](../media/word2013-callouts2.png)

您已準備好進行最後一個步驟，觀看分類、標記和保護實作示範。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於安裝用戶端|[安裝 Azure Information Protection 用戶端](info-protect-client.md)|


>[!div class="step-by-step"]
[&#171; 步驟 2](infoprotect-tutorial-step2.md)
[步驟 4 &#187;](infoprotect-tutorial-step4.md)


<!--HONumber=Aug16_HO4-->


