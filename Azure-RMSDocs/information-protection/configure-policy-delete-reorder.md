---
title: "如何刪除或重新排序 Azure Information Protection 標籤 | Azure Rights Management"
description: "透過在 Azure Information Protection 原則中設定此項，您可以刪除或重新排序使用者在 Information Protection 列上看到的標籤。"
manager: mbaldwin
ms.date: 08/10/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ae0f603f-a632-4ac5-a3f7-6358d4255eff
translationtype: Human Translation
ms.sourcegitcommit: c9f9211e7c1dcf293caf81475515114b5433d6a7
ms.openlocfilehash: 43b43657627135886f6d0be42fef41ba939bdae1


---

# 如何刪除或重新排序 Azure Information Protection 標籤

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

透過在 Azure Information Protection 原則中設定此項，您可以刪除或重新排序使用者在 Information Protection 列上看到的標籤。

![刪除或重新排序 Azure Information Protection 原則中的標籤](../media/info-protect-contextmenu.png)

相較於刪除標籤，如果您想要保留標籤設定但避免在 Information Protection 列上顯示，您可能只希望停用標籤。

透過排序來以邏輯性進展的方式為使用者在 Information Protection 列中顯示標籤。 例如，以敏感度從低到高的方式排序標籤，來讓使用者先看到敏感性最低的標籤，並逐步查看到敏感性最高的標籤。 [預設原則](configure-policy-default.md)會使用此設定。

> [!IMPORTANT]
>如果您針對標籤所設定的[條件](configure-policy-classification.md)可能會套用到多個標籤，您必須將標籤以敏感性從低到高的方式排序。 這種排序可確保評估條件時會套用敏感性最高的標籤。


使用下列指示來進行這些變更。

1. 如果您尚未這樣做，請登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Information Protection] 刀鋒視窗。 
    
    例如，在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 **Information**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗上，根據您要刪除、停用或重新排序標籤，執行下列其中一項動作：

    - 若要刪除標籤︰以滑鼠右鍵按一下您想要刪除的標籤，或是選取該標籤的操作功能表 (**...**)，按一下 [刪除此標籤]，並按一下 [是] 以確認。 然後按一下 [儲存]。 

    - 若要停用標籤︰選取您想要停用的標籤。 在 [標籤] 刀鋒視窗上，針對 [已啟用] 按一下 [關閉]，然後按一下 [儲存]。

    - 若要重新排序標籤︰以滑鼠右鍵按一下您想要重新排序的標籤，或是選取該標籤的操作功能表 (**...**)，按一下 [上移] 或 [下移]，直到標籤已位於您想要的排序。 然後按一下 [儲存]。 

3. 若要讓變更可供使用者使用，請按一下 [Azure Information Protection] 刀鋒視窗上的 [發佈]。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  





<!--HONumber=Aug16_HO4-->


