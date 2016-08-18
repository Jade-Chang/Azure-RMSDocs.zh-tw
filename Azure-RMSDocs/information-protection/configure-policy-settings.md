---
title: "如何設定 Azure Information Protection 的全域原則設定 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
translationtype: Human Translation
ms.sourcegitcommit: b2263c212a1b869b778767493645f10ad821828f
ms.openlocfilehash: 508161474bf6fd7406668de3976206947de254de


---

# 如何設定 Azure Information Protection 的全域原則設定

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

Azure Information Protection 原則中有 3 個設定會套用至所有使用者及所有裝置：

![Azure Information Protection 原則全域設定](../media/info-protect-policy-settings.png)


若要設定這些設定：

1. 如果您尚未這樣做，請登入 [Azure 入口網站](https://portal.azure.com)，然後瀏覽至 [Azure Information Protection] 刀鋒視窗。 
    
    例如，在中樞功能表中，按一下 [瀏覽] 並開始在 [篩選] 方塊中輸入 **Information**。 選取 [Azure Information Protection]。

2. 在 [Azure Information Protection] 刀鋒視窗上，設定這些全域設定：

    - [所有文件和電子郵件必須有標籤]：當您將這個選項設為 [開啟] 時，所有儲存的文件和傳送的電子郵件都必須套用標籤。 標籤可能是由使用者手動指派、因[條件](configure-policy-classification.md)自動指派，或根據預設指派 (透過設定 [選取預設標籤] 選項)。 

    如果使用者在儲存文件或傳送電子郵件時沒有指派標籤，則會提示使用者選取標籤：

    ![新分類敏感度等級較低時的 Azure Information Protection 提示](../media/info-protect-enforce-label.png)

    - [選取預設標籤]：當您設定此選項時，請選取要指派給沒有標籤的文件與電子郵件的標籤。 如果標籤有子標籤，則您無法將該標籤設為預設值。 

    - [降低敏感度等級時，使用者必須提供理由]：當您將此選項設為 [開啟]且使用者將現有文件或電子郵件的標籤變更為較低敏感度等級的標籤 (例如從 [秘密] 變更為 [公用])，系統會提示使用者提供此動作的說明。 例如，使用者可能會說明文件已不再包含敏感性資訊。 該動作和使用者的理由將會記錄在該使用者的本機 Windows 事件記錄檔中︰[應用程式]  >  [Microsoft Azure Information Protection]。  

    ![新分類敏感度等級較低時的 Azure Information Protection 提示](../media/info-protect-lower-justification.png)

    此選項不適用於子標籤。

3. 若要儲存變更，請按一下 [儲存]。

4. 若要讓變更可供使用者使用，請按一下 [發佈]。

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。  












<!--HONumber=Aug16_HO2-->


