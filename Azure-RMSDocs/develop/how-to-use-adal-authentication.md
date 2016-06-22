---
# required metadata

title: RMS 應用程式的 ADAL 驗證 | Azure RMS
description: 概述 ADAL 驗證的程序
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何︰使用 ADAL 驗證

使用 Azure Active Directory Authentication Library (ADAL) 向 Azure RMS 驗證您的應用程式。

藉由更新應用程式來使用 ADAL 驗證而不是 Microsoft Online 登入小幫手，您和您的客戶將能夠︰

- 利用多重要素驗證
- 安裝 RMS 2.1 用戶端，而不需要電腦的系統管理權限
- 認證您的 Windows 10 應用程式

## 兩種驗證方法

本主題包含兩種方法來驗證對應的程式碼範例。

- **內部驗證** - RMS SDK 所管理的 OAuth 驗證。

  如果您想要 RMS 用戶端在需要驗證時顯示 ADAL 驗證提示，請使用此方法。 如需如何設定您應用程式的詳細資訊，請參閱＜內部驗證＞一節。

  > [!Note] 如果您的應用程式目前搭配使用 AD RMS SDK 2.1 與登入小幫手，則建議您使用內部驗證方法作為您的應用程式移轉路徑。

- **外部驗證** - 您應用程式所管理的 OAuth 驗證。

  如果您想要您的應用程式管理它自己的 OAuth 驗證，請使用此方法。 使用這個方法，RMS 用戶端只有在需要驗證時才會執行應用程式所定義的回呼。 如需詳細範例，請參閱本主題結尾的＜外部驗證＞。

  > [!Note] 外部驗證並不代表可以變更使用者；RMS 用戶端一律會使用所指定 RMS 租用戶的預設使用者。

## 內部驗證

1. 遵循[為 ADAL 驗證設定 Azure RMS](adal-auth.md) 中的 Azure 設定步驟，然後回到下列應用程式初始化步驟。
2. 您現在已經準備好設定應用程式使用 RMS SDK 2.1 所提供的內部 ADAL 驗證。

若要設定 RMS 用戶端，請在呼叫 [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) 設定 RMS 用戶端之後，立即將呼叫加入 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 中。 請使用下列程式碼片段作為範例。

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## 外部驗證

請使用此程式碼作為管理驗證權杖的範例。
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

          IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
          {
              sizeof(IPC_OAUTH2_CALLBACK_INFO),
              pfGetADALToken,
              pContextForAdal
          };

          IPC_CREDENTIAL credentialContext =
          {
              IPC_CREDENTIAL_TYPE_OAUTH2,
              NULL
          };
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## 相關主題

* [資料類型](/rights-management/sdk/2.1/api/win/datatypes)
* [環境屬性](/rights-management/sdk/2.1/api/win/environmentproperties)
* [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreateoauth2token)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC_CREDENTIAL)
* [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC_NAME_VALUE_LIST)
* [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IIPC_OAUTH2_CALLBACK_INFO)
* [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC_PROMPT_CTX)
* [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IIPC_AAD_APPLICATION_ID)


<!--HONumber=Jun16_HO2-->


