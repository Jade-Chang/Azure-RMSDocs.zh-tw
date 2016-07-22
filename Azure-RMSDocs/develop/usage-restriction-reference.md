---
title: "使用限制參考 | Azure RMS"
description: "使用限制由本主題中列出的常數定義。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 16E36039-0FD6-4A0A-82C8-2C9DB19D27DD
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2acf8095764e2c222881240985df8bccf8a64173
ms.openlocfilehash: 9788b067f9395b9e078e76994a2a8a79e95baf06


---

# 使用限制參考

使用限制由本主題中列出的常數定義。

AD RMS 權限欄中所列的每個使用者權限，均具有說明、強制端點和建議的強制執行方法。

| AD RMS 權限/描述 | 如何強制執行 |
|--------------------------|----------------|
|**IPC_GENERIC_ALL** <br><br> 授與使用者所有權限。 <br><br> **一般強制端點**：無 |此權限是由系統使用，通常不應直接勾選。 <br><br> [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) 使用此權限來決定是否要為使用者授與其他權限，如此範例中所示。<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`|
|**IPC_GENERIC_READ** <br><br> 讀取文件內容的權限。 <br><br> **一般強制端點**：文件載入|未載入或出現文件內容|
|**IPC_GENERIC_WRITE** <br><br> 編輯文件內容的權限 <br><br> **一般強制端點**：文件修改|進行可用來修改文件不可編輯內容的任何 UI 控制。 <br><br> 停用觸發文件變更的任何功能表項目。 **[編輯]** > **[剪下]**、**[編輯]** > **[貼上]** 和 **[插入]** 是典型的範例。 <br><br>停用觸發文件變更的任何捷徑功能表項目。|
|沒有 AD RMS 權限 <br><br> 沒有描述 <br><br> **一般強制端點**：儲存 | 停用 **[檔案]** > **[儲存]** 功能表。 <br><br> **注意**：此權限不會控制 **[檔案]** > **[另存新檔]**，因為該權限不代表變更原始文件。<br><br> 停用可以用來觸發儲存的任何鍵盤快速鍵 (例如，Ctrl+S)。<br><br> **提示**：最佳做法是將您的核心 **[檔案]** > **[儲存]** 程式碼更新為在使用者不需要此權限時失敗。 這可以做為若您遺漏可以用來觸發儲存的任何 UX 機制時的安全網。 |
|**IPC_GENERIC_EXTRACT** <br><br> 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 <br><br> **一般強制端點**︰複製到剪貼簿 | 停用 **[編輯]** > **[複製]** 功能表。 停用 **[編輯]** > **[剪下]** 功能表。 <br><br>停用任何捷徑功能表的 [複製] 和 [剪下]。<br><br>停用可以用來觸發複製的任何鍵盤快速鍵 (例如，Ctrl+C 或 Ctrl+X)。<br><br>更新 [**WM_CUT**](https://msdn.microsoft.com/library/windows/desktop/ms649023) 的視窗訊息處理常式，以在使用者沒有此權限時拒絕複製資料。 如果視窗使用預設的 Windows 提供的訊息處理常式，請將此視窗設為子類別，並為 **WM_COPY** 和 **WM_CUT** 提供您自己的處理常式。 |
|沒有 AD RMS 權限 <br><br> 沒有描述 <br><br> **一般強制端點**：另存新檔 |在您的 [另存新檔] 對話方塊中，停用可能會導致儲存文件而未受 RMS 保護的任何檔案格式。|
|沒有 AD RMS 權限 <br><br> 沒有描述 <br><br> **一般強制端點**：Alt+PrtScn|呼叫任何視窗上可以轉譯文件內容的 [**IpcProtectWindow**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcprotectwindow)。|
|**IPC_GENERIC_EXPORT** <br><br> 從受保護的格式擷取內容，並將它放在不同的 AD RMS 受保護格式的權限。 <br><br> **一般強制端點**：另存新檔|在您的 [另存新檔] 對話方塊中，停用儲存為任何其他檔案格式的能力。<br><br>**提示**：最佳做法是將您的核心 **[檔案]** > **[另存新檔]** 程式碼更新為在使用者嘗試將檔案儲存為不同的格式並且不具備此權限時失敗。 這可以做為若您遺漏可以用來觸發另存新檔的任何 UX 機制時的安全網。|
|**IPC_GENERIC_PRINT** <br><br> 列印文件內容的權限。 <br><br> **一般強制端點**：列印|停用 **[檔案]** > **[列印]** 功能表。<br><br>停用可以用來觸發列印的任何鍵盤快速鍵 (例如，Ctrl+P)。<br><br>停用可以用來觸發列印的捷徑功能表項目。<br><br>**提示**：最佳做法是將您的核心 **[檔案]** > **[列印]** 程式碼更新為在使用者不需要此權限時失敗。 這可以做為若您遺漏可以用來觸發列印的任何 UX 機制時的安全網。|
|**IPC_GENERIC_COMMENT** <br><br> 有些應用程式支援在文件中加入註解和註釋的能力，而無須更新核心文件內容。<br><br>此權限授與使用者存取這項功能。 <br><br> **一般強制端點**： <br><br> 檢閱 > 插入註解 <br><br> 檢閱 > 刪除註解 | 停用可用來修改文件註解或註釋的功能表項目。 **[檢閱]** > **[插入註解]** 和 **[檢閱]** > **[刪除註解]** 是範例。 <br><br>停用任何可能會觸發修改文件註解的鍵盤快速鍵。<br><br>**注意**：預設實作需要 **IPC_GENERIC_COMMENT** 和 **IPC_GENERIC_WRITE** 才能將新註解保存至檔案。 應用程式可以選擇對授與了 **IPC_GENERIC_COMMENT** 權限而未授與 **IPC_GENERIC_WRITE** 權限的情況加入支援。 在此情況下，它允許儲存，只要文件修改僅限於註解即可。|
|**IPC_VIEW_RIGHTS** <br><br> 沒有描述 <br><br> **一般強制端點**：N/A|系統強制使用。 除非授與此權限，否則系統將不允許開發人員從授權查詢[**使用者權限清單**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_user_rights_list)。
|**IPC_EDIT_RIGHTS** <br><br> 有些應用程式允許使用者修改使用者集合和 AD RMS 保護的內容的權限。<br><br>此權限授與使用者存取這項功能。 <br><br> **一般強制端點**︰應用程式權限編輯 UI 控制項|停用使用者存取可用於編輯文件的 RMS 原則的任何 UI。|

 

 

 



<!--HONumber=Jul16_HO3-->


