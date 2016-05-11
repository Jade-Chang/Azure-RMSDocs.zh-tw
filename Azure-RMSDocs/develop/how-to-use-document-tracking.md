---
# required metadata

title: 作法：使用文件追蹤 | Azure RMS
description: 文件追蹤功能需要稍微了解如何管理相關聯的中繼資料並註冊服務。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d193afec-6dc5-477d-8e67-f820a97480ff

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
# 作法：使用文件追蹤

使用文件追蹤功能需要稍微了解如何管理相關聯的中繼資料並註冊服務。

## 管理文件追蹤中繼資料

支援文件追蹤的每個作業系統都有類似的實作。 這些實作包括代表中繼資料的一組屬性，新增至使用者原則建立方法的新參數，以及登錄要利用文件追蹤服務來追蹤之原則的方法。

在操作方面，文件追蹤只需要內容名稱和通知類型屬性。

您用來設定特定內容之文件追蹤的步驟順序如下︰

-   建立授權中繼資料物件。

    如需詳細資訊，請參閱 [LicenseMetadata](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) 或 [MSLicenseMetadata](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc)。

-   設定內容名稱和通知類型。 這些是唯一的必要的屬性。

    如需詳細資訊，請參閱平台適當授權中繼資料類別的屬性存取方法，[LicenseMetadata](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) 或 [MSLicenseMetadata](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc)。

-   根據原則類型；範本或臨機操作︰

    -   針對以文件追蹤為基礎的範本，請建立傳遞授權中繼資料做為參數的使用者原則。

        如需詳細資訊，請參閱 [UserPolicy.create](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) 和 [MSUserPolicy.userPolicyWithTemplateDescriptor](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc)。

    -   針對以臨機操作為基礎的文件追蹤，請在原則描述元物件上設定授權中繼資料屬性。

        如需詳細資訊，請參閱 [PolicyDescriptor.getLicenseMetadata](https://stage.docs.microsoft.com/en-us/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java)、[PolicyDescriptor.setLicenseMetadata](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) 和 [MSPolicyDescriptor.licenseMetadata](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc)。

    注意  只有在針對指定使用者原則設定文件追蹤的過程期間，才能直接存取授權中繼資料物件。 建立使用者原則物件之後，無法存取相關聯的授權中繼資料，也就是變更授權中繼資料的值沒有任何作用。

     

-   文件追蹤的呼叫平台註冊方法。

    請參閱 [MSUserPolicy.registerForDocTracking](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) 或 [UserPolicy.registerForDocTracking](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc)。

 

 





<!--HONumber=Apr16_HO3-->


