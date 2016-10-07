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
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: a8a513260dde6047c95c52c48217b7b4d8466cbc


---

# 作法：使用內建權限

本主題概述 Microsoft Rights Management SDK 4.2 提供的內建權限，和應用程式在接受這些限制時應強制執行的使用限制。 下表顯示內建的權限；一般權限、可編輯文件權限和電子郵件權限，後面接著描述及其值 (依作業系統分類)。

**注意** - 針對 Linux SDK，請參閱 *rights.h* 原始程式檔以取得詳細資料。

## 一般權限 ##

| Right | 說明 | Android | iOS 和 OSX | Windows 市集和 Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **全部：** | 所有一般權限的集合。 | [CommonRights.All](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL) | [MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)| [CommonRights.All</strong>](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)| [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Owner**| 授與完全控制受保護內容的權限 |  [CommonRights.Owner](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner) |[MSCommonRights owner](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_) |[CommonRights.Owner](/information-protection/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner) |  [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **檢視** | 檢視受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者開啟並檢視受保護的內容；不過，需要其他權限才能修改、擷取、轉寄或儲存內容。 |  [CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [MSCommonRights view](/information-protection/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)|[CommonRights.View](/information-protection/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html) |


## 可編輯的文件權限 ##

| Right | 說明 | Android | iOS 和 OSX | Windows 市集和 Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **全部：** | 包含所有可編輯文件權限的集合。| [EditableDocumentRights.All](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL) | [MSEditableDocumentRights all](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.All](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all) |[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **註解** | 註解文件的權限。 | [EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)|[MSEditableDocumentRights comment](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Comment](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)| [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **編輯** | 編輯受保護內容，並以相同的受保護格式儲存該內容的權限。 一般而言，授與此權限時，應用程式可讓使用者變更受保護的內容，然後將它儲存到相同的檔案。 | [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit) | [MSEditableDocumentRights edit](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Edit](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit) | [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html) |
| **匯出** | 從受保護的格式擷取內容，並將它放在不同的 AD RMS 受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者將受保護的內容儲存到其他 AD RMS 受保護格式；例如，如果應用程式實作 [另存新檔] 功能。 | [EditableDocumentRights.Export](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export) | [MSEditableDocumentRights exportable](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Export](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export) | [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **擷取** | 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓使用者從受保護的內容中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓使用者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與電子郵件的擷取權限具有相同值。 |  [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract) |[MSEditableDocumentRights extract](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Extract](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract) |  [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **列印** | 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓使用者列印受保護的內容。 此權限與電子郵件的列印權限具有相同值。 | [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print) |  [MSEditableDocumentRights print](/information-protection/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)| [EditableDocumentRights.Print](/information-protection/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print) | [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
 

## 電子郵件權限 ##

| Right | 說明 | Android | iOS 和 OSX | Windows 市集和 Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **全部：** |包含所有電子郵件權限的集合。 |  [EmailRights.All](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL) | [MSEmailRights all](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.All](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)|[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **擷取** | 從受保護的格式擷取內容，並將它放在不受保護格式的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者從受保護的郵件中複製和貼上資訊。 如果應用程式實作 [另存新檔]<em></em> 功能，應用程式可能也會讓收件者將受保護的內容儲存至未受保護的格式及其他受保護的格式。 此權限與可編輯文件的擷取權限具有相同值。 | [EmailRights.Extract](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract) | [MSEmailRights extract](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Extract</strong>](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract) | [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**轉寄**| 轉寄受保護訊息的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者轉寄受保護的郵件。| [<strong>EmailRights.Forward</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward) | [MSEmailRights forward](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Forward](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward) | [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**列印** | 列印受保護內容的權限。 一般而言，授與此權限時，應用程式可讓電子郵件收件者列印受保護的郵件。 此權限與可編輯文件的列印權限具有相同值。 | [EmailRights.Print](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print) |[MSEmailRights print](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Print](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print) | [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **回覆** | 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護的訊息，並包含原始訊息的副本。 | [EmailRights.Reply](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply) | [MSEmailRights reply](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Reply](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply) | [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **全部回覆** | 一般而言，授與此權限時，應用程式可讓電子郵件收件者回覆受保護訊息的所有收件者，並包含原始訊息的副本。 | [EmailRights.ReplyAll</strong>](/information-protection/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll) | [MSEmailRights replyAll](/information-protection/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.ReplyAll](/information-protection/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall) | [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|



<!--HONumber=Oct16_HO1-->


