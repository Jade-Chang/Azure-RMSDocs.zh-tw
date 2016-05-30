---
# required metadata

title: 追蹤內容 |Azure RMS
description: 實作文件追蹤的基本指導方針
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 追蹤內容

本主題涵蓋了追蹤 Rights Management Services SDK 2.1 所保護之內容文件的基本實作指導方針。

文件追蹤是 Rights Management 系統的功能。 藉由在文件保護程序期間新增特定中繼資料，可以向追蹤服務入口網站註冊文件，網站進而提供數個追蹤選項。

使用這些 API 以文件追蹤中繼資料來新增/更新內容授權。

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    我們希望您設定所有的中繼資料屬性。 以下就是這些屬性，依類型排列。

    如需詳細資訊，請參閱[**授權中繼資料屬性類型**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)。

    -   **IPC\_MD\_CONTENT\_PATH**

        使用這個屬性來識別追蹤的文件。 在不可能提供完整路徑的情況下，只要提供檔案名稱。

    -   **IPC\_MD\_CONTENT\_NAME**

        使用這個屬性來識別追蹤的文件名稱。

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        使用這個屬性來指定何時要傳送通知。 如需詳細資訊，請參閱[**通知類型**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)。

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        使用這個屬性來指定通知類型。 如需詳細資訊，請參閱[**通知的喜好設定**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)。

    -   **IPC\_MD\_DATE\_MODIFIED**

        我們建議您在每次使用者按一下 [儲存] 後設定此日期。

    -   **IPC\_MD\_DATE\_CREATED**

        檔案的原始日期。

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

使用這些 API 中適當的一個將中繼資料新增至您的檔案或資料流。

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最後，使用此 API 在追蹤系統中註冊您的追蹤文件。

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

以下的程式碼片段顯示設定文件追蹤中繼資料和呼叫註冊追蹤系統的範例。



    HRESULT hr = S_OK;
    LPCWSTR wszOutputFile = NULL;
    wstring wszWorkingFile;
    IPC_LICENSE_METADATA md = {0};

    md.cbSize = sizeof(IPC_LICENSE_METADATA);
    md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
    md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
    //file origination date, current time for this example
    md.ftDateCreated = GetCurrentTime();
    md.ftDateModified = GetCurrentTime();

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

    /* This will contain the serialized license */
    PIPC_BUFFER pSerializedLicense;

    /* the context to use for the call */
    PCIPC_PROMPT_CTX pContext;

    wstring wstrContentName(“MyDocument.txt”);
    bool sendLicenseRegistrationNotificationEmail = FALSE;

    hr = IpcRegisterLicense( pSerializedLicense,
                              0,
                              pContext,
                              wstrContentName.c_str(),
                              sendLicenseRegistrationNotificationEmail);


## 相關主題


* [**授權中繼資料屬性類型**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**通知的喜好設定**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**通知類型**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=May16_HO2-->


