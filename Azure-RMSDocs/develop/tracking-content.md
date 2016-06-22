---
# required metadata

title: 如何啟用文件追蹤和撤銷 | Azure RMS
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
<<<<<<< HEAD

# 追蹤內容
=======
>>>>>>> 81ec5ddf5acf3de78d77c01ed95631e44d37fe6e

# 如何：啟用文件追蹤和撤銷

本主題涵蓋實作內容文件追蹤的基本指導，以及用於中繼資料更新和建立應用程式 **[追蹤使用情況] 按鈕**的範例程式碼。

## 實作文件追蹤的步驟

步驟 1 和 2 讓文件可供追蹤。 步驟 3 讓您的應用程式使用者能夠連線到文件追蹤網站，以便追蹤及撤銷您受保護的文件。

1. 新增文件追蹤中繼資料
2. 使用 RMS 服務註冊文件
3. 將 [追蹤使用情況] 按鈕加入您的應用程式中

這些步驟的實作詳細資料如下。

## 1.新增文件追蹤中繼資料

文件追蹤是 Rights Management 系統的功能。 藉由在文件保護程序期間新增特定中繼資料，可以向追蹤服務入口網站註冊文件，網站進而提供數個追蹤選項。

使用這些 API 以文件追蹤中繼資料來新增/更新內容授權。


在操作方面，文件追蹤只需要**內容名稱**和**通知類型**屬性。


- [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
- [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

  我們希望您設定所有的中繼資料屬性。 以下就是這些屬性，依類型排列。

  如需詳細資訊，請參閱[授權中繼資料屬性類型](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)。

  - **IPC_MD_CONTENT_PATH**

    使用這個屬性來識別追蹤的文件。 在不可能提供完整路徑的情況下，只要提供檔案名稱。

  - **IPC_MD_CONTENT_NAME**

    使用這個屬性來識別追蹤的文件名稱。

  - **IPC_MD_NOTIFICATION_TYPE**

    使用這個屬性來指定何時要傳送通知。 如需詳細資訊，請參閱＜通知類型＞。

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    使用這個屬性來指定通知類型。 如需詳細資訊，請參閱＜通知喜好設定＞。

  - **IPC_MD_DATE_MODIFIED**

    建議您在每次使用者按一下 [儲存] 時設定此日期。

  - **IPC_MD_DATE_CREATED**

    使用這個屬性來設定檔案的原始日期

- [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

使用這些 API 中適當的一個將中繼資料新增至您的檔案或資料流。

- [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
- [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最後，使用此 API 在追蹤系統中註冊您的追蹤文件。

- [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)


## 2.使用 RMS 服務註冊文件

以下的程式碼片段顯示設定文件追蹤中繼資料和呼叫註冊追蹤系統的範例。

      C++
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

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

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

## 將 **[追蹤使用情況]** 按鈕加入您的應用程式中

將 **[追蹤使用情況]** UI 項目加入您的應用程式中，就像使用下列其中一個 URL 格式一樣簡單︰

- 使用內容識別碼
  - 使用 [IpcGetLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetlicenseproperty) 取得內容識別碼；若授權已序列化則使用 [IpcGetSerializedLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetserializedlicenseproperty)，並使用授權屬性 **IPC_LI_CONTENT_ID**。 如需詳細資訊，請參閱[授權屬性類型](/rights-management/sdk/2.1/api/win/constants#msipc_license_property_types)。
  - **ContentId** 和 **Issuer** 中繼資料，請使用下列格式︰ `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    範例 - `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- 如果您沒有該中繼資料的存取權 (也就是您正在檢查未受保護的文件版本)，可在下列格式使用 **Content_Name**︰ `https://track.azurerms.com/#/?q={ContentName}`

  範例 - https://track.azurerms.com/#/?q=Secret!.txt

用戶端只需以適當的 URL 開啟瀏覽器。 RMS 文件追蹤入口網站會處理驗證及任何必要的重新導向。

## 相關主題

* [授權中繼資料屬性類型](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)
* [通知的喜好設定](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [通知類型](/rights-management/sdk/2.1/api/win/constants#msipc_notification_type)
* [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

 


<!--HONumber=Jun16_HO2-->


