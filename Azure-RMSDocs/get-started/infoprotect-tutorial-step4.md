---
title: "快速入門教學課程步驟 4 | Azure Rights Management"
description: "簡介教學課程的步驟 3，可讓貴組織快速試用 Microsoft Azure Information Protection，需時約 30 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 468748c1-49d6-4c3e-a612-9c584acdc782
translationtype: Human Translation
ms.sourcegitcommit: ce1d0a700e0b69d71f5cb2e93f406124bc0ca581
ms.openlocfilehash: c9ed50317e18e86438b4393ce629d23d433c99fe


---

# 步驟 4：觀看分類、標記和保護實作示範 

>*適用於：Azure Information Protection*

現在您已開啟 Word 文件並安裝 Azure Information Protection 用戶端，您已準備好看看使用我們設定的原則來開始標記並保護您的文件有多麼容易。

分類和保護是在您儲存文件時發生，但在這樣做之前，我們將使用尚未儲存的文件來看看套用及變更標籤有多容易。

## 手動變更預設標籤

在 Information Protection 列中，選取 [個人] 標籤，並於出現提示時證明為何會降低分類層級：

![Azure Information Protection 快速入門教學課程步驟 4 - 提示確認為何降低](../media/info-protect-lower-justification.png)

選取 **[The previous label no longer applies]** (不再套用舊標籤)，然後按一下 **[確認]**。 您會看到 [敏感度] 值變更為 [個人]。

## 完全移除分類

在 Information Protection 列上，按一下 [個人] 旁的編輯標籤圖示。 這會顯示可用的標籤。 但不要選擇其中一個標籤，這次請按一下移除標籤圖示。 按一下 [確定]，確認並提供此動作的理由。  

您會看到 [敏感度] 值顯示 [未設定]，如果您未設定預設標籤，這便是使用者最初看到的樣子：

![Azure Information Protection 快速入門教學課程步驟 4 - 移除分類](../media/sensitivity-not-set.png)


## 查看標記和自動保護的建議提示

1. 在 Word 文件中，輸入有效的信用卡號碼，例如︰**4242-4242-4242-4242**。 

2. 儲存文件 (使用任何檔案名稱、任何位置)。 

3. 您現在看到提示︰**[It is recommended to label this file as Confidential]** (建議將這個檔案標記為機密)。 按一下 [立即變更]。

    ![Azure Information Protection 快速入門教學課程步驟 4 - 建議提示](../media/change-now.png)

    除了標籤設為 [機密] 的文件外，您會立刻看到貴組織名稱的浮水印橫跨頁面，並套用**敏感度︰機密**的頁尾。 

    文件也會受到您指定的 Azure Rights Management 範本保護，您可以在按一下 [檔案] 索引標籤，並檢視 [保護文件] 的資訊時進行確認。 如果您使用預設的機密範本，您會看到文件僅限內部使用者 (組織外的使用者將無法開啟文件) 的資訊，且其內容無法複製或列印。 身為文件擁有者，您可以複製及列印，但如果您將它以電子郵件傳送給組織中的另一位使用者，他們將無法執行這些動作。

既然您已了解分類、標籤和保護如何作用，接著看看與其他組織的人員共用文件時，要如何保護您的文件。 您甚至可以追蹤它們的用法以及撤銷存取權。

>[!div class="step-by-step"]
[&#171; 步驟 3](infoprotect-tutorial-step3.md)
[步驟 5 &#187;](infoprotect-tutorial-step5.md)



<!--HONumber=Sep16_HO4-->


