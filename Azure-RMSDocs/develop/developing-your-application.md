---
title: "開發您的應用程式 | Azure RMS"
description: "簡介如何使用 RMS SDK 2.1 開發應用程式。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/01/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4560a1cf3424ae4dddd3a0675b62e9c5e55de9fa
ms.openlocfilehash: 1f46d93a47fae3b7e7de334db73b7e7b65ea6eea


---

# <a name="developing-your-application"></a>開發您的應用程式

本主題包含已啟用 RMS 應用程式的核心層面基本指導，可以當作您的專屬應用程式開發基礎。

## <a name="introduction"></a>簡介

本主題中的指導以範例應用程式 *IPCHelloWorld* 為基礎，可協助引導您了解已啟用權限應用程式的基本概念和程式碼。 *IPCHelloWorld* 專案已經為 Rights Management Services SDK 2.1 設定完成。

### <a name="download-sample"></a>下載範例
- 請驗證您已向 Connect 網站註冊：
  - 如需註冊，請前往 [Connect](http://connect.microsoft.com)
  - 使用您的 Microsoft 帳戶登入
  - 前往 [Rights Management Connect 網站](https://connect.microsoft.com/site1170)
  - Join 
- 下載完整的 *IPCHellowWorld* 範例應用程式 [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)

如需如何設定新的專案以使用 RMS SDK 2.1 的資訊，請參閱[設定 Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)。



## <a name="loading-msipcdll"></a>載入 MSIPC.dll

在您呼叫任何 RMS SDK 2.1 函式之前，必須先呼叫 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 函式以載入 MSIPC.dll。

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## <a name="enumerating-templates"></a>列舉範本

RMS 範本會定義用來保護資料的原則，也就是定義允許存取資料及其權限的使用者。 RMS 範本安裝在 RMS 伺服器上。

下列程式碼片段會列舉來自預設 RMS 伺服器的可用 RMS 範本。

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

此呼叫會擷取安裝在預設伺服器上的 RMS 範本，並將結果載入 *pcTil* 變數指向的 [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx) 結構，然後顯示範本。

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## <a name="serializing-a-license"></a>將授權序列化

在您可以保護任何資料之前，您需要序列化授權並取得內容金鑰。 內容金鑰可用來加密機密資料。 序列化的授權通常會附加至加密的資料，並且供受保護資料的取用者使用。 取用者必須使用序列化授權呼叫 [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx) 函式取得內容金鑰，以將內容解密並取得與內容相關聯的原則。

為了簡單起見，請使用 [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) 傳回的第一個 RMS 範本將授權序列化。

通常，您會使用使用者介面對話方塊來允許使用者選取所需的範本。

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

執行此動作之後，您具備您需要附加至受保護資料的內容金鑰 *hContentKey* 和序列化的授權 *pSerializedLicense*。


## <a name="protecting-data"></a>保護資料

現在您已準備好使用 [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx) 函式為機密資料加密。 首先，您必須詢問 **IpcEncrypt** 函式加密資料的大小。

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

這裡的 *wszText* 包含您要保護的純文字。 [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx) 函式會在 *cbEncrypted* 參數中傳回加密資料的大小。

現在可配置記憶體給加密的資料。

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

最後，您可以執行實際加密。

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

在這個步驟之後，您具備可供取用者用來解密資料的加密資料 *pbEncrypted* 及序列化授權 *pSerializedLicense*。

## <a name="error-handling"></a>錯誤處理

在整個範例應用程式中，*DisplayError* 函式可用來處理錯誤。

      C++
      void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
      {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
      }

*DisplayError* 函式使用 [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx) 函式，從對應的錯誤程式碼收到錯誤訊息，並將其列印為標準輸出。

## <a name="cleaning-up"></a>清除

在您完成之前，您也需要釋放所有配置的資源。

      C++
      if (NULL != pbEncrypted) {
        LocalFree((HLOCAL)pbEncrypted);
      }

      if (NULL != pSerializedLicense) {
        IpcFreeMemory((LPVOID)pSerializedLicense);
      }

      if (NULL != hContentKey) {
        IpcCloseHandle((IPC_HANDLE)hContentKey);
      }

      if (NULL != pcTil) {
        IpcFreeMemory((LPVOID)pcTil);
      }

## <a name="related-topics"></a>相關的主題

- [開發人員指導與資訊](developer-notes.md)
- [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx)
- [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Nov16_HO1-->


