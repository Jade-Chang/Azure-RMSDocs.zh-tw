---
title: "如何找出使用者是否已註冊個人版 RMS | Azure Information Protection"
description: "身為系統管理員，您如何得知使用者是否已申請個人版 RMS？ 您可以使用本文中所述的任何單一方法或是多種方法的組合。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: b9979d48af7146f8021de840248f71cb1399b777


---


# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>如何找出您的使用者是否已註冊個人版 RMS

>*適用於：Azure 資訊保護*

身為系統管理員，您如何得知使用者是否已申請個人版 RMS？ 您可使用下列任一方法或一組方法：

-   詢問使用者如何保護高度機密檔案，特別是在與組織外部的其他人共同作業時。

-   當您在組織中具有 Azure 訂用帳戶時，請使用 [Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) 指令程式，並查看 **RIGHTSMANAGEMENT_ADHOC** 是否做為其中一個訂用帳戶傳回。 如果是，這會是授與組織的個人版 RMS 訂閱，提供使用者有效單位的集區以方便使用自助式註冊程序。

-   使用系統管理方案 (例如 System Center Configuration Manager) 來清查已安裝的軟體和使用中的軟體。 Rights Management 共用應用程式會藉由使用 **ipviewer.exe** 程式來執行，您可以免費 [下載及安裝應用程式](http://go.microsoft.com/fwlink/?LinkId=303970) ，以便識別後續將此應用程式用於軟體清查時的其他相關特性。

-   檢查 Rights Management 共用應用程式建立的副檔名。 .pfile 和 .ppdf 副檔名是最明顯的例子，但當這種檔案由 Rights Management 服務原生保護時，有其他檔案可變更其副檔名。 如需詳細資訊，請參閱 [Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)的[支援的檔案類型和副檔名](http://technet.microsoft.com/library/dn339003.aspx)一節。




<!--HONumber=Nov16_HO2-->


