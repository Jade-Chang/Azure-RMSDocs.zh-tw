---
title: "設定 Azure Information Protection 原則 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 781632c5a28377339431cd6537b1b9e11d0a3259
ms.openlocfilehash: 0e31053a83c30d8552cfb78914d0d13baac25f42


---

# 設定 Azure Information Protection 原則

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

若要設定分類、標記和保護，您必須設定 Azure Information Protection 原則。 然後，此原則會下載到已安裝 [Azure Information Protection 用戶端](https://www.microsoft.com/en-us/download/details.aspx?id=53018)的電腦。

若要在 Azure Information Protection 預覽版期間設定 Azure Information Protection 原則：

1. 登入 [Azure 入口網站](https://portal.azure.com)。

2. 瀏覽至 [Azure Information Protection] 刀鋒視窗︰例如，在中樞功能表中，按一下 [瀏覽]，開始在 [篩選] 方塊中輸入 **Information Protection**。 從結果中，選取 [Azure Information Protection]。 

    然後您會看到 [Azure Information Protection] 刀鋒視窗，您可以在其中設定 Azure Information Protection 原則，該原則包含下列元素：

    - 使用者可在他們的 Office 應用程式中看見的 Information Protection 列標題與工具提示。

    - 可讓您和使用者分類文件及電子郵件的標籤。

    - 在使用者儲存文件和傳送電子郵件時強制執行分類的選項。

    - 設定預設標籤做為分類文件和電子郵件之起點的選項。

    - 在使用者選取比原始敏感度等級較低的標籤時，提示使用者提供理由的選項。


Azure Information Protection 隨附[預設原則](configure-policy-default.md)，其中包含 [個人]、[公用]、[內部]、[機密] 及[秘密] 標籤。 您可以使用預設標籤而不做任何變更、自訂它們，或將它們刪除並建立新標籤。

當您在 [Azure Information Protection] 刀鋒視窗上進行任何變更時，請按一下 [儲存] 以儲存變更，或按一下 [捨棄] 以還原至上次儲存的設定。 

當您完成想要的變更之後，請按一下 [發佈]。 

每當支援的 Office 應用程式啟動時，Azure Information Protection 用戶端會檢查是否有任何變更，並將變更下載為其 Azure Information Protection 原則。

## 設定組織的原則

使用下列資訊以協助您設定 Azure Information Protection 原則：

- [預設 Information Protection 原則](configure-policy-default.md)

- [如何設定全域原則設定](configure-policy-settings.md)

- [如何建立新標籤](configure-policy-new-label.md)

- [如何刪除或重新排序標籤](configure-policy-delete-reorder.md)

- [如何變更或自訂現有標籤](configure-policy-change-label.md)

- [如何設定標籤以套用保護](configure-policy-protection.md)

- [如何設定標籤以套用視覺標記](configure-policy-markings.md)

- [如何設定自動與建議分類的條件](configure-policy-classification.md)

## 後續步驟

如需如何自訂預設原則的範例，以及在 Office 應用程式中查看產生的行為，請嘗試 [Azure Information Protection 快速入門教學課程](infoprotect-quick-start-tutorial.md)。




<!--HONumber=Aug16_HO2-->


