---
title: "如何使用文件追蹤 | Azure RMS"
description: "文件追蹤功能需要稍微了解如何管理相關聯的中繼資料並註冊服務。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 04234755fabb10794f5be7c4fc658573bebf6e70
ms.openlocfilehash: 616d5dd088665abf6e7d435978b021b10c5ac3f5


---

# 作法：使用文件追蹤

使用文件追蹤功能需要稍微了解如何管理相關聯的中繼資料並註冊服務。

## 管理文件追蹤中繼資料

支援文件追蹤的每個作業系統都有類似的實作。 這些實作包括代表中繼資料的一組屬性，新增至使用者原則建立方法的新參數，以及登錄要利用文件追蹤服務來追蹤之原則的方法。

在操作方面，文件追蹤只需要**內容名稱**和**通知類型**屬性。

您用來設定特定內容之文件追蹤的步驟順序如下︰

-   建立**授權中繼資料**物件，然後設定**內容名稱**和**通知類型**。 這些是唯一的必要的屬性。
   - Android - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
   -  iOS - [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

選擇原則類型；範本或臨機操作︰
- 針對以文件追蹤為基礎的範本，請建立傳遞授權中繼資料做為參數的**使用者原則**。
  - Android - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- 針對以臨機操作為基礎的文件追蹤，請在**原則描述元**物件上設定**授權中繼資料**屬性。
  - Android - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS - [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx)。

    **注意**  只有在針對指定使用者原則設定文件追蹤的過程期間，才能直接存取授權中繼資料物件。 建立使用者原則物件之後，無法存取相關聯的授權中繼資料，也就是變更授權中繼資料的值沒有任何作用。

     

-   最後，呼叫平台註冊方法以追蹤文件。
  - Android - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) 或 [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)

 

 



<!--HONumber=Oct16_HO3-->


