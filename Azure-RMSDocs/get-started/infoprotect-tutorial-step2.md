---
title: "快速入門教學課程步驟 1 | Azure Information Protection"
description: "簡介教學課程的步驟 2，可讓貴組織快速試用 Microsoft Azure Information Protection，需時約 30 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: b23022c5fbec3d4f6f19ab5017ecf9badf01a9e7
ms.openlocfilehash: c8cad9c4b6efe2630843bcb1618ecd535670e0fe


---

# 步驟 2︰設定及發佈 Azure Information Protection 原則

>*適用於：Azure Information Protection*

雖然 Azure Information Protection 有預設原則，您不需設定即可使用，不過我們即將看看該原則並進行一些變更。

1. 在新的瀏覽器視窗以您租用戶的全域管理員登入 [Azure 入口網站](https://portal.azure.com)。

2. 在 [中樞] 功能表中，按一下 [新增]，然後從 [MARKETPLACE] 清單中選取 [安全性 + 識別]。 在 [安全性 + 識別] 刀鋒視窗中，從 [精選應用程式] 清單中選取 [Azure Information Protection]。 在 [Azure Information Protection] 刀鋒視窗中，按一下 [建立]。

    這會建立 [Azure 資訊保護] 刀鋒視窗，以便您下次登入入口網站時，從中樞 [更多服務] 清單選取服務。 

    > [!TIP] 
    > 選取 [釘選到儀表板]，在儀表板上建立 [Azure 資訊保護] 磚，以便您可以在下次登入入口網站時略過瀏覽步驟。

3.  探索主要的 **Azure Information Protection** 刀鋒視窗，其中顯示自動建立的預設 Information Protection 原則：
    
    - 分類的標籤︰[個人]、[公用]、[內部]、[機密] 及 [密碼]。 閱讀每個分類標籤的工具提示以了解要如何使用標籤。 請注意，[密碼] 有兩個子標籤︰[All-Employees] (所有員工) 和 [我的群組]，它們提供分類如何有子類別的範例。

    - 根據預設設定，[內部]、[機密] 及 [密碼] 標籤皆設定了視覺標記 (例如，頁尾、頁首、浮水印)，而標籤都沒有設定保護。 另外有三個全域設定未經設定，因此所有文件和電子郵件都不需要有標籤，也沒有預設標籤，而且使用者不需要在降低分類層級時提供理由。

    ![Azure Information Protection 快速入門教學課程步驟 3 - 預設原則](../media/info-protect-policy.png)

## 變更預設範本的全域設定並提示輸入理由

在教學課程中，我們將變更幾個全域設定，讓您可以查看其運作方式︰

1. 將 [Select the default label] (選取預設標籤) 設定為 [內部]。

2. 將 [Users must provide justification to set a lower classification label, remove a label, or remove protection] (使用者必須提供理由，才能設定較低分類標籤、移除標籤或移除保護) 設定為 [開啟]。

## 設定要保護的標籤、浮水印及提示分類的條件

我們現在將會變更其中一個標籤 [機密] 的設定：

1. 按一下 [機密] 標籤。 
    
    在新的 [Label: Confidential] (標籤: 機密) 刀鋒視窗中，您現在會看到每個標籤的可用設定。 

2. 在 [Label: Confidential] (標籤: 機密) 刀鋒視窗中，找出 [Set RMS template for protecting documents and emails containing this label] (設定 RMS 範本以保護包含此標籤的文件與電子郵件) 區段：
    
    針對 [Select RMS template from] (RMS 範本選取來源) 選項，保留預設值 [Azure RMS]。 然後，針對 [選取 RMS 範本]，按一下下拉式方塊並選取預設範本 [\<您的組織名稱> - 機密]。 
    
    例如，如果您的組織名稱是 VanArsdel, Ltd，您會看到並選取 [VanArsdel, Ltd - 機密]： 
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 設定 Azure RMS 保護](../media/step2-select-rms-template.png)
    
    如果您已停用這個預設 Azure Rights Management 範本，請選取替代範本。 不過，如果您選取部門範本，請確定您的帳戶包含在範圍內。
    
3. 找出 [Set visual marking] (設定視覺標記) 區段：
    
    針對 [Documents with this label have a watermark] (具有此標籤的文件有浮水印) 設定，按一下 [開啟]，然後在 [文字] 方塊中輸入您的組織名稱。 例如 **VanArsdel, Ltd**： 
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 設定 Azure RMS 保護](../media/step2-configure-watermark.png)
    
    雖然您可以變更浮水印的大小、色彩和配置，我們仍會暫時保留預設值。
    
4. 找出 [Configure conditions for automatically applying this label] (設定自動套用此標籤的條件) 區段：
    
    按一下 [新增條件]，然後在 [條件] 刀鋒視窗中，選取下列項目︰
    
    a. **Choose the type of condition (選擇條件類型)**︰保留預設值 [內建]。
    
    b。 **選取內建**︰從下拉式清單中，選取 [信用卡號碼]。
    
    c. **Minimum number of occurrences (發生次數下限)**︰保留預設值 **1**。
    
    d. **Count occurrences with unique values only (僅計算唯一值的發生次數)**：保留預設值 [關閉]。
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 設定信用卡條件](../media/step2-configure-condition.png)
    
    按一下 [儲存] 回到 [標籤: 機密] 刀鋒視窗。

5. 在 [Label: Confidential] (標籤: 機密) 刀鋒視窗中，您會看到 [信用卡號碼] 顯示為 [條件名稱]，且 [發生次數] 為 **1**：
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 設定信用卡條件](../media/step2-see-condition.png)

6. **Select how this label is applied (選取此標籤的套用方式)**︰保留預設值 [建議使用]，而且不要變更預設原則提示：
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 建議的分類](../media/step2-keep-recommended.png)

7. 在 [Enter notes for internal housekeeping] (輸入內部清理的備註) 方塊中，輸入**僅限用於測試目的**：
    
    ![Azure Information Protection 快速入門教學課程步驟 3 - 輸入備註](../media/step2-type-notes.png)

8. 在此 [Label: Confidential] (標籤: 機密) 刀鋒視窗中，按一下 [儲存]。 然後，在主要的 [Azure Information Protection] 刀鋒視窗中，再按一次 [儲存]。

9. 現在我們已進行變更並儲存，我們想要提供給使用者，因此按一下 [發行]，並按一下 [是] 以確認。

![Azure Information Protection 快速入門教學課程步驟 3 - 已設定預設原則](../media/info-protect-policy-configured.png)

您可以關閉 Azure 入口網站，或維持開啟，以在完成本教學課程後嘗試其他組態選項。

現在，您已經看過預設原則，並進行了一些變更，下一個步驟是安裝 Azure Information Protection 用戶端和 Rights Management 共用應用程式。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於原則的設定選項|[設定 Azure Information Protection 原則](../deploy-use/configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 步驟 1](infoprotect-tutorial-step1.md)
[步驟 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Sep16_HO4-->


