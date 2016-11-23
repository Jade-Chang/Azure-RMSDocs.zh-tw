---
title: "作法：使用內建權限 | Azure RMS"
description: "概述 RMS SDK 4.2 提供的內建權限，和應用程式在接受這些限制時應強制執行的使用限制。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experimental: true
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: dc40edaf8856ece3c40d1bfc4674a357f2c055ea
ms.openlocfilehash: 3d897f191368b7af6fd339603e183583fa9b4a27


---

# <a name="how-to-use-builtin-rights"></a>作法：使用內建權限

本主題概述 Microsoft Rights Management SDK 4.2 提供的內建權限，和應用程式在接受這些限制時應強制執行的使用限制。 以下顯示內建的權限；常見權限、可編輯的文件的權限和電子郵件權限，後面接著描述及其值 (依作業系統分類)。

**注意** - 針對 Linux SDK，請參閱 *rights.h* 原始程式檔以取得詳細資料。

## <a name="common-rights"></a>一般權限

**全部** - 所有一般權限的集合。
- Android：[CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 與 OS X：[MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx) - 使用者擁有者和檢視以實作**全部**
- Windows 市集和 Windows Phone：[CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux：[CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**擁有者** - 擁有者權限授與受保護內容的完全控制權。
- Android：[<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 和 OS X：[MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows 市集和 Windows Phone：[CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux：[CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**檢視** - 檢視受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者開啟並檢視受保護的內容；不過，需要其他權限才能修改、擷取、轉寄或儲存內容。

- Android：[CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS 和 OS X：[MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Windows 市集和 Windows Phone：[CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux：[CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>可編輯的文件權限
**全部** - 包含所有可編輯文件權限的集合。
- Android：[EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux：[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**註解** - 註解文件的權限。
- Android：[EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux：[EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**編輯** - 編輯受保護內容，並以相同的受保護格式儲存該內容的權限。 一般而言，授與此權限時，應用程式可讓使用者變更受保護的內容，然後將它儲存到相同的檔案。
- Android：[EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux：[EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**匯出** - 從受保護的格式擷取內容，並將它放在不同的 AD RMS 受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者將受保護的內容儲存到其他 AD RMS 受保護格式；例如，如果應用程式實作 [另存新檔] 功能。

- Android：[EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux：[EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**擷取** - 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者從受保護的內容中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓使用者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與電子郵件的擷取權限具有相同值。

- Android：[EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux：[EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**列印** - 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者列印受保護的內容。 此權限與電子郵件的列印權限具有相同值。

- Android：[EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS 和 OS X：[MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux：[EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>電子郵件權限

**全部** - 包含所有電子郵件權限的集合。
- Android：[EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux：[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**擷取** - 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者從受保護的郵件中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓收件者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與可編輯文件的擷取權限具有相同值。

- Android：[EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux：[EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**轉寄** - 轉寄受保護郵件的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者轉寄受保護的郵件。
- Android：[<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux：[EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**列印** - 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者列印受保護的郵件。 此權限與可編輯文件的列印權限具有相同值。

- Android：[EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux：[EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回覆** - 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護的郵件及加入原始郵件的副本。

- Android：[EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux：[EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** - 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護郵件的所有收件者，及加入原始郵件的副本。

- Android：[EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS 和 OS X：[MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Windows 市集和 Windows Phone：[EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux：[EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 



<!--HONumber=Oct16_HO3-->


