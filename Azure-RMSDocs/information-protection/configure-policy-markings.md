---
title: "如何設定 Azure Information Protection 的視覺標記標籤 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 78b68c7a502776c6492437e9b8a5c3f1ebf27f95


---

# 如何設定 Azure Information Protection 的視覺標記標籤

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

當您將標籤指派給文件或電子郵件訊息時，您可以選取數個選項讓選擇的分類顯而易見。 這些視覺標記為頁首、頁尾及浮水印：

在套用標籤及儲存文件時，視覺標記會套用至 Word、Excel 和 PowerPoint 文件。 若為電子郵件訊息，則會在電子郵件訊息傳送時套用視覺標記。

關於這些視覺標記的其他資訊：

- 頁首和頁尾適用於 Word、Excel、PowerPoint 和 Outlook。

- 浮水印適用於 Word、Excel 和 PowerPoint：

    - Excel：浮水印只會顯示在 [頁面配置] 和 [預覽列印] 模式，以及列印出來的文件上。

    - PowerPoint：浮水印會以背景影像的形式套用至母投影片。

- 您可以只指定文字字串，或使用[變數](#using-variables-in-the-text-string)，在套用頁首、頁尾或浮水印時，動態建立文字字串。 

您可以使用下列指示設定標籤的視覺標記。

1. 如果您尚未這樣做，請登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Information Protection] 刀鋒視窗。 
    
    例如，在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 **Information**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗中，選取您要設定視覺標記的標籤。

3. 在 [標籤] 刀鋒視窗上的 [設定視覺標記 (例如頁首或頁尾)] 區段，將視覺標記設定為您要的設定，然後按一下 [儲存]：

    - 若要設定頁首：針對 [含有此標籤的文件加上頁首]，如果您想要頁首，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定頁首文字、大小、色彩和頁首的對齊方式。
    
    - 若要設定頁尾：針對 [含有此標籤的文件加上頁尾]，如果您想要頁尾，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定頁尾文字、大小、色彩和頁首的對齊方式。
    
    - 若要設定浮水印：針對 [含有此標籤的文件加上浮水印]，如果您想要浮水印，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定浮水印文字、大小、色彩和頁首的配置。 

4. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 在文字字串中使用變數

您可以在頁首、頁尾或浮水印文字字串中使用下列變數︰

- `${Item.Label}` 針對選取的標籤

- `${Item.Name}` 針對檔案名稱或電子郵件主旨

- `${Item.Location}` 針對檔案路徑

- `${User.Name}` 針對文件或電子郵件的擁有者

- `${Event.DateTime}` 針對選取的標籤設定的日期和時間 
    
範例︰如果您為 [秘密] 標籤頁尾指定字串 `Document: ${item.name} Sensitivity: ${item.label}`，則套用至名為 project.docx 之文件的頁尾文字將為**project.docx 敏感度：秘密**。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  





<!--HONumber=Aug16_HO2-->


