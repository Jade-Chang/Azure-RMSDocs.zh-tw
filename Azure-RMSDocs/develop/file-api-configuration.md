---
title: "檔案 API 組態 | Azure RMS"
description: "可透過登錄中設定進行設定的檔案 API 的行為。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d2339ece646fc51410186d43facdea28ac8fdfe
ms.openlocfilehash: 8232137fb52b03a30513b132b02251f3cc01079a


---

# 檔案 API 組態


可透過登錄中設定進行設定的檔案 API 的行為。

檔案 API 提供兩種類型的保護；原生保護與 PFile 保護。

-   **原生保護** - 根據其 MIME 類型 (副檔名) 的 AD RMS 格式來保護檔案。
-   **PFile 保護** - 檔案受到 AD RMS 受保護檔案 (PFile) 格式所保護。

如需有關支援的檔案格式的詳細資訊，請參閱本題的**檔案 API 檔案支援詳細資料**。

## 機碼/機碼值類型和描述

下列章節說明用於控制加密的機碼和機碼值。

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection

**類型**︰機碼

**描述**︰包含檔案 API 的一般設定。

### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;

**類型**︰機碼

**描述**︰指定特定副檔名的設定資訊；例如，TXT、JPG 等等。

- 允許萬用字元 '*'；不過，特定副檔名的設定優先於萬用字元設定。 萬用字元不會影響 Microsoft Office 檔案的設定；必須依檔案類型明確停用這些設定。
- 若要指定沒有副檔名的檔案，請使用 '.'
- 指定特定副檔名的機碼時，不指定 '' 字元；例如使用 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` 來指定 .txt 檔案的設定。 (請勿使用 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`)。

設定機碼中的 **Encryption** 值來指定保護行為。 若未設定 **Encryption** 值，則會執行檔案類型的預設行為。


### HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\&lt;EXT&gt;\Encryption*

**類型**：REG_SZ

**描述**：包含三個值之一：

- **Off**︰已停用加密。

> [!Note] 
> 這項設定對解密並無任何影響。 只要使用者擁有 **EXTRACT** 權限，無論加密的檔案是使用原生或 Pfile 保護加密，都能予以解密。

- **Native**︰使用原生加密。 對於 Office 檔案，加密的檔案將具有原始檔案的相同副檔名。 例如，.docx 副檔名的檔案將會加密到副檔名為.docx 的檔案。 對於其他可能已套用原生保護的檔案，會將檔案加密成副檔名格式為 p*zzz* 的檔案，其中 *zzz* 是原始副檔名。 例如，.txt 檔案會加密為副檔名為 .ptxt 的檔案。 以下包含可能已套用原生保護的副檔名清單。

- **Pfile**︰使用 PFile 加密。 加密的檔案會有附加到原始副檔名的 .pfile。 例如，加密後，.txt 檔案將具有 txt.pfile 副檔名。


> [!Note] 
> 此設定對 Office 檔案格式並無任何影響。 例如，如果 `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` 值設為 &quot;Pfile”，.docx 檔案仍會利用原生保護加密，且加密的檔案仍會具有副檔名 .docx。

設定任何其他值，或不設定值以執行預設行為。

## 不同檔案格式的預設行為

-   **Office 檔案** 啟用原生加密。
-   **txt、xml、jpg、jpeg、pdf、png、tiff、bmp、gif、giff、jpe、jfif、jif 檔案** 啟用原生加密 (xxx 變成 pxxx)
-   **所有其他檔案** 啟用受保護檔案 (pfile) 加密 (xxx 成為 xxx.pfile)

若嘗試在封鎖的檔案類型上加密，會發生 [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes) 錯誤。

### 檔案 API- 檔案支援詳細資料

可為任何檔案類型 (副檔名) 新增原生支援。 例如，如果副檔名 &lt;ext&gt; (非 office) 的管理設定為 "NATIVE"，任何這類副檔名都會使用 \*.p&lt;ext&gt;。

**Office 檔案**

-   副檔名︰doc、dot、xla、xls、xlt、pps、ppt、docm、docx、dotm、dotx、xlam、xlsb、xlsm、xlsx、xltm、xltx、xps、potm、potx、ppsx、ppsm、pptm、pptx、thmx。
-   保護類型 = Native (預設值)︰sample.docx 會加密成 sample.docx
-   保護類型 = Pfile︰對於 Office 檔案，與 Native 具有相同的效果。
-   Off︰停用加密。

**PDF 檔案**

-   保護類型 = Native：sample.pdf 會加密並命名為 sample.ppdf
-   保護類型 = Pfile：sample.pdf 會加密並命名為 sample.pdf.pfile。
-   Off︰停用加密。

**所有其他檔案格式**

-   保護類型 = Pfile：sample.*zzz* 會加密並命名為 sample.*zzz*.pfile；其中 *zzz* 是原始副檔名。
-   Off︰停用加密。

### 範例

下列設定會啟用 txt 檔案的 PFile 加密。 Office 檔案將套用原生保護 (預設值)、txt 檔案將套用 PFile 保護，而封鎖其他所有檔案的保護 (預設值)。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

下列設定會啟用所有非 Office 檔案 (txt 檔案除外) 的 PFile 加密。 Office 檔案將套用原生保護 (預設值)、txt 檔案將封鎖保護，其他所有檔案則套用 PFile 保護。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

下列設定停用 docx 檔案的原生加密。 非 docx 檔案的 Office 檔案將套用原生保護 (預設值)，並封鎖其他所有檔案的保護 (預設值)。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## 相關的主題

* [開發人員注意事項](developer-notes.md)
* [**IPCERROR\_FILE\_ENCRYPT\_BLOCKED**](/rights-management/sdk/2.1/api/win/error%20codes)
 

 



<!--HONumber=Aug16_HO4-->


