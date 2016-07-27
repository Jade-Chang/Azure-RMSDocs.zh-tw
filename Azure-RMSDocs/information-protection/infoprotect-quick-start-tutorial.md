---
title: "Azure Information Protection 快速入門教學課程 | Azure Rights Management"
description: "一個簡介教學課程，可為組織快速試用 Microsoft Azure Information Protection，只有 4 個步驟，花費時間不超過 15 分鐘。"
author: cabailey
manager: mbaldwin
ms.date: 07/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: cac95dec84f99d2e6caa3458dc8284defe2324bc
ms.openlocfilehash: 7dc988365c1fa86827d1a7edc33c0a2eb6180f0e


---

# Azure Information Protection 快速入門教學課程 

*適用於：Azure Information Protection 預覽*

使用此教學課程，可為組織快速試用 Azure Information Protection 預覽，只有 4 個步驟，花費時間不超過 15 分鐘。 (選擇性) 啟用 Azure Rights Management 服務、查看和修改預設 Azure Information Protection 原則、安裝 Azure Information Protection 用戶端，然後使用 Word 文件以查看分類、標記和保護實作示範。

本教學課程的目標對象是 IT 系統管理員和顧問，目的是協助他們評估 Azure Information Protection 是否能夠作為組織的企業資訊保護方案。 在生產環境中，會由系統管理員完成指示來啟動服務、設定 Information Protection 原則，以及為使用者安裝用戶端。 標記文件的指示會由使用者完成。 本教學課程包含這兩組指示，以示範分類、標記和保護組織資料的端對端案例。 

如果您對於完成本教學課程、使用預覽版本的 Azure Information Protection 有任何問題，或是想要看看其他人對它的意見，請前往 [Azure Information Protection Yammer 網站](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)。

## 必要條件 
若要完成本教學課程，您需要具備下列項目：

- 包含 Azure Rights Management 的任何訂用帳戶，可讓您存取預覽版本的 Azure Information Protection。 Azure Information Protection 可用於支援 Azure Rights Management 的所有區域。 如需可用訂用帳戶和免費試用連結的詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。

- Azure 的訂用帳戶，以便您可以存取 Azure 入口網站，設定 Azure Information Protection 原則。 如果您的組織尚無 Azure 訂用帳戶，您可以註冊免費試用以取得訂用帳戶：移至 [Azure 快速入門](https://account.windowsazure.com/organization) 頁面，並遵循指示進行。

  > [!TIP] 
  > 如果您需要取得其中一或兩個訂用帳戶，請事先進行，因為這項程序有時可能需要一段時間才能完成。

- 用來登入 Office 365 系統管理中心或是 Azure 傳統入口網站的全域系統管理員帳戶，如果您需要啟動 Rights Management 服務的話。 此帳戶也必須有電子郵件地址和工作電子郵件服務 (例如 Exchange Online 或 Exchange Server)。

- 執行 Windows (至少要是 Windows 7 Service Pack 1)，且已安裝 Office 2016、Office 2013 Service Pack 1 或 Office 2010 的電腦。 

- 如果您的組織中部署了 Active Directory Rights Management Services (AD RMS)︰電腦必須是先前未使用 AD RMS 的工作群組電腦。 如果您要保護文件，這是必要條件，且如此可確保電腦只從 Azure Rights Management 下載範本。 不支援電腦在同一時間連接至 AD RMS 和 Azure RMS。 如果您對移轉資訊有興趣，請參閱[從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。   

讓我們開始這次的教學。

>[!div class="step-by-step"]
[&#187;步驟 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO3-->


