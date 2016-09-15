---
title: "Rights Management 共用應用程式&colon; 版本發行記錄 | Azure RMS"
description: "查看適用於 Windows 的 Rights Management 共用應用程式版本有哪些新功能或變更。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6751bd90-959f-4eba-91ed-6588ac983762
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 035c9eb6cb630cafd5bd7fc7e2371340043ddc5e
ms.openlocfilehash: 361fde97756c24fa46df6eda16d7506b4b8aaa3a


---

# Rights Management 共用應用程式：版本發行記錄

>*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

Rights Management 小組會定期更新 Rights Management 共用應用程式以進行修正和新增功能。 使用下列資訊查看版本的新功能或變更。 最新的版本會先列出。

不會列出 2015 年 1 月 1 日之前的版本。

> [!NOTE]
> 如果您有任何與 RMS 共用應用程式相關的意見反應或疑問，請將電子郵件訊息傳送至 [AskIPTeam](mailto:AskIPTeam@microsoft.com?subject=RMS%20sharing%20app:%20Feedback%20or%20question)。

## 1.0.2217.0 版

**發行日期**：2016 年 7 月 13 日

**修正**：

- 使用同盟和多因素驗證的組織使用者，在保護內容時不再收到錯誤 0x800704DC。



## 1.0.2191.0 版
**發行日期**：2016 年 6 月 16 日

**修正**：

- 文件追蹤網站現在會顯示每份追蹤文件的正確檢視數量。

- 現在，所有地區設定的範本皆會顯示為可供使用者使用。

- 針對 PowerPoint 檔案使用 [共用保護] 之後，現可正確儲存本機版本檔案的變更。

- 錯誤訊息的少量輕微錯誤與改進。


## 版本 1.0.2004.0
**發行日期**：2015 年 12 月 11 日

**修正**：

-   只有檔案擁有者和具有**共同擁有者**權限層級的人員可以取消檔案的保護。 以前，擁有者和具有**共同作者**與**共同擁有者**權限層級的人員可以取消檔案保護。

-   對 **.tif** 檔案的原生保護 (以前只有 .tiff 檔案)，以產生受 RMS 保護的唯讀 **.ptif** 檔案。

-   改進錯誤訊息 (正確性和清晰性)。

-   內容加密和解密的效能改進。

**新功能**：

-   支援非系統管理員的安裝，讓標準使用者可以安裝 RMS 共用應用程式。

    執行 Office 2010 的標準使用者會有一些限制。 如需詳細資訊，請參閱[下載並安裝 Rights Management 共用應用程式](install-sharing-app.md)使用者指示中的[如果不是本機系統管理員，而且使用 Office 2010](install-sharing-app.md#if-you-are-not-a-local-administrator-and-use-office-2010)一節。

## 1.0.1908.0 版
**發行日期**：2015 年 9 月 16 日

**修正**：

-   支援 Azure RMS 的多因素驗證 (MFA)，該驗證也會移除使用新式驗證之應用程式對 Microsoft 登入小幫手的相依性。

    如需詳細資訊，請參閱 [Azure Rights Management 的需求](../get-started/requirements-azure-rms.md)主題中的[多因素驗證 (MFA) 與 Azure RMS](../get-started/requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-rms) 一節。

## 1.0.1784.0 版
**發行日期**：2015 年 7 月 30 日

**修正**：

-   權限原則範本的預設重新整理間隔會從 7 天減少到 1 天。

-   少數回復和次要的 bug。

## 1.0.1770.0 版
**發行日期**：2015 年 4 月 25 日

**修正**：

-   現在，只有擁有者和共同擁有者可以移除保護。 共同作者不能移除保護。

-   網路共用上的檔案現在可以受到保護。

**新功能**：

-   支援文件追蹤和撤銷。 如需詳細資訊，請參閱[當您使用 RMS 共用應用程式時，追蹤及撤銷文件](sharing-app-track-revoke.md)。

-   當您選擇 [共用保護] 時的範本支援：

    -   您現在可以選取範本。

    -   您會看到包含範本和自訂權限的清單方塊，而不是滑動軸。

    -   您不會再看見 **允許在所有裝置上使用** 和 **強制使用限制**的選項。 根據檔案類型，會改為自動選取 [一般保護]  。

    如需詳細資訊，請參閱 [Rights Management 共用應用程式的對話方塊選項](sharing-app-dialog-box.md)。

## 1.0.1667.0 版
**發行日期**：2015 年 1 月 19 日

**修正**：

-   RMS 共用應用程式 PPDF 檢視器中的中文語言字型支援。

-   改進的錯誤處理和訊息。

-   較新版本的應用程式可供下載時，可修正自動更新通知的相關問題。

**新功能**：

-   **支援組織內有多個電子郵件網域**：如果您使用 AD RMS 且組織中的使用者有多個電子郵件網域，這項更新可讓您的使用者取用受組織中使用者在其他網域中所保護的內容。 如需詳細資訊，請參閱《[Rights Management 共用應用程式系統管理員指南](sharing-app-admin-guide.md)》的[僅限 AD RMS：支援組織內有多個電子郵件網域](sharing-app-admin-guide.md#ad-rms-only-support-for-multiple-email-domains-within-your-organization)一節。




<!--HONumber=Aug16_HO4-->


