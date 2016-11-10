---
title: "如何允許您的服務應用程式使用雲端式 RMS | Azure RMS"
description: "本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7df62371ba4a2eea0227c731cf90b3454993f533
ms.openlocfilehash: 28b85313e278455391040797ea2886bd9247abe2


---

# <a name="howto-enable-your-service-application-to-work-with-cloud-based-rms"></a>如何允許您的服務應用程式使用雲端式 RMS

本主題概述設定服務應用程式以使用 Azure Rights Management 的步驟。 如需詳細資訊，請參閱[開始使用 Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx)。

**重要**  
若要搭配 Azure RMS 使用 Rights Management Services SDK 2.1 服務應用程式，您必須建立自己的租用戶。 如需詳細資訊，請參閱 [Azure RMS 需求：支援 Azure RMS 的雲端訂閱](../get-started/requirements-subscriptions.md)。

## <a name="prerequisites"></a>必要條件

-   必須安裝與設定 RMS SDK 2.1。 如需詳細資訊，請參閱[開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)。
-   您必須藉由使用對稱金鑰選項，或其他方式來[透過 ACS 建立服務身分識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)，並從該程序記錄金鑰資訊。

## <a name="connecting-to-the-azure-rights-management-service"></a>連接到 Azure Rights Management 服務

-   呼叫 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)。
-   設定 [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注意**  如需詳細資訊，請參閱[設定 API 安全性模式](setting-the-api-security-mode-api-mode.md)

     
-   下列步驟為建立 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 結構執行個體的設定，其中以來自 Azure Rights Management Service 的連線資訊填入 *pcCredential* ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) 成員。
-   在您建立 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 結構的執行個體時，請使用對稱金鑰服務身分識別建立的資訊 (參閱本主題先前所列的必要條件) 設定 *wszServicePrincipal*、*wszBposTenantId* 和 *cbKey* 參數。

**注意**：由於探索服務的現有條件，如果您不在北美洲，因為不接受其他地區的對稱金鑰認證，所以您必須直接指定您的租用戶 URL。 這可透過 [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) 或 [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx) 函數的 [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx) 類型的 *pConnectionInfo* 參數完成。

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>產生對稱金鑰，並收集所需的資訊

### <a name="instructions-to-generate-a-symmetric-key"></a>產生對稱金鑰的指示

-   安裝 [Microsoft Online 登入小幫手](http://go.microsoft.com/fwlink/p/?LinkID=286152)
-   安裝 [Azure AD PowerShell 模組](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)。

**注意**：您必須是租用戶系統管理員才能使用 Powershell Cmdlet。

- 啟動 Powershell 並執行下列命令來產生金鑰

    `Import-Module MSOnline`

    `Connect-MsolService`(請輸入您的系統管理員認證)

    `New-MsolServicePrincipal`(請輸入顯示名稱)

- 在它產生對稱金鑰之後，它會輸出金鑰相關資訊，包含金鑰本身和 *AppPrincipalId*。

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>找出 **TenantBposId** 和 **Urls** 的指示

-   安裝 [Azure RMS PowerShell 模組](https://technet.microsoft.com/en-us/library/jj585012.aspx)。
-   啟動 Powershell 並執行下列命令來取得租用戶的 RMS 組態。

    `Import-Module aadrm`

    `Connect-AadrmService`(請輸入您的系統管理員認證)

    `Get-AadrmConfiguration`


- 建立 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 的執行個體，並設定一些成員。

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


如需詳細資訊，請參閱 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)。

-   建立 [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) 結構的執行個體，其中包含您的 [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 執行個體。

**注意**：*conectionInfo* 成員會利用來自前一次 `Get-AadrmConfiguration` 呼叫的 URL 進行設定，並且利用那些欄位名稱在此註明。

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

### <a name="identify-a-template-and-then-encrypt"></a>找出範本，然後加密

-   選取用於加密的範本
    呼叫傳入相同 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 執行個體的 [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   利用本主題稍早的範本，呼叫傳入相同 [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 執行個體的 [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)。

使用 [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) 的範例：

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

使用 [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx) 的範例：

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

您現在已完成啟用應用程式以使用 Azure Rights Management 所需的步驟。

## <a name="related-topics"></a>相關的主題

* [開始使用 Azure Rights Management](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [開始使用 RMS SDK 2.1](getting-started-with-ad-rms-2-0.md)
* [透過 ACS 建立服務識別](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)
 

 



<!--HONumber=Nov16_HO1-->


