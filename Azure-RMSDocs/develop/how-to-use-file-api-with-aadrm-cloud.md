---
# required metadata

title: 啟用您的服務應用程式以使用以雲端為基礎的 RMS | Azure RMS
description: 本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1f726c6a-68a5-421f-8ed9-9cbb051c205b

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 啟用您的服務應用程式以使用以雲端為基礎的 RMS

本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。 如需詳細資訊，請參閱[開始使用 Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)。

**重要**  
建議的最佳作法是先針對 RMS 伺服器，使用 RMS 生產前環境來測試 Rights Management Services SDK 2.1 應用程式。 然後，如果您希望客戶能夠搭配使用您的應用程式與 Azure RMS 服務，請移至測試該環境。

若要使用 RMS SDK 2.1 服務應用程式搭配 Azure RMS，如果您沒有 Azure RMS 租用戶，您必須要求一個。 透過租用戶要求傳送郵件給 <rmcstbeta@microsoft.com>。

## 先決條件

-   必須安裝與設定 RMS SDK 2.1。 如需詳細資訊，請參閱[開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)。
-   您必須藉由使用對稱金鑰選項，或其他方式來[透過 ACS 建立服務身分識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)，並從該程序記錄金鑰資訊。

## 連接到 Azure Rights Management 服務

-   呼叫 [IpcInitialize](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)。
-   設定 [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)。


    int mode = IPC_API_MODE_SERVER;
    IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


注意  如需詳細資訊，請參閱[設定 API 安全性模式](setting-the-api-security-mode-api-mode.md)

     

-   下列步驟為建立 [IPC\_PROMPT\_CTX](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 結構以及利用來自 Azure Rights Management 服務之連線資訊填入的 pcCredential ([IPC\_CREDENTIAL](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) 成員的執行個體設定。
-   在您建立 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 結構的執行個體時，使用對稱金鑰服務身分識別建立的資訊 (請參閱本主題稍早所列的必要條件) 來設定 wszServicePrincipal、wszBposTenantId 和 cbKey 參數。

注意   由於現有的條件與我們的探索服務，如果您不在北美，不接受其他地區的對稱金鑰認證，因此您必須直接指定您的租用戶 URL。 這可透過 [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 或 [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist) 的 [IPC\_CONNECTION\_INFO](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) 參數完成。

## 產生對稱金鑰，並收集所需的資訊

### 產生對稱金鑰的指示

-   安裝 [Microsoft Online 登入小幫手](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安裝 [Azure AD PowerShell 模組](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

注意  您必須是租用戶系統管理員才能使用 Powershell 指令程式。


-   啟動 Powershell 並執行下列命令來產生金鑰
            `Import-Module MSOnline`
            `Connect-MsolService` (輸入您的系統管理員認證)
            `New-MsolServicePrincipal` (輸入顯示名稱)
-   在它產生對稱金鑰之後，它會輸出金鑰相關資訊，包含金鑰本身和 AppPrincipalId。



    The following symmetric key was created as one was not supplied
    ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp
    ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
    ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
    AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963



### 找出 TenantBposId 和 Urls 的指示

-   安裝 [Azure RMS PowerShell 模組](https://technet.microsoft.com/en-us/library/jj585012.aspx)。
-   啟動 Powershell 並執行下列命令來取得租用戶的 RMS 組態。

    `Import-Module aadrm`

    `Connect-AadrmService` (輸入您的系統管理員認證)

    `Get-AadrmConfiguration`


-   建立 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 的執行個體並設定一些成員。

    // 建立金鑰結構。
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // 利用服務建立的資訊設定每個成員。
    symKey.wszBase64Key = "您的服務主體金鑰";
    symKey.wszAppPrincipalId ="您的應用程式主體識別碼";
    symKey.wszBposTenantId ="您的租用戶識別碼";


如需詳細資訊，請參閱 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)。

-   建立 [IPC\_CREDENTIAL](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) 結構的執行個體，包含您的 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 執行個體。

注意  conectionInfo 成員會利用來自前一次對 `Get-AadrmConfiguration` 呼叫的 URL 設定，並且利用那些欄位名稱在此註明。

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### 找出範本，然後加密

-   選取用於加密的範本
    在相同的 [IPC\_PROMPT\_CTX](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 執行個體中呼叫 [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 傳遞。


    PCIPC_TIL pTemplates = NULL;
    IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),
           IPC_GTL_FLAG_FORCE_DOWNLOAD,
           0,
           &promptCtx,
           NULL,
           &pTemplates);


-   利用本主題稍早的範本，呼叫 [IpcfEncrcyptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)，並在相同的 [IPC\_PROMPT\_CTX](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 執行個體中傳遞。

使用 [IpcfEncrcyptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) 的範例：

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

使用 [IpcfDecryptFile](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile) 的範例：

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

您現在已完成啟用應用程式以使用 Azure Rights Management 所需的步驟。

### 相關主題

* [開發人員概念](ad-rms-concepts-nav.md)
* [開始使用 Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [透過 ACS 建立服務身分識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 


<!--HONumber=Apr16_HO3-->


