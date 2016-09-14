---
title: "系統管理員如何控制個人版 RMS 建立的帳戶 | Azure RMS"
description: "如果您不想將組織的個人版 RMS 訂閱轉換成付費訂閱，如何在 Azure Active Directory 中控制使用者帳戶的方式。"
author: cabailey
manager: mbaldwin
ms.date: 09/01/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79d098e47cdfe608bc62ed385a5c8236fb7c6d3c
ms.openlocfilehash: 6383c1d583eb45973750305e709d8f5d792892b5


---



# 系統管理員如何控制個人版 RMS 建立的帳戶

>*適用於：Azure Rights Management*


如果您不想將組織的個人版 RMS 訂閱轉換成付費訂閱，您仍可使用下列方法，控制您組織所建立之 Azure 目錄中的使用者帳戶：

-   為 Azure Active Directory 和 Active Directory 網域服務基礎結構實作目錄整合方案。 您可同步帳戶和密碼，讓該使用者不必建立新帳戶來使用 Rights Management，且您的內部部署密碼原則將套用至新 Azure 使用者帳戶。 您也可同步密碼，讓使用者不必記憶不同的密碼來使用 Rights Management。

-   您可防止使用者註冊並搭配使用 Azure Rights Management 與個人版 RMS 訂用帳戶。 這麼做在大多數情況下有一些好處，因為使用者將共用沒有保護的檔案 (可能讓您的公司處於風險中)，或將使用其他檔案保護機制，IT 部門將無法運用這種機制存取資料。 不過，若要防止使用者註冊並使用個人版 RMS，請在 Azure 中取得組織之目錄的擁有權後執行下列其中一個動作：

    -   防止所有使用者註冊自助訂用帳戶，其中包括個人版 RMS。  您目前無法設定此服務。此設定會套用至所有使用自助程序的 Azure 訂用帳戶。 若要執行此動作，請將 **AllowAdHocSubscriptions** 參數設為 false，再搭配使用 Azure Active Directory 之 Windows PowerShell 模組的 [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) Cmdlet。 例如：**Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   防止使用者在 Azure 建立新帳戶，代表只有已經在 Azure 擁有帳戶的使用者才能註冊包含個人版 RMS 的自助訂用帳戶。  若要執行此動作，請將 **AllowEmailVerifiedUsers** 參數設為 false，再搭配使用 Azure Active Directory 之 Windows PowerShell 模組的 [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) Cmdlet。 例如：**Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   同步您的 Active Directory 網域服務基礎結構與 Azure Active Directory。 此動作可防止使用者在註冊個人版 RMS 等自助訂用帳戶時建立新帳戶，且您可刪除或停用先前在 Azure 目錄中建立的帳戶。

若要控制 Azure 目錄中的使用者帳戶，或防止使用者註冊個人版 RMS，您必須擁有 Azure 訂閱並擁有目錄。 如果您還沒有 Azure 訂用帳戶，您可以免費取得一個。 若在自助程序期間為您自動建立目錄，請取得用來建立網域的網域擁有權。 如果您已擁有在 Azure 中的目錄，但使用者指定您在組織中使用的新網域，請將該網域合併到現有的目錄中。 如需詳細資訊，請參閱 [何謂 Azure 的自助註冊？](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)中的指示


## 後續步驟

如果使用者 (而不是系統管理員) 可以在 Azure Active Directory 中，針對個人版 RMS 建立自己的帳戶，要如何瞭解已這麼做？  請參閱[如何找出您的使用者是否已註冊個人版 RMS](rms-for-individuals-identify-sign-up.md)。



<!--HONumber=Sep16_HO1-->


