---
# required metadata

title: 常見的錯誤狀況和解決方案 | Azure RMS
description: 本主題包括使用 RMS SDK 2.1 開發人員工具時可能遭遇到的常見錯誤訊息。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: A5B95EB8-3528-4CFF-86FC-166613A5F4A3
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 這個 SDK 內容不是最新版本。 很快就可以在 MSDN 上找到文件的[目前版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)。 **
# 常見的錯誤狀況和解決方案
本主題包括使用 Rights Management Services SDK 2.1 開發人員工具時可能遭遇到的常見錯誤訊息。 它也提供建議的動作，在適用的情況下修正錯誤。

**重要** - 對於錯誤條件處理，一律在 SDK API 呼叫失敗後使用 [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) 呼叫，如此您會收到錯誤性質的完整資訊。

 

## 錯誤和動作 ##
下列清單包含一份錯誤常數、其相關聯的說明和建議動作，以解決錯誤狀況。

**錯誤** - *IPCERROR_DEBUGGER_DETECTED* - RMS SDK 2.1 偵測到偵錯工具

**動作** - RMS SDK 2.1 的開發人員版本不會檢查是否有任何偵錯工具。 可能的話，請使用這個版本 (RMS SDK 2.1) 來偵錯應用程式。
如果您必須偵錯 RMS SDK 2.1 的生產版本，請使用下列指導方針。

某些 RMS SDK 2.1 函數是設計在偵錯工具下執行︰
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

若要遵循這些函式呼叫來偵錯程式碼，您必須中斷處理序，並在函式呼叫完成後附加偵錯工具。 其中一個方法是使用 assert 陳述式來中斷至偵錯工具。 ASSERTE 巨集包含在 *Crtdbg.h* 標頭中。
如需 \_ASSERTE 的詳細資訊，請參閱 [\_ASSERT、\_ASSERTE 巨集](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)

**錯誤** - *IPCERROR_BROKEN_CERT_CHAIN* - 憑證鏈結不符。

**動作** - 根據您用來簽署 AD RMS 應用程式資訊清單的金鑰，確定階層金鑰包含正確值。
這些是簽署金鑰及其關聯值 (階層 **DWORD**)：
- ISV—1
- Production—0 或不存在

**錯誤** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* - 您正在使用以 ISV 簽署金鑰簽署的應用程式，但其嘗試與生產 AD RMS 伺服器通訊，或情形相反。

- 如果您使用 AD RMS 伺服器的開發人員版本，請確定您使用 ISV 簽署金鑰來簽署應用程式。
- 如果您使用 AD RMS 伺服器的生產版本，請確定您使用生產簽署金鑰來簽署應用程式。

**錯誤** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST* - 應用程式資訊清單無效。 重建二進位檔 (應用程式)，以及未重新產生資訊清單時，可能會發生此情況。

**動作** - 確定每次重建應用程式時會重新產生應用程式資訊清單。

## 相關主題 ##
* [開發人員注意事項](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [\_ASSERT、\_ASSERTE 巨集](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Jun16_HO1-->


