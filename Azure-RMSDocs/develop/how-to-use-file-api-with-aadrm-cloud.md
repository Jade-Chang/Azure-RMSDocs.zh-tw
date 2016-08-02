---
title: "如何允許您的服務應用程式使用雲端式 RMS | Azure RMS"
description: "本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79397c82d9478cbd55630a376fe2d12f3873ebc4
ms.openlocfilehash: fce408a8c7a1114375745c3783443b87cd80ba78


---

# 如何允許您的服務應用程式使用雲端式 RMS

本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。 如需詳細資訊，請參閱[開始使用 Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx)。

**重要**  
若要搭配 Azure RMS 使用 Rights Management Services SDK 2.1 服務應用程式，您必須建立自己的租用戶。 如需詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。

## 先決條件

-   必須安裝與設定 RMS SDK 2.1。 如需詳細資訊，請參閱[開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)。
-   您必須藉由使用對稱金鑰選項，或其他方式來[透過 ACS 建立服務身分識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)，並從該程序記錄金鑰資訊。

## 連接到 Azure Rights Management 服務

-   呼叫 [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)。
-   設定 [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注意**  如需詳細資訊，請參閱[設定 API 安全性模式](setting-the-api-security-mode-api-mode.md)

     
-   下列步驟為建立 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 結構執行個體的設定，其中以來自 Azure Rights Management Service 的連線資訊填入 **pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) 成員。
-   在您建立 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key) 結構的執行個體時，請使用對稱金鑰服務身分識別建立的資訊 (參閱本主題先前所列的必要條件) 設定 **wszServicePrincipal**、**wszBposTenantId** 和 **cbKey** 參數。

**注意** 由於探索服務的現有條件，如果您不在北美洲，因為不接受其他地區的對稱金鑰認證，所以您必須直接指定您的租用戶 URL。 這可透過 [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) 或 [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist) 的 [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) 參數完成。

## 產生對稱金鑰，並收集所需的資訊

### 產生對稱金鑰的指示

-   安裝 [Microsoft Online 登入小幫手](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安裝 [Azure AD PowerShell 模組](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

**注意**  您必須是租用戶系統管理員才能使用 Powershell 指令程式。

-   啟動 Powershell 並執行下列命令以產生金鑰         `Import-Module MSOnline`
            `Connect-MsolService` (輸入您的系統管理員認證)         `New-MsolServicePrincipal` (輸入顯示名稱)
-   在它產生對稱金鑰之後，它會輸出金鑰相關資訊，包含金鑰本身和 **AppPrincipalId**。


    因為未提供對稱金鑰，所以已建立下列對稱金鑰：ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### 找出 **TenantBposId** 和 **Urls** 的指示

-   安裝 [Azure RMS PowerShell 模組](https://technet.microsoft.com/en-us/library/jj585012.aspx)。
-   啟動 Powershell 並執行下列命令來取得租用戶的 RMS 組態。

    `Import-Module aadrm`

    `Connect-AadrmService` (輸入您的系統管理員認證)

    `Get-AadrmConfiguration`


-   建立 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key) 的執行個體，並設定一些成員。

    // 建立金鑰結構。
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // 利用服務建立的資訊設定每個成員。
    symKey.wszBase64Key = "您的服務主體金鑰"; symKey.wszAppPrincipalId = "您的應用程式主體識別碼"; symKey.wszBposTenantId = "您的租用戶識別碼";


如需詳細資訊，請參閱 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key)。

-   建立 [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) 結構的執行個體，其中包含您的 [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key) 執行個體。

**注意**  *conectionInfo* 成員會利用來自前一次 `Get-AadrmConfiguration` 呼叫的 URL 進行設定，並且利用那些欄位名稱在此註明。

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
    呼叫傳入相同 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 執行個體的 [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   利用本主題稍早的範本，呼叫傳入相同 [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 執行個體的 [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)。

使用 [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) 的範例：

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

使用 [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile) 的範例：

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

您現在已完成啟用應用程式以使用 Azure Rights Management 所需的步驟。

## 相關主題

* [開始使用 Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [透過 ACS 建立服務身分識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential_symmetric_key#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 



<!--HONumber=Jul16_HO4-->


