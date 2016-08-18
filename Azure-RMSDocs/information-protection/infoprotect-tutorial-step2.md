---
title: "Azure Information Protection 快速入門教學課程步驟 2 | Azure Rights Management"
description: "簡介教學課程的步驟 2，可為組織快速試用 Microsoft Azure Information Protection，只有 4 個步驟，花費時間不超過 15 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3bc193c2-0be0-4c8e-8910-5d2cee5b14f7
translationtype: Human Translation
ms.sourcegitcommit: 09cb56aaa0d7d97073623c518aa331d591a376e3
ms.openlocfilehash: 65d758635b77ee7d6c423a1400a7621e8e05b14d


---

# 步驟 2︰設定及發佈 Azure Information Protection 原則

>*適用於：Azure Information Protection 預覽*

**[本資訊為初步資訊而且可能隨時變更。 ]**

雖然 Azure Information Protection 有預設原則，您不需設定即可使用，不過我們即將看看該原則並進行一些變更。

1. 登入 [Azure 入口網站](https://portal.azure.com)。 如果您想要測試保護，以及分類和標記，請以全域管理員身分登入，以便您擷取 Azure Rights Management 範本。
 
2. 在中樞功能表︰按一下 [新增]  >  [安全性 + 身分識別]  >  [Azure Information Protection (預覽)]  >  [建立]。

    這會建立 [Azure Information Protection] 刀鋒視窗，以便在下次您登入入口網站，您可以從中樞 [瀏覽] 清單選取服務。 

    > [!TIP] 
    > 選取 [釘選到儀表板]，在儀表板上建立 [Azure Information Protection] 磚，以便您可以在下次登入入口網站時略過瀏覽步驟。

3.  探索主要的 **Azure Information Protection** 刀鋒視窗，其中顯示自動建立的預設 Information Protection 原則：
    
    - 分類的標籤︰[個人]、[公用]、[內部]、[機密] 及 [密碼]。 閱讀每個分類標籤的工具提示以了解要如何使用標籤。 請注意，[密碼] 有兩個子標籤︰[All-Employees] (所有員工) 和 [我的群組]，它們提供分類如何有子類別的範例。

    - 根據預設設定，[內部]、[機密] 及 [密碼] 標籤皆設定了視覺標記 (例如，頁尾、頁首、浮水印)，而標籤都沒有設定保護。 此外，未設定三個全域設定，因此所有文件和電子郵件不需要有標籤，也沒有預設標籤，且使用者不需要在降低敏感度等級時提供理由。

    ![Azure Information Protection 快速入門教學課程步驟 3 - 預設原則](../media/info-protect-policy.png)

在教學課程中，我們將變更幾個全域設定，讓您可以查看其運作方式︰

-  **選取預設標籤**︰將此設為 [內部]。

- **降低敏感度等級時，使用者必須提供理由**︰將此設為 [開啟]。

我們現在將會變更其中一個標籤 [機密] 的設定：

1. 按一下 [機密] 標籤。

2. 在 [標籤: 機密] 刀鋒視窗中，您現在會看到每個標籤的可用設定。 進行下列變更：

    a. 如果您已啟用 Azure Rights Managment：在 [設定 RMS 範本以保護包含此標籤的文件與電子郵件] 區段中，如果您看到 [選取 RMS 範本來源]，請保留預設值 [Azure RMS]。 然後，針對 [選取 RMS 範本]，按一下下拉式方塊並選取預設範本 [\<您的組織名稱> - 機密]。 例如，如果您的組織名稱是 VanArsdel, Ltd，您會看到並選取 [VanArsdel, Ltd - 機密]。 如果您已停用這個預設 Azure Rights Management 範本，請選取替代範本。 不過，如果您選取部門範本，請確定您的帳戶包含在範圍內。
    
    如果未啟用 Azure Rights Management，則您無法使用此選項。
    
    b。 [Documents with this label have a watermark] (具有此標籤的文件有浮水印)：按一下 [開啟] 並在 [文字] 方塊中輸入您的組織名稱。 例如 **VanArsdel, Ltd**。 
    
    c. 按一下 [新增條件]，然後在 [條件] 刀鋒視窗中，選取下列項目︰
    
    - [Choose the type of condition] (選擇條件類型)：[內建]
    
    - [選取內建]：[信用卡號碼]
    
    - [Minimum number of occurrences] (發生次數下限)：**1**
    
    - [僅計算唯一值的出現次數]：[開啟]
    
    - 按一下 [儲存] 回到 [標籤: 機密] 刀鋒視窗。

3. 在 [標籤: 機密] 刀鋒視窗中，您會看到 [信用卡號碼] 會顯示為 [條件名稱]，且 [發生次數] 為 **1**。

4. [Select how this label is applied] (選取此標籤的套用方式) 保持為：[建議使用]

5. 在 [Enter notes for internal housekeeping] (輸入內部維護的附註) 方塊中，輸入 **For testing purposes only**。

6. 在此 [標籤: 機密] 刀鋒視窗中按一下 [儲存]，然後在主要的 [Azure Information Protection] 刀鋒視窗中，再次按一下 [儲存]。

7. 現在我們已進行變更並儲存，我們想要提供給使用者，因此按一下 [發行]，並按一下 [是] 以確認。

![Azure Information Protection 快速入門教學課程步驟 3 - 已設定預設原則](../media/info-protect-policy-configured.png)

您可以關閉 Azure 入口網站，或維持開啟，以在完成本教學課程後嘗試其他組態選項。

現在，您已經看過預設原則，並進行了一些變更，下一個步驟是安裝 Azure Information Protection 用戶端。

|如果您想要更多的資訊|其他資訊|
|--------------------------------|--------------------------|
|關於原則的設定選項|[設定 Azure Information Protection 原則](configure-policy.md)|


>[!div class="step-by-step"]
[&#171; 步驟 1](infoprotect-tutorial-step1.md)
[步驟 3 &#187;](infoprotect-tutorial-step3.md)


<!--HONumber=Aug16_HO2-->


