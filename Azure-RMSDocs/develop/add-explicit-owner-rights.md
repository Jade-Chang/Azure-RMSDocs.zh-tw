---
title: "如何新增明確的擁有者權限 | Azure RMS"
description: Your application should explicitly add "Owner" rights when creating a license from scratch.
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 22016f824263916f5f265d818c51975d42c35799


---

# 如何：新增明確的擁有者權限

從頭開始建立授權時，您的應用程式應該明確加入「擁有者」權限 ([**IpcCreateLicenseFromScratch**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch))。

## 必要條件

當您的應用程式正在使用 [**IpcCreateLicenseFromScratch**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 建立授權控制代碼時，它也必須明確授與擁有者完整權限 (權限)。

>[!NOTE] 
> 使用內含 **IPC\_LI\_OWNER** 屬性的 [**IpcSetLicenseProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) 將使用者設為「擁有者」，並不會授與擁有者完整權限。

下列範例程式碼僅代表涉及建立特定權限並將其加入指定授權中的步驟。

## 指示
 
## 步驟 1：範例案例

此範例中，會在以 [**IpcCreateLicenseFromScratch**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch) 建立的授權中加入需要的權限。 此範例顯示透過權限清單建立權限並指派給授權。

下列兩個權限會新增給這些使用者︰

-   指派給 joe@contoso.com 的*讀取*權限
-   指派給 mary\_kay@contoso.com 的*完整*權限

        // Create User Rights structure
        IPC_USER_RIGHTS ownerRightForOwner = {0};

        // Create rights
        LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure
        ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
        ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
        ownerRightForOwner.rgwszRights = rgwszOwnerRights;
        ownerRightForOwner.cRights = 1;

        // Create User Rights structure for Joe with Read permissions
        IPC_USER_RIGHTS joeReadRight = {0};
        LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

        // Assign values to members of Rights structure for Joe
        joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
        joeReadRight.User.wszID = "joe@contoso.com";
        joeReadRight.rgwszRights = rgwszReadRights;
        joeReadRight.cRights = 1;

        // Create User Rights structure for Mary Kay with Full permissions
        IPC_USER_RIGHTS mary_kayFullRight = {0};
        LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

        // Assign values to members of Rights structure for Mary Kay
        mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
        mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
        mary_kayFullRight.rgwszRights = rgwszFullRights;
        mary_kayFullRight.cRights = 1;

        // Create User Rights List and assign the above rights
        size_t uNoOfUserRights = 3;
        PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
        pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
        (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

        if(pUserRightsList == NULL)
        {
          // Handle error
        }

        // Assign values to members of Rights List structure for Joe and Mary Kay
        (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
        (*pUserRightsList).cUserRights = uNoOfUserRights;
        (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
        (*pUserRightsList).rgUserRights[1] = joeReadRight;
        (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

        // Set the Rights List property on the license via its handle
        // hLicense is a license handle created with IpcCreateLicenseFromScratch
        hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

        if(FAILED(hr))
        {
          // Handle the error
        }



## 相關主題

* [開發人員注意事項](developer-notes.md)
* [**IpcCreateLicenseFromScratch**](/information-protection/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcSetLicenseProperty**](/information-protection/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
 

 



<!--HONumber=Oct16_HO1-->


