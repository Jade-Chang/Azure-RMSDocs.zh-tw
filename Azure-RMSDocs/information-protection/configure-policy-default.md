---
title: "預設 Azure Information Protection 原則 | Azure Rights Management"
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 977cbf2f45cab75aaca9c2a16dd1564c2af2fe4a


---

# 預設 Azure Information Protection 原則

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

請使用下列資訊以了解設定 Azure Information Protection 預設原則的方式。 如果您修改了預設原則，您可以參考這些值來將原則還原為預設值。

## Information Protection 列

標題：**敏感度**

工具提示：**資訊敏感度由四個不同等級組成 (公用、內部、機密、秘密)，可讓使用者識別將資訊公開給企業內部或外部未經授權之使用者的風險。**


## 標籤

預設標籤一共有 5 個，並含有下列設定：

### **個人**

工具提示：**僅供個人使用。此資料不會受到組織監視。個人資訊不能包含任何商務相關的資料。**

色彩：淺綠色

視覺標記：無

條件：無

保護：否

----


### **公用**

工具提示︰**此為內部資訊，可供公司內部或外部的所有人員使用。**

色彩︰綠色

視覺標記：無

條件：無

保護：否

----

### **內部**

工具提示︰**此資訊包含廣泛的內部商務資料，可供所有員工使用，並與授權的客戶或商務合作夥伴共用。內部資訊的範例，包括公司原則和大部分的內部通訊。**

色彩：藍色

視覺標記：頁尾 (文件和電子郵件)

條件：無

保護：否

----

### **機密**

工具提示︰**此資料包含敏感性商務資訊。向未經授權的使用者公開此資料可能會對組織造成損害。機密資訊的範例，包括員工資訊、個別客戶專案或合約，以及銷售帳戶資料。**

色彩︰橙色

視覺標記：頁尾 (文件和電子郵件)

條件：無

保護：否

----

### **秘密**

工具提示：**此資料包含必須加以保護的公司高度敏感性資訊。向未經授權的使用者公開秘密資料可能會對組織造成嚴重損害。秘密資訊的範例，包括個人識別資訊、客戶記錄、原始碼，以及預先宣布的財務報告。**

色彩：紅色

視覺標記：頁尾 (文件和電子郵件)

條件：無

保護：否

----


## 子標籤

預設子標籤一共有 2 個，並含有下列設定：

### [秘密] > [全體公司]

工具提示︰**此資料包含敏感性商務資訊，並允許所有公司員工存取。**

視覺標記：無

條件：無

保護：否

----

### [秘密] > [我的群組]

工具提示︰**此資料包含敏感性商務資訊，並僅允許員工群組存取。**

視覺標記：無

條件：無

保護：否

## 全域設定

所有文件和電子郵件必須有標籤 (自動套用或由使用者套用)：關閉

選取預設標籤：無

降低敏感度等級時，使用者必須提供理由 (例如，從 [機密] 變更為 [公用])：關閉

## 後續步驟

如需關於設定 Azure Information Protection 原則的詳細資訊，請使用[設定組織的原則](configure-policy.md#configuring-your-organization-s-policy)一節中的連結。 



<!--HONumber=Jul16_HO5-->


