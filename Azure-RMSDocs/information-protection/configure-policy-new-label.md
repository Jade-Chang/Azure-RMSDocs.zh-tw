---
title: "如何建立新的 Azure Information Protection 標籤 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b45faa5-0c9c-40d6-910a-f117e7b6e8a3
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: c2f8f3204e3d5947137e7e9111ba4eba2628293b


---

# 如何建立新的 Azure Information Protection 標籤

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

雖然 Azure Information Protection 有隨附可自訂的預設標籤，您也可以自行建立使用者可在 Information Protection 列上看見的標籤。

您可以新增新的標籤，或在需要額外的分類層級時新增新的子標籤到現有的標籤。 例如，屬於[預設原則](configure-policy-default.md)的 [秘密] 標籤就包含子標籤。

使用下列指示以新增新的標籤到 Azure Information Protection 原則。

1. 如果您尚未這樣做，請登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Information Protection] 刀鋒視窗。 
    
    例如，在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 **Information**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗上，執行下列其中一個動作：

    - 若要建立新標籤：按一下 [新增新的標籤]。

    - 若要建立新的子標籤：以滑鼠右鍵按一下您想要建立子標籤的標籤，或是選取該標籤的操作功能表 (**...**)，然後按一下 [新增子標籤]。

3. 在 [標籤] 或 [子標籤] 刀鋒視窗上，為新的標籤選取您想要的選項，然後按一下 [儲存]。

    > [!NOTE]
    >如需設定保護的詳細資訊，請參閱[如何設定標籤以套用保護](configure-policy-protection.md)。

4. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  





<!--HONumber=Aug16_HO2-->


