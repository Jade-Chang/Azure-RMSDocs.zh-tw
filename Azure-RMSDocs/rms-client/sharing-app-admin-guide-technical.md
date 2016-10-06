---
title: "Rights Management 共用應用程式技術概觀 | Azure Information Protection"
description: "適用於企業網路中負責部署適用於 Windows 的 RMS 共用應用程式之系統管理員的技術詳細資料。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: aac3c6c7b5167d729d9ac89d9ae71c50dd1b6a10
ms.openlocfilehash: 3b4cd04732e38da31bf31d899993c912694e3ee8


---


# Microsoft Rights Management 共用應用程式技術概觀與保護詳細資料

>*適用於︰Active Directory Rights Management Services、Azure Information Protection、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*


Microsoft Rights Management 共用應用程式是可選擇性下載的應用程式，適用於 Microsoft Windows 和其他提供下列功能的平台：

-   保護單一檔案、大量保護多個檔案、以及保護選取之資料夾內的所有檔案。

-   完整支援對所有類型檔案的保護，以及對常用文字和影像檔案類型的內建檢視器。

-   對不支援 RMS 保護的檔案提供一般保護。

-   與使用 Office 資訊版權管理 (IRM) 保護的檔案之間有完全互通性。

-   與使用檔案分類基礎結構 (FCI) 和支援的 PDF 撰寫工具保護的 PDF 檔案之間有完全互通性。

Microsoft Rights Management 共用應用程式使用 [AD RMS Client 2.1 執行階段](http://www.microsoft.com/download/details.aspx?id=38396)。 使用 AD RMS 2.1 的功能，Microsoft Rights Management 共用應用程式的功能可提供一般使用者簡單的保護和使用體驗。

在 2013 年 10 月版的 RMS 中，您可以使用 Office 2010 以原生方式保護文件，並將其傳送給其他公司的人員，再由這些人員使用 Azure Information Protection 的 Azure Rights Management Service 加以取用。 此外，在此版本中，如果您使用「密碼編譯模式 2」的 AD RMS，則可以使用個人版 RMS 向使用 Azure Rights Management Service 的其他公司人員取用內容。 如需密碼編譯模式 2 的詳細資訊，請參閱＜ [AD RMS 密碼編譯模式](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx)＞。

如需部署資訊，請參閱[自動部署 Microsoft Rights Management 共用應用程式](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)

## 保護的層級 – 原生和一般
Microsoft Rights Management 共用應用程式支援兩個不同的層級的保護，如下表所述。

|保護類型|原生|泛型|
|----------------------|----------|-----------|
|說明|針對文字、影像、Microsoft Office (Word、Excel、PowerPoint) 檔案、.pdf 檔案及其他支援 Rights Management Service 的應用程式檔案類型，原生保護提供了包含加密和強制執行權限的強力層級保護。|針對所有其他應用程式和檔案類型，一般保護提供包含檔案封裝 (使用 .pfile 檔案類型) 和驗證 (確認使用者是否獲得開啟檔案授權) 的保護層級。|
|保護|完整加密檔案並以下列方式強制執行保護：<br /><br />受保護的內容轉譯之前，透過電子郵件收到檔案或是透過檔案或共用權限存取檔案的人，必須成功通過驗證。<br /><br />此外，當檔案受到保護時，若要在 IP 檢視器中 (適用於受保護的文字和影像檔) 或相關聯的應用程式中 (適用於所有其他支援的檔案類型) 轉譯內容時，將完全強制執行內容擁有者所設定的使用權限與原則。|以下列方式強制執行檔案保護：<br /><br />受保護的內容轉譯之前，獲得開啟檔案授權和獲得檔案存取權的人，必須成功通過驗證。 如果授權失敗，檔案不會開啟。<br /><br />系統會顯示內容擁有者所設定的使用權限與原則，以通知授權使用者其預定使用原則。<br /><br />不過，稽核授權的使用者開啟並存取檔案的記錄時，非支援應用程式不會強制執行使用權限。|
|預設檔案類型|這是下列檔案類型的預設保護層級：<br /><br />- 文字和影像檔案<br /><br />- Microsoft Office (Word、Excel、PowerPoint) 檔案<br /><br />- 可攜式文件格式 (.pdf)<br /><br />如需詳細資訊，請參閱下一節的[支援的檔案類型與副檔名](#supported-file-types-and-file-name-extensions)。|這是完整保護不支援的所有其他檔案類型 (如 .vsdx、.rtf 等等) 的預設保護。|
您可以變更 RMS 共用應用程式套用的預設保護層級。 您可以將預設的原生層級變更為一般、從一般變更為原生，甚至阻止 RMS 共用應用程式套用保護。 如需詳細資訊，請參閱本文章中的[變更檔案的預設保護層級](#changing-the-default-protection-level-of-files)一節。

## 支援的檔案類型與副檔名
下表列出 Microsoft Rights Management 共用應用程式原生支援的檔案類型。 當套用原生保護時，這些類型檔案的原始副檔名會變更，且這些檔案會變成唯讀。

此外，當 RMS 共用應用程式原生保護使用者藉由共用保護的 Word、Excel 或 PowerPoint 檔案，這個動作會自動建立第二個檔案，它是原始檔案的副本，具有相同的檔案名稱，但副檔名為 **.ppdf**。 這個版本的檔案可確保安裝了 RMS 共用應用程式的收件者可以隨時開啟已套用原生保護的檔案。

受到一般保護的檔案，原始檔案的副檔名一律會變更為 .pfile。

> [!WARNING]
> 如果您有防火牆、Web proxy 或會檢查並根據副檔名採取動作的安全性軟體，您可能需要重新設定這些安全性功能以支援這些新的副檔名。

|原始副檔名|受 RMS 保護的副檔名|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|。jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|。png|。ppng|
|.tif|.ptif|
|。tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|。giff|.pgiff|
|。jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|
¹ PDF 轉譯由 Foxit 提供。 Copyright © 2003–2014 by Foxit Corporation.

下表列出 Microsoft Rights Management 共用應用程式在 Microsoft Office 2016、Office 2013 和 Office 2010 中原本就支援的檔案類型。 這些檔案受 Rights Management Service 保護後副檔名維持不變。

|Office 支援的檔案類型|Office 支援的檔案類型|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### 變更檔案的預設保護層級
您可以編輯登錄來變更 RMS 共用應用程式對檔案的保護。 例如，您可以強制支援原生保護的檔案受到 RMS 共用應用程式的一般保護。

您會這樣做的可能原因有：

-   若要要確保所有使用者都可以從他們的行動裝置開啟檔案。

-   若要要確保所有沒有支援原生保護之應用程式的使用者都可以開啟檔案。

-   若要配合會依檔案副檔名而採取動作的安全性系統，也可以重新設定系數以配合 .pfile 副檔名，但無法重新設定以配合原生保護的多個副檔名。

同樣地，您可以強制 RMS 共用應用程式對預設會套用一般保護的檔案套用原生保護。 這可能適用於您有支援 RMS API的應用程式的情況 – 例如，內部開發人員所撰寫的企業營運應用程式或向獨立軟體廠商 (ISV) 購買的應用程式。

您也可以強制 RMS 共用應用程式封鎖檔案的保護 (不套用原生保護或一般保護)。 例如，當您有必須能夠開啟特定檔案來處理其內容的自動化應用程式或服務，可能有此需要。 當您封鎖某個檔案類型的保護時，使用者無法使用 RMS 共用應用程式來保護該檔案類型的檔案。 當他們嘗試保護檔案時，會看到訊息指出管理員已防止保護，且他們必須取消其保護檔案的動作。

若要設定 RMS 共用應用程式對預設會套用原生保護的檔案套用一般保護，請進行以下登錄編輯：

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**：建立名為 * 的新金鑰。

    此設定表示具有任何副檔名的檔案。

2.  在新增的金鑰 HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\\\* 中，建立 (REG_SZ) 名為 **Encryption** 的新字串值，且其資料值為 **Pfile**。

    這項設定會導致 RMS 共用應用程式套用一般保護。

這兩項設定會導致 RMS 共用應用程式對所有有副檔名的檔案套用一般保護。 如果這是您的目標，則不需要進一步的設定。 不過，您可以定義特定檔案類型的例外狀況，讓它們仍然受到原生保護。 若要這樣做，您必須為每種檔案類型進行三個額外的登錄編輯：

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection**：加入包含該檔案副檔名 (不含前面的點) 的新機碼。

    例如，為副檔名為 .docx 的檔案建立 **DOCX**機碼。

2.  在新加入的檔案類型機碼中 (例如，**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**)，建立名為 **AllowPFILEEncryption** 的新 DWORD 值，且設定其值為 **0**。

3.  在新加入的檔案類型機碼中 (例如，**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RMSSharingApp\FileProtection\DOCX**)，建立名為 **Encryption** 的新字串值，且設定其值為 **Native**。

進行這些設定後，所有檔案會受到一般保護，但 .docx 副檔名的檔案除外，後者會受到 RMS 共用應用程式的原生保護。

針對您想要定義為例外狀況的其他檔案類型重複這三個步驟，因為它們支援原生保護，而您不要它們受 RMS 共用應用程式的一般保護。

您可以變更 **Encryption** 字串的值，為其他案例進行類似登錄編輯，此字串支援下列值：

-   **Pfile**：一般保護

-   **Native**：原生保護

-   **Off**：封鎖保護

## 另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)




<!--HONumber=Sep16_HO4-->


