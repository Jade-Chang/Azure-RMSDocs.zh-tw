---
title: "為 ADAL 驗證設定 Azure RMS | Azure RMS"
description: "概述以 Azure ADAL 為基礎的驗證設定步驟"
keywords: "驗證, RMS, ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 9b912a2a66838dc6e6a3b227bcfe4ac589fe06c1


---

# 為 ADAL 驗證設定 Azure RMS

本主題描述以 Azure ADAL 為基礎的驗證設定步驟。

## Azure 驗證設定

您需要下列項目：

- [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/en-us/) (免費試用版就已足夠)。 如需詳細資訊，請參閱[使用者如何為個人註冊 RMS](../understand-explore/rms-for-individuals-user-sign-up.md)
- Microsoft Azure Rights Management 訂用帳戶 (免費[個人版 RMS](https://technet.microsoft.com/en-us/library/dn592127.aspx) 帳戶就已足夠)。

> [!NOTE] 
> 請詢問 IT 管理員您是否有 Microsoft Azure Rights Management 訂用帳戶，以讓 IT 管理員執行下面步驟。 如果您的組織沒有訂用帳戶，則應該讓 IT 管理員建立訂用帳戶。 此外，您的 IT 管理員應該使用*工作或學校帳戶*來訂閱，而不是 *Microsoft 帳戶* (即 Hotmail)。

註冊 Microsoft Azure 之後：

- 使用具有系統管理權限的帳戶，登入您組織的 [Azure 管理入口網站](https://manage.windowsazure.com)。

![Azure 登入](../media/AzurePortalLogin.png)

- 往下瀏覽至入口網站左側的 **[Active Directory]** 應用程式。

![選取 Active Directory](../media/AzureADPick.png)

- 如果您尚未建立目錄，請選擇入口網站左下角的 **[新增]** 按鈕。

![選取 [新增]](../media/AzureNewBtn.png)

- 選取 **[Rights Management]** 索引標籤，並確定 **[Rights Management 狀態]** 是 **[使用中]**、**[未知]** 或 **[未經授權]**。 如果狀態是 **[非使用中]**，請選擇入口網站中下方的 **[啟用]** 按鈕，並確認您的選擇。

![選擇 [啟用]](../media/RMTab.png)

- 現在，選取您的目錄，並選擇 [應用程式]，以在目錄中建立新的 *[原生應用程式]*。

![選取 [應用程式]](../media/CreateNativeApp.png)

- 然後選擇入口網站中下方的 **[新增]** 按鈕。

![選取 [新增]](../media/AddAppBtn.png)

- 在提示字元中，選擇 **[加入我的組織正在開發的應用程式]**。

![選取 [加入我的組織正在開發的應用程式]](../media/AddAnAppPick.png)

- 選取 **[原生用戶端應用程式]** 並選擇 **[下一步]** 按鈕，以命名您的應用程式。

![命名您的應用程式](../media/TellUsInput.png)

- 新增重新導向 URI，然後選擇 [下一步]。
  重新導向 URI 必須是有效的 URI，而且對您的目錄而言是唯一的。 例如，您可以使用 `com.mycompany.myapplication://authorize` 這類項目。

![新增重新導向 URI](../media/RedirectURI.png)

- 在目錄中選取您的應用程式，然後選擇 **[設定]**。

![選擇 [設定]](../media/ConfigYourApp.png)

>[!NOTE] 
> 複製 **[用戶端識別碼]** 和 **[重新導向 URI]**，並在設定 RMS 用戶端時儲存它們以供未來使用。

- 瀏覽至您應用程式設定的底端，然後選擇 **[其他應用程式的權限]** 下的 **[加入應用程式]** 按鈕。

>[!NOTE] 
> 根據預設，為 Windows Azure Active Directory 顯示的**委派權限**均為正確，只要選取一個選項：**[登入及讀取使用者設定檔]**。

![選取 [加入應用程式]](../media/PermissionsToOtherBtn.png)

- 現在，將此 GUID `00000012-0000-0000-c000-000000000000` 加入 **[STARTING WITH]** (開頭) 編輯方塊，然後選擇 [檢查] 按鈕。

![加入 GUID](../media/AddGUID.png)

- 選擇 **[Microsoft Rights Management]** 旁邊的加號按鈕。

![選取 [+] 按鈕](../media/ChoosePlusBtn.png)

- 現在，請選擇對話方塊左下角的核取記號。

![選擇核取標記](../media/ChooseCheck.png)

- 您現在已經準備好將相依性新增至 Azure RMS 的應用程式。 若要新增相依性，請選取 **[其他應用程式的權限]** 下的新 **[Microsoft Rights Management Services]** 項目，然後選擇 **[委派的權限:]** 下拉式方塊下的 **[Create and access protected content for users]** (建立和存取受保護使用者內容) 核取方塊。

![設定權限](../media/AddDependency.png)

- 選擇入口網站中下方的**儲存**圖示，以儲存您的應用程式來保存變更。

![選取 [儲存]](../media/SaveApplication.png)



<!--HONumber=Jul16_HO3-->


