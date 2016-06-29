---
# required metadata

title: 啟用電子郵件通知 |Azure RMS
description: 可存取受保護的內容時，用來通知其擁有者的電子郵件。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 如何：啟用電子郵件通知

可存取受保護的內容時，用來通知其擁有者的電子郵件。

若要設定針對指定授權的電子郵件通知，請使用 [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) 搭配屬性型別參數 *dwPropID* 作為 [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA) 以及應用程式資料欄位，格式如 [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)。

    C++

    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
        

下表包含 RMS 電子郵件通知的應用程式資料欄位、屬性名稱/值組。


|屬性名稱 | 資料類型 | 範例值 | 附註 |
|--------------|-----------|---------------|-------|
|MS.Content.Name|字串|“FinancialReport.docx”|這是與受保護內容相關聯的識別碼。<br><br> 受保護檔案的這個值應該是檔案的名稱，不含任何路徑資訊。<br><br> 其他類型內容 (例如電子郵件訊息) 的這個值則可能是電子郵件的主旨或可能是空的。|
|MS.Notify.Enabled|字串|“true” &#124; “false”|如果此值設定為"true"，當有人嘗試使用它來取得使用者授權時，系統會傳送通知電子郵件給發行授權的擁有者。|
|MS.Notify.Culture|字串|“en-US”| **來源：** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>這個值用來判斷通知電子郵件的當地語系化的語言，以及電子郵件訊息中應使用的日期/時間和數字格式。<br><br>它應該會根據建立發行授權之電腦上的使用者設定而設定，或根據發行授權擁有者的慣用文化而設定。|
|MS.Notify.TZID|字串|“Pacific Standard Time”|**來源︰** TimeZoneInfo.Local.Id - Windows time zone ID.<br><br>這個值是 Microsoft Windows 作業系統的時區識別碼，描述特定時區及其特性。|
|MS.Notify.TZO|字串|“-480”|這是發行授權擁有者的時區位移，為與 UTC 的時間差 (分鐘)。<br><br>若有提供有效的 TZID 值，統將使用其指定的時區位移系，忽略這個值。<br><br>非 Windows 發行平台很可能會使用此值，因其無法存取 Windows 作業系統的時區識別碼值清單。<br><br>如未提供 TZID 值，會用這個值來計算通知訊息的時間位移，TZSN 則用於 (不管時區值為何) 表示時區的名稱。 這會導致固定的時區，不會針對日光節約時間更新。<br><br>例如：<br><br>如果 TXID 空白，且 TZ0 設為 -420、 TZSN 設為 "Pacific Daylight Time"，通知電子郵件中的所有值會調整為「太平洋日光節約時間」並如此顯示，即使目前不是過日光節約時間。<br><br>另一方面，如果同時提供 TZID 以及 TZSN 和 TZDN，則會根據日期和時間應該以日光節約模式或標準模式顯示，來調整並顯示電子郵件通知中的時間。|
|MS.Notify.TZSN|字串|“Pacific Standard Time”|**來源：** TimeZoneInfo.Local.StandardName - Standard Time Zone name.<br><br>這應該是時區的標準時區名稱的當地語系化名稱。|
|MS.Notify.TZDN|字串|“Pacific Daylight Time”|**來源：** TimeZoneInfo.Local.DaylightName - Daylight Time Zone name.<br><br>這應該是時區的日光節約名稱的當地語系化名稱。 如果時區不支援日光節約時間，它可能和標準名稱相同。|

## 相關主題

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 


<!--HONumber=Jun16_HO2-->


