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
** 這個 SDK 內容不是最新版本。 很快就可以在 MSDN 上找到文件的[目前版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)。 **
# RMS 應用程式的 ADAL 驗證

使用 Azure ADAL 針對應用程式進行 Azure RMS 驗證，現在是 RMS 用戶端 2.1 的一部分。

藉由更新應用程式來使用 ADAL 驗證而不是 Microsoft Online 登入小幫手，您和您的客戶將能夠︰

- 利用多重要素驗證
- 安裝 RMS 2.1 用戶端，而不需要電腦的系統管理權限
- 認證您的 Windows 10 應用程式

## 兩種驗證方法

本主題包含兩種方法來驗證對應的程式碼範例。

- **內部驗證** - RMS SDK 所管理的 OAuth 驗證。 如果您想要 RMS 用戶端在需要驗證時顯示 ADAL 驗證提示，請使用此方法。 如需如何設定您應用程式的詳細資訊，請參閱＜內部驗證＞一節。

> [!NOTE] 如果您的應用程式目前搭配使用 AD RMS SDK 2.1 與登入小幫手，則建議您使用內部驗證方法作為您的應用程式移轉路徑。

- **外部驗證** - 您應用程式所管理的 OAuth 驗證。 如果您想要您的應用程式管理它自己的 OAuth 驗證，請使用此方法。 使用這個方法，RMS 用戶端只有在需要驗證時才會執行應用程式所定義的回呼。 如需詳細範例，請參閱本主題結尾的＜外部驗證＞。

> [!NOTE] 外部驗證並不代表可以變更使用者；RMS 用戶端一律會使用所指定 RMS 租用戶的預設使用者。

### 內部驗證

您需要下列項目：

- [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/en-us/) (免費試用版就已足夠)：
- Microsoft Azure Rights Management 訂用帳戶 (免費[個人版 RMS](https://technet.microsoft.com/en-us/library/dn592127.aspx) 帳戶就已足夠)。

> [!NOTE] 請詢問 IT 管理員您是否有 Microsoft Azure Rights Management 訂用帳戶，以讓 IT 管理員執行下面步驟。 如果您的組織沒有訂用帳戶，則應該讓 IT 管理員建立訂用帳戶。 此外，您的 IT 管理員應該使用工作或學校帳戶來訂閱，而不是 Microsoft 帳戶 (即 Hotmail)。

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

- 新增重新導向 URI，然後選擇 [下一步]。 重新導向 URI 必須是有效的 URI，而且對您的目錄而言是唯一的。 例如，您可以使用 `com.mycompany.myapplication://authorize` 這類項目。

![新增重新導向 URI](../media/RedirectURI.png)

- 在目錄中選取您的應用程式，然後選擇 **[設定]**。

![選擇 [設定]](../media/ConfigYourApp.png)

>[!NOTE] 複製 **[用戶端識別碼]** 和 **[重新導向 URI]**，並在設定 RMS 用戶端時儲存它們以供未來使用。

- 瀏覽至您應用程式設定的底端，然後選擇 **[其他應用程式的權限]** 下的 **[加入應用程式]** 按鈕。

![選取 [加入應用程式]](../media/PermissionsToOtherBtn.png)

- 現在，將此 GUID `00000012-0000-0000-c000-000000000000` 加入 **[STARTING WITH]** (開頭) 編輯方塊，然後選擇 [檢查] 按鈕。

![加入 GUID](../media/AddGUID.png)

- 選擇 **[Microsoft Rights Management]** 旁邊的加號 (+) 按鈕。

![選取 [+] 按鈕](../media/ChoosePlusBtn.png)

- 現在，請選擇對話方塊左下角的核取記號。

![選擇核取標記](../media/ChooseCheck.png)

- 您現在已經準備好將相依性新增至 Azure RMS 的應用程式。 若要新增相依性，請選取 **[其他應用程式的權限]** 下的新 **[Microsoft Rights Management Services]** 項目，然後選擇 **[委派的權限:]** 下拉式方塊下的 **[Create and access protected content for users]** (建立和存取受保護使用者內容) 核取方塊。

![設定權限](../media/AddDependency.png)

- 選擇入口網站中下方的**儲存**圖示，以儲存您的應用程式來保存變更。

![選取 [儲存]](../media/SaveApplication.png)

- 您現在已經準備好設定應用程式使用 RMS SDK 2.1 所提供的內部 ADAL 驗證。 若要設定 RMS 用戶端，請在呼叫 [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) 設定 RMS 用戶端之後，立即加入 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) 呼叫。 請使用下列程式碼片段作為範例。


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### 外部驗證

- 請使用此程式碼作為如何管理您自己的驗證 Token 的範例。


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey) { IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT { wstring wstrToken; HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken); return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr; };

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
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### 相關主題
- [資料類型](/rights-management/sdk/2.1/api/win/Data%20types)
- [環境屬性](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=Jun16_HO1-->


