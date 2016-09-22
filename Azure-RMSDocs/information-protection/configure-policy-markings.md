---
title: "如何設定 Azure Information Protection 的視覺標記標籤 | Azure Information Protection"
description: "當您將標籤指派給文件或電子郵件訊息時，您可以選取數個選項讓選擇的分類顯而易見。 這些視覺標記為頁首、頁尾及浮水印。"
manager: mbaldwin
ms.date: 09/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: df2676eeb062-f25a-4cf8-a782-e59664427d54
translationtype: Human Translation
ms.sourcegitcommit: 801ca11da602d4acb9c398c9a89aeb33e45cb0f4
ms.openlocfilehash: 999a0937bf741514ae8ee5ef819d4ab901c3304b


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

1. 如果您尚未這樣做，請在新的瀏覽器視窗中登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure 資訊保護] 刀鋒視窗。 
    
    例如，在中樞功能表按一下 [更多服務] 開始在 [篩選] 方塊中輸入**資訊**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗中，選取您要設定視覺標記的標籤。

3. 在 [標籤] 刀鋒視窗上的 [設定視覺標記 (例如頁首或頁尾)] 區段，將視覺標記設定為您要的設定，然後按一下 [儲存]：

    - 若要設定頁首：針對 [含有此標籤的文件加上頁首]，如果您想要頁首，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定頁首文字、大小、色彩和頁首的對齊方式。
    
    - 若要設定頁尾：針對 [含有此標籤的文件加上頁尾]，如果您想要頁尾，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定頁尾文字、大小、色彩和頁首的對齊方式。
    
    - 若要設定浮水印：針對 [含有此標籤的文件加上浮水印]，如果您想要浮水印，請選取 [開啟]；若不想要則選取 [關閉]。 如果您選取 [開啟]，請接著指定浮水印文字、大小、色彩和頁首的配置。 

4. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 在文字字串中使用變數

您可以在頁首、頁尾或浮水印文字字串中使用下列變數︰

- `${Item.Label}` 適用於選取的標籤。 例如︰內部

- `${Item.Name}` 適用於檔案名稱或電子郵件主旨。 例如︰JulySales.docx

- `${Item.Location}` 適用於文件的路徑和檔案名稱，以及電子郵件的電子郵件主旨。 例如︰\\\Sales\2016\Q3\JulyReport.docx

- `${User.Name}` 適用於文件或電子郵件的擁有者，依據 Windows 登入使用者名稱。 例如︰rsimone

- `${User.PrincipalName}` 適用於文件或電子的郵件擁有者，依據 Azure Information Protection 用戶端登入電子郵件地址 (UPN)。 例如︰rsimone@vanarsdelltd.com

- `${Event.DateTime}` 適用於所選標籤的設定日期和時間。 例如：8/16/2016 1:30 PM
    
範例︰如果您為 [秘密] 標籤頁尾指定字串 `Document: ${item.name}  Classification: ${item.label}`，則套用至名為 project.docx 之文件的頁尾文字將為**文件：project.docx 類別：秘密**。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  





<!--HONumber=Sep16_HO3-->


