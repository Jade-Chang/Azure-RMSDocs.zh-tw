---
title: "重新整理範本 | Azure Information Protection"
description: "當您使用 Azure Rights Management Service 時，範本會自動下載到用戶端電腦，讓使用者可以從他們的應用程式中選取這些範本。 不過，如果您對這些範本做了變更，可能就需要採取一些其他步驟。"
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b6a1fc3fa0a19f3a6b65aa7b8815eda7432cd7
ms.openlocfilehash: 2870edc314f3ee6f6e3b8937cbe5b653092c5910


---


# 重新整理使用者的範本

>*適用於︰Azure Information Protection、Office 365*

當您使用 Azure Information Protection 的 Azure Rights Management Service 時，範本會自動下載到用戶端電腦，讓使用者可以從他們的應用程式中選取這些範本。 不過，如果您對這些範本做了變更，可能就需要採取一些其他步驟：

|應用程式或服務|變更範本後如何重新整理範本|
|--------------------------|---------------------------------------------|
|Exchange Online|需要手動設定組態來重新整理範本。<br /><br />如需設定步驟，請參閱下列章節，[僅適用於 Exchange Online：如何設定 Exchange 下載已變更的自訂範本](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates)。|
|Office 365|自動重新整理 - 不需要其他步驟。|
|Office 2016 和 Office 2013<br /><br />適用於 Windows 的 RMS 共用應用程式|自動重新整理 - 透過排程：<br /><br />若為這些更新版本的 Office︰預設重新整理間隔是每 7 天。<br /><br />若為適用於 Windows 的 RMS 共用應用程式：從 1.0.1784.0 版開始，預設重新整理間隔是每 1 天。 舊版的預設值重新整理間隔是每 7 天。<br /><br />若要強制進行比這個排程更快的重新整理，請參閱下列章節，[適用於 Windows 的 Office 2016、Office 2013 及 RMS 共用應用程式︰如何強制重新整理已變更的自訂範本](#office-2016-office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template)。|
|Office 2010|在使用者登入時重新整理。<br /><br />若要強制重新整理，請要求或強制使用者登出後再重新登入。 或者，請參閱下一節：[僅適用於 Office 2010：如何強制重新整理已變更的自訂範本](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template)。|
對於使用 RMS 共用應用程式的行動裝置，不需要設定其他組態，系統就會自動下載範本 (並在必要時重新整理)。

## 僅適用於 Exchange Online：如何設定 Exchange 下載已變更的自訂範本
如果您已經為 Exchange Online 設定資訊版權管理 (IRM)，在您於 Exchange Online 中使用 Windows PowerShell 進行下列變更之前，系統將不會為使用者下載自訂範本。

> [!NOTE]
> 如需關於如何在 Exchange Online 中使用 Windows PowerShell 的詳細資訊，請參閱[搭配 Exchange Online 使用 PowerShell](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx)。

您必須在每次變更範本時都執行這個程序。

### 更新 Exchange Online 的範本

1.  在 Exchange Online 中使用 Windows PowerShell，連線至服務：

    1.  提供您的 Office 365 使用者名和密碼：

        ```
        $Cred = Get-Credential
        ```

    2.  執行下列兩個命令連線到 Exchange Online 服務：

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  使用 [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) Cmdlet 從 Azure RMS 重新匯入信任的發佈網域 (TPD)：

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    例如，如果您的 TPD 名稱是 **RMS Online-1** (許多組織的典型名稱)，請輸入︰**Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**

    > [!NOTE]
    > 若要驗證您的 TPD 名稱，您可以使用 [Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) Cmdlet。

3.  若要確認是否已經成功匯入範本，請等候幾分鐘，然後執行 [Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) Cmdlet 並將 Type 設為 All。 例如：

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > 保留輸出內容的副本十分有用，這麼做可讓您於稍後封存範本時輕鬆地複製範本名稱或 GUID。

4.  對於您希望可在 Outlook Web App 中使用的每個匯入的範本，您必須使用 [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) Cmdlet，並將 Type 設為 Distributed：

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    因為 Outlook Web Access 會快取 UI 24 小時，所以使用者可能會一整天都看不到新範本。

此外，如果您封存某個範本 (自訂或預設) 並使用 Exchange Online 搭配 Office 365，則當使用者使用 Outlook Web App 或採用了 Exchange ActiveSync 通訊協定的行動裝置時，將會繼續看見已封存的範本。

為了讓使用者不再看見這些範本，請在 Exchange Online 中使用 Windows PowerShell 來連線至服務，然後執行下列命令以使用 [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) Cmdlet：

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

## Office 2016、Office 2013 及 Windows 的 RMS 共用應用程式：如何強制重新整理已變更的自訂範本
藉由在執行 Office 2016、Office 2013 或 Windows 的 Rights Management (RMS) 共用應用程式的電腦上編輯登錄，您可以變更自動排程，使變更的範本在電腦上的重新整理頻率比它們的預設值更頻繁。 您也可以刪除登錄值中的現有資料來強制立即重新整理。

> [!WARNING]
> 如果您使用登錄編輯程式的方式不正確，可能會發生嚴重的問題而導致可能需要重新安裝作業系統。 Microsoft 無法保證您可以解決因不正確使用登錄編輯程式而導致的問題。 您需自行承擔使用登錄編輯程式的風險。

### 變更自動排程

1.  使用登錄編輯程式，建立並設定下列其中一個登錄值：

    - 設定以天為單位的更新頻率 (最小值 1 天)：建立名為 **TemplateUpdateFrequency** 的新登錄值並為資料定義整數值，該值可指定下載任何已下載範本之變更的頻率，以天為單位。 使用下列資訊來尋找登錄路徑以建立這個新的登錄值。

        **登錄路徑︰**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **類型：**REG_DWORD

        **值：**TemplateUpdateFrequency

    - 設定以秒為單位的更新頻率 (最小值 1 秒)：建立名為 **TemplateUpdateFrequencyInSeconds** 的新登錄值並為資料定義整數值，該值可指定下載任何已下載範本之變更的頻率，以秒為單位。 使用下列資訊來尋找登錄路徑以建立這個新的登錄值。

        **登錄路徑︰**HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **類型：**REG_DWORD

        **值：** TemplateUpdateFrequencyInSeconds

    請確定您建立並設定其中一個登錄值，不能兩者同時設定。 如果兩者均存在， **TemplateUpdateFrequency** 會被忽略。

2.  如果您想要強制立即重新整理範本，請移至下一個程序。 否則，立即重新啟動您的 Office 應用程式和 [檔案總管] 的執行個體。

### 強制立即重新整理

1.  使用登錄編輯程式，刪除 **LastUpdatedTime** 值的資料。 例如，資料可能會顯示 **2015-04-20T15:52**，請刪除 2015-04-20T15:52，就不會顯示任何資料。 使用下列資訊來尋找登錄路徑以刪除這個登錄值資料。

    **登錄路徑︰** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **類型：**REG_SZ

    **值：**LastUpdatedTime

    > [!TIP]
        > 在登錄路徑中，<*MicrosoftRMS_FQDN*> 指的是您的 Microsoft RMS 服務 FQDN。 如果您想要確認此值：

    > 1.  執行 Azure RMS 的 [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) Cmdlet。 如果您尚未針對 Azure RMS 安裝 Windows PowerShell 模組，請參閱[針對 Azure Rights Management 安裝 Windows PowerShell](install-powershell.md)。
    > 2.  從輸出中找出 **LicensingIntranetDistributionPointUrl** 值。
    > 
    >     例如：**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  從該值，移除此字串的 **https://** 和 **/_wmcs/licensing**。 其餘的值為您的 Microsoft RMS 服務 FQDN。 在我們的範例中，Microsoft RMS 服務 FQDN 將為下列值：
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  刪除下列資料夾和其所包含的所有檔案：**%localappdata%\Microsoft\MSIPC\Templates**

3.  重新啟動您的 Office 應用程式和 [檔案總管] 的執行個體。

## 僅適用於 Office 2010：如何強制重新整理已變更的自訂範本
藉由在執行 Office 2010 的電腦上編輯登錄，您可以設定一個值，讓變更的範本在電腦上重新整理，而不需要等待使用者登出與登入。 您也可以刪除登錄值中的現有資料來強制立即重新整理。

> [!WARNING]
> 如果您使用登錄編輯程式的方式不正確，可能會發生嚴重的問題而導致可能需要重新安裝作業系統。 Microsoft 無法保證您可以解決因不正確使用登錄編輯程式而導致的問題。 您需自行承擔使用登錄編輯程式的風險。

### 變更更新頻率

1.  始用登錄編輯程式，建立名為 **UpdateFrequency** 的新登錄值並為資料定義整數值，該值可指定下載任何已下載範本之變更的頻率，以天為單位。 使用下表來尋找登錄路徑以建立這個新的登錄值。

    **登錄路徑︰**HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **類型：**REG_DWORD

    **值：**UpdateFrequency

2.  如果您想要強制立即重新整理範本，請移至下一個程序。 否則，立即重新啟動您的 Office 應用程式。

### 強制立即重新整理

1.  使用登錄編輯程式，刪除 **LastUpdatedTime** 值的資料。 例如，資料可能會顯示 **2015-04-20T15:52**，請刪除 2015-04-20T15:52，就不會顯示任何資料。 使用下表來尋找登錄路徑以刪除這個登錄值資料。

    **登錄路徑︰**HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **類型：**REG_SZ

    **值：**lastUpdatedTime


2.  刪除下列資料夾和其所包含的所有檔案：**%localappdata%\Microsoft\MSIPC\Templates**

3.  重新啟動您的 Office 應用程式。

## 另請參閱
[設定 Azure Rights Management 的自訂範本](configure-custom-templates.md)


<!--HONumber=Sep16_HO4-->


