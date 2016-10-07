---
title: "作法：使用內建權限 | Azure RMS"
description: "概述 RMS SDK 4.2 提供的內建權限，和應用程式在接受這些限制時應強制執行的使用限制。"
keywords: 
author: bruceperlerms
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
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: d8fb04fd80e9a84bd7784e48b77e3aa8b045bf2d


---

# 作法：使用內建權限

本主題概述 Microsoft Rights Management SDK 4.2 提供的內建權限，和應用程式在接受這些限制時應強制執行的使用限制。 以下顯示內建的權限；常見權限、可編輯的文件的權限和電子郵件權限，後面接著描述及其值 (依作業系統分類)。

**注意** - 針對 Linux SDK，請參閱 *rights.h* 原始程式檔以取得詳細資料。

## 一般權限 ##

**全部** - 所有一般權限的集合。
- Android：[CommonRights.All](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS 和 OS X：[MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 市集和 Windows Phone：[CommonRights.All</strong>](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux：[CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**擁有者** - 擁有者權限授與受保護內容的完全控制權。
- Android：[<strong>CommonRights.Owner](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS 和 OS X：[MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 市集和 Windows Phone：[CommonRights.Owner](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux：[CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**檢視** - 檢視受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者開啟並檢視受保護的內容；不過，需要其他權限才能修改、擷取、轉寄或儲存內容。

- Android：[CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS 和 OS X：[MSCommonRights view](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Windows 市集和 Windows Phone：[CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux：[CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## 可編輯的文件權限 ##
**全部** - 包含所有可編輯文件權限的集合。
- Android：[EditableDocumentRights.All](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS 和 OS X：[MSEditableDocumentRights all](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.All](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux：[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**註解** - 註解文件的權限。
- Android：[EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS 和 OS X：[MSEditableDocumentRights comment](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux：[EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**編輯** - 編輯受保護內容，並以相同的受保護格式儲存該內容的權限。 一般而言，授與此權限時，應用程式可讓使用者變更受保護的內容，然後將它儲存到相同的檔案。
- Android：[EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS 和 OS X：[MSEditableDocumentRights edit](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux：[EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**匯出** - 從受保護的格式擷取內容，並將它放在不同的 AD RMS 受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者將受保護的內容儲存到其他 AD RMS 受保護格式；例如，如果應用程式實作 [另存新檔] 功能。

- Android：[EditableDocumentRights.Export](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS 和 OS X：[MSEditableDocumentRights exportable](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Export](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux：[EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**擷取** - 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者從受保護的內容中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓使用者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與電子郵件的擷取權限具有相同值。

- Android：[EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS 和 OS X：[MSEditableDocumentRights extract](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux：[EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**列印** - 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者列印受保護的內容。 此權限與電子郵件的列印權限具有相同值。

- Android：[EditableDocumentRights.Print](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS 和 OS X：[MSEditableDocumentRights print](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Windows 市集和 Windows Phone：[EditableDocumentRights.Print](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux：[EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## 電子郵件權限 ##

**全部** - 包含所有電子郵件權限的集合。
- Android：[EmailRights.All](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS 和 OS X：[MSEmailRights all](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.All](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux：[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**擷取** - 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者從受保護的郵件中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓收件者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與可編輯文件的擷取權限具有相同值。

- Android：[EmailRights.Extract](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS 和 OS X：[MSEmailRights extract](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.Extract</strong>](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux：[EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**轉寄** - 轉寄受保護郵件的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者轉寄受保護的郵件。
- Android：[<strong>EmailRights.Forward</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS 和 OS X：[MSEmailRights forward](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.Forward](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux：[EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**列印** - 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者列印受保護的郵件。 此權限與可編輯文件的列印權限具有相同值。

- Android：[EmailRights.Print](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS 和 OS X：[MSEmailRights print](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.Print](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux：[EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**回覆** - 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護的郵件及加入原始郵件的副本。

- Android：[EmailRights.Reply](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS 和 OS X：[MSEmailRights reply](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.Reply](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux：[EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll** - 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護郵件的所有收件者，及加入原始郵件的副本。

- Android：[EmailRights.ReplyAll</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS 和 OS X：[MSEmailRights replyAll](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Windows 市集和 Windows Phone：[EmailRights.ReplyAll](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux：[EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 



<!--HONumber=Oct16_HO1-->


