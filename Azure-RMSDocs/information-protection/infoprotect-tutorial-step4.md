---
title: "Azure Information Protection 快速入門教學課程步驟 4 | Azure Rights Management"
description: "簡介教學課程的步驟 4，可為組織快速試用 Microsoft Azure Information Protection，只有 4 個步驟，花費時間不超過 15 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 07/15/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: e80ea074fb1f6e571b846969b15c08cf7108b11c
ms.openlocfilehash: dcb34eb8bfee6232d32245634dc56f717257b644


---

# 步驟 4：觀看分類、標記和保護實作示範 

*適用於：Azure Information Protection 預覽*

現在您已開啟 Word 文件並安裝 Azure Information Protection 用戶端，您已準備好看看使用我們設定的原則來開始標記並保護您的文件有多麼容易。

分類和保護是在您儲存文件時發生，但在這樣做之前，我們將使用尚未儲存的文件來看看套用及變更標籤有多容易。

### 手動變更預設標籤︰

- 在 Information Protection 列上，按一下 [內部] 旁的編輯標籤圖示。 這會顯示可用的標籤。 選擇 [個人]，系統會提示您說明為何會降低分類層級。 選取 [This file no longer requires that classification] (這個檔案不再需要該分類)，然後按一下 [確認]。  

    您會看到 [敏感度] 值變更為 [個人]。

    ![Azure Information Protection 快速入門教學課程步驟 4 - 提示確認為何降低](../media/confirm-lowering.png)

### 完全移除分類︰

- 在 Information Protection 列上，按一下 [個人] 旁的編輯標籤圖示。 這會顯示可用的標籤。 但不要選擇其中一個標籤，這次請按一下移除標籤圖示。 按一下 [確定]，確認並提供此動作的理由。  

    您會看到 [敏感度] 值顯示 [未設定]，如果您未設定預設標籤，這便是使用者最初看到的樣子。

    ![Azure Information Protection 快速入門教學課程步驟 4 - 移除分類](../media/sensitivity-not-set.png)


### 查看標記和自動保護的建議提示︰

1. 在 Word 文件中，輸入有效的信用卡號碼，例如︰**4242-4242-4242-4242**。 

2. 儲存文件 (使用任何檔案名稱、任何位置)。 

3. 您現在看到提示︰[It is recommended to label this file as Confidential] (建議將這個檔案標記為機密)。 按一下 [立即變更]。

    ![Azure Information Protection 快速入門教學課程步驟 4 - 建議提示](../media/change-now.png)

    您會立即在頁面上看到您的組織名稱浮水印，此外還有頁尾 [敏感度: 機密]。 

    如果您選擇套用 RMS 範本的選項，文件也會受到您指定之 Azure Rights Management 範本保護，您可以在按一下 [檔案] 索引標籤，並檢視 [保護文件] 的資訊時進行確認。 如果您使用預設的機密範本，您會看到文件僅限內部使用者 (組織外的使用者將無法開啟文件) 的資訊，且其內容無法複製或列印。 身為文件擁有者，您可以複製及列印，但如果您將它以電子郵件傳送給組織中的另一位使用者，他們將無法執行這些動作。

> [!NOTE]
>如果完成這些步驟時有任何問題，請在 [首頁] 索引標籤的 [保護] 群組中，按一下 [保護]，然後按一下 [說明與意見反應]。 
>
>在 [Microsoft Azure Information Protection] 對話方塊中，按一下 [傳送意見反應]。 這樣會寄送電子郵件給 Information Protection 團隊，並自動從您的電腦附加記錄檔，以協助診斷任何問題。

##  後續步驟

現在您已了解預設 Azure Information Protection 原則及其自訂方法，也了解 Word 文件的標記如何運作，請嘗試一些其他設定，看看它們如何在支援 Azure Information Protection 的其他 Office 應用程式中運作︰Excel、PowerPoint 及 Outlook。 如果在安裝 Azure Information Protection 用戶端時，這些應用程式已開啟，請關閉並重新開啟它們，然後再嘗試使用 Azure Information Protection。

例如，您可以將 Information Protection 列上的預設標題 [敏感度] 變更為您自己選擇的標題。 您可以變更工具提示、標籤色彩、標籤順序及其名稱。 您可以建立新的標籤，並定義您自己的自動規則。 您可以藉由設定大小、色彩，並從對角線變更為水平來微調您的浮水印。

請注意，如果使用 Excel 搭配浮水印，只有在 [頁面配置] 和 [列印預覽] 模式，以及列印出來時，才能看到它們。

您每次在 Azure 入口網站變更 Information Protection 原則的任何設定時，請記得**儲存**原則，然後**發行**它。 因為您可以在多個刀鋒視窗上進行變更，所以最好檢查所有刀鋒視窗都未將 [儲存] 按鈕顯示為已啟用，這表示您有未儲存的變更。 如果您發行新的變更時，Office 應用程式已開啟，請關閉並重新開啟您的應用程式，下載最新的原則。

您完成自己的測試後，可能發現參閱 [Azure Information Protection 常見問題集](faq.md)很有用。




<!--HONumber=Jul16_HO3-->


