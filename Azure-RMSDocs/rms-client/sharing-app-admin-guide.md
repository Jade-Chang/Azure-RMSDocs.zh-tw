---
# required metadata

title: Rights Management 共用應用程式系統管理員指南 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Rights Management 共用應用程式系統管理員指南 (英文)

*適用於︰Active Directory Rights Management Services、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*


如果您負責企業網路上的 Microsoft Rights Management 共用應用程式，或是您想獲得比 [Rights Management 共用應用程式使用者指南](sharing-app-user-guide.md)或[適用於 Windows 的 Microsoft Rights Management 共用應用程式的常見問題集](http://go.microsoft.com/fwlink/?LinkId=303971)中的更多技術資訊，請使用下列資訊。.

RMS 共用應用程式最適合與 Azure RMS 搭配使用，因為此部署設定支援傳送受保護的附件給組織中另一個使用者，並支援電子郵件通知和文件追蹤與撤銷等選項。  不過，遵守一些限制，它也可搭配內部部署版本 AD RMS。 如需 Azure RMS 和 AD RMS 支援的功能完整比較，請參閱[比較 Azure Rights Management 與 AD RMS](../understand-explore/compare-azure-rms-ad-rms.md)。 如果您有 AD RMS 並想要移轉至 Azure RMS，請參閱 [從 AD RMS 移轉至 Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md)。.

## 自動部署 Microsoft Rights Management 共用應用程式
RMS 共用應用程式的 Windows 版本支援指令碼式安裝，這使得它非常適合用於企業部署。

此安裝的唯一必要條件是電腦執行 Windows 7 Service Pack 1 以上的版本且已安裝 Microsoft Framework 4.0 以上的版本。 如果您需要安裝 Microsoft.NET Framework 4.0，可以 [從 Microsoft 下載中心下載並安裝](http://www.microsoft.com/download/details.aspx?id=17718)。.

### 若要下載 RMS 共用應用程式以進行自動部署

1.  請移至 Microsoft 下載中心的 [[Microsoft Rights Management sharing application for Windows]](http://www.microsoft.com/download/details.aspx?id=40857) (適用於 Windows 的 Microsoft Rights Management 共用應用程式) 頁面，按一下 **[下載] **。.

2.  選取並下載您需要的檔案。 有兩個用戶端安裝套件：一個適用於 Windows 64 位元 (Microsoft Rights Management 共用應用程式 x64.zip)，另一個適用於 Windows 32 位元 (Microsoft Rights Management 共用應用程式 x86.zip)。

3.  從壓縮的安裝套件將檔案解壓縮，例如，按兩下檔案。 然後將解壓縮的檔案複製到用戶端電腦可以存取的網路位置。

RMS 共用應用程式的安裝程式套件支援不同的部署案例，並包括下列項目：

|說明|部署狀況|
|---------------|-----------------------|
|Microsoft Online 登入小幫手|Office 2010 和 Azure RMS<br /><br />Office 2013 和 Azure RMS，如果您尚未安裝 [2015 年 6 月9 日，Office 2013 的更新](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hotfix for Office (KB2596501)|Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS|
|讓 AD RMS Client 1.0 可與 Azure RMS 搭配使用的 Hotfix (KB2843630)|Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS|
|AD RMS Client 和 RMS 共用應用程式|Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS<br /><br />Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS<br /><br />僅 RMS 共用應用程式和 Office 增益集|
|功能區的 Office 增益集|Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS<br /><br />Office 2010 和 Azure RMS<br /><br />Office 2010 和 Active Directory RMS<br /><br />僅 RMS 共用應用程式和 Office 增益集|
|Azure Active Directory Rights Management 準備工具|Office 2010 和 Azure RMS|
使用下列程序來識別為這些部署案例部署 RMS 共用應用程式所需的命令：

-   **Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS**

    您的使用者執行 Office 2016 或 Office 2013，您的組織使用 Azure RMS 或 Active Directory RMS，且使用者與使用 Azure RMS 或 Active Directory RMS 的其他組織共同作業。

-   **Office 2010 和 Azure RMS**

    您的使用者執行 Office 2010，您的組織使用 Azure RMS，且使用者與使用 Azure RMS 或 Active Directory RMS 的其他組織共同作業。

-   **Office 2010 和 Active Directory RMS**

    您的使用者執行 Office 2010，您的組織使用 AD RMS，且使用者與使用 Azure RMS 的其他組織共同作業。

-   **僅 RMS 共用應用程式和 Office 增益集**

    您的使用者執行 Office 2016、Office 2013 或 Office 2010，您的組織使用 AD RMS，且使用者不需與使用 Azure RMS 的其他組織共同作業。 此安裝可讓您只安裝共用應用程式和 Office 增益集。

> [!NOTE]
> 在這些案例中，如果您的組織執行 AD RMS，則您的使用者可以接收來自其他使用 Azure RMS 之組織的受保護內容，但您的使用者無法將受保護內容傳送給使用 Azure RMS 之組織中的使用者。 不過，如果您的組織執行 Azure RMS，您的使用者可以傳送和接收來自其他組織的受保護內容。

您必須重新啟動電腦，才能完成每個程序的安裝。 您可以使用命令 (例如 **shutdown /i**) 起始自動重新啟動。.

### 若要為 Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS 部署 RMS 共用應用程式

-   在您想要安裝 RMS 共用應用程式和相關元件的每一部電腦上，以提高的權限執行下列命令：

    ```
    setup.exe /s
    ```

若要確認是否成功，請參閱本文章中的[確認安裝成功](#verifying-installation-success)一節。

### 若要為 Office 2010 和 Azure RMS 部署 RMS 共用應用程式

1.  您必須是 Office 365 或 Azure Active Directory 租用戶的全域管理員，才可以藉由執行 Azure Active Directory Rights Management 準備工具取得貴組織的憑證服務 URL。 您只需要在單一電腦上執行此工具一次。 當您在每一部電腦上安裝 RMS 共用應用程式時，將使用憑證服務 URL：

    1.  使用本機系統管理員帳戶登入電腦。

    2.  在該電腦上 [下載並安裝 Microsoft Online 登入小幫手](http://www.microsoft.com/download/details.aspx?id=28177)。.

    3.  執行下列命令以查看顯示在螢幕上的憑證服務 URL，您可加以複製儲存供下個步驟使用：

        -   Windows 8.1 和 Windows 8，64 位元：

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Windows 8.1 和 Windows 8，32 位元：

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   若為 Windows 7，64 位元：

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > 此命令可能會提示您輸入 Azure 認證。 如果電腦未加入網域，系統會提示您。 如果電腦已加入網域，此工具可能可以使用快取的認證。

2.  在您要安裝 RMS 共用應用程式的每一部電腦上，以提高的權限執行下列命令：

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  在您要安裝 RMS 共用應用程式的每一部電腦上，使用者必須執行下列命令 (不需使用提高的權限)。 有不同的方式可達到這個目的，包括要求使用者執行命令 (例如，電子郵件中的連結或技術支援入口網站上的連結)，或您可以將它加入使用者的登入指令碼：

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

若要確認是否成功，請參閱本文章中的[確認安裝成功](#verifying-installation-success)一節。

### 若要為 Office 2010 和 Active Directory RMS 部署 RMS 共用應用程式

1.  在您要安裝 RMS 共用應用程式的每一部電腦上，以提高的權限執行下列命令：

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  在您要安裝 RMS 共用應用程式的每一部電腦上，使用者必須執行下列命令 (不需使用提高的權限)。 有不同的方式可達到這個目的，包括要求使用者執行命令 (例如，電子郵件中的連結或技術支援入口網站上的連結)，或您可以將它加入使用者的登入指令碼：

    -   Windows 10、Windows 8.1、Windows 8，64 位元：

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Windows 10、Windows 8.1、Windows 8，32 位元：

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   若為 Windows 7，64 位元：

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

若要確認是否成功，請參閱本文章中的[確認安裝成功](#verifying-installation-success)一節。

### 若僅安裝 RMS 共用應用程式和 Office 增益集

1.  使用下列命令安裝 AD RMS Client 和 RMS 共用應用程式：

    -   若為 64 位元 Windows：

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   若為 32 位元 Windows：

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    例如： `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  使用下列命令安裝 Office 增益集：

    -   若為 64 位元版本的 Office：

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   若為 32 位元版本的 Office：

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    例如： `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

若要確認是否成功，請參閱本文章中的[確認安裝成功](#verifying-installation-success)一節。

## 確認安裝成功
您可以使用安裝記錄檔來確認安裝成功。

### 若要確認 Office 2016 或 Office 2013 和 Azure RMS 或 Active Directory RMS 的 RMS 共用應用程式安裝成功

-   若要確認在每部電腦上 Setup.exe 命令執行成功，請在 *%temp%\RMS_installer_&lt;guid&gt;* 資料夾中搜尋安裝記錄檔 **RMInstaller.log**，然後找到結束代碼。

    成功安裝的結束代碼是 0，任何其他數字都表示安裝失敗。

    範例記錄檔名稱：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### 若要確認 Office 2010 和 Azure RMS 的 RMS 共用應用程式安裝成功

1.  若要確認在每部電腦上 Setup.exe 命令執行成功，請在 *%temp%\RMS_installer_&lt;guid&gt;* 資料夾中搜尋安裝記錄檔 **RMInstaller.log**，然後找到結束代碼。

    成功安裝的結束代碼是 0，任何其他數字都表示安裝失敗。

    範例記錄檔名稱：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  若要確認 RMSSetup.exe 命令執行成功，使用者的 *%localappdata%\microsoft\drm* 資料夾中應已建立下列檔案：

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    CLC-&#42;.drm 檔案的範例：

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### 若要確認 Office 2010 和 Active Directory RMS 的 RMS 共用應用程式安裝成功

1.  若要確認在每部電腦上 Setup.exe 命令執行成功，請在 *%temp%\RMS_installer_&lt;guid&gt;* 資料夾中搜尋安裝記錄檔，然後找到結束代碼。

    成功安裝的結束代碼是 0，任何其他數字都表示安裝失敗。

    範例記錄檔名稱：**C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  若要確認在每部電腦上 aadrmprep.exe 命令執行成功，請在安裝記錄檔中搜尋下列文字： **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > 有時候，這項安裝可能執行兩次；第一次出現失敗，第二次成功。

    如果您想要手動檢查這項工具所產生的登錄變更，如下所示：

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;憑證 URL&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### 若要確認僅 RMS 共用應用程式和 Office 增益集的安裝成功

1.  若要確認 Setup_ipviewer.exe 命令執行成功，請在安裝記錄檔中搜尋下列文字：**安裝成功或錯誤：0**

    安裝成功的記錄範例

    **MSI (s) (F0:B8) [14:19:57:854]:產品：Active Directory Rights Management Services 用戶端 2.1 -- 安裝順利完成。**

    **MSI (s) (F0:B8) [14:19:57:854]:Windows Installer 已安裝產品。 產品名稱：Active Directory Rights Management Services 用戶端 2.1。 Product Version:1.0.1179.1. Product Language:1033. 製造商：Microsoft Corporation. 安裝成功或錯誤狀態：0.**

2.  若要確認在每部電腦上 Office 增益集安裝成功，請在安裝記錄檔中搜尋下列文字：**安裝成功或錯誤：0**

    安裝成功的記錄範例

    **MSI (s) (9C:88) [18:49:04:007]:產品：Microsoft RMS Office 增益集 -- 安裝順利完成。**

    **MSI (s) (9C:88) [18:49:04:007]:Windows Installer 已安裝產品。 產品名稱：Microsoft RMS Office 增益集。 Product Version:1.0.7. Product Language:1033. 製造商：Microsoft. 安裝成功或錯誤狀態：0.**

## 解除安裝命令
這些部署所需的安裝命令並非全都支援解除安裝命令。 您可以解除安裝 AD RMS 用戶端和共用應用程式，且您可以解除安裝 Office 增益集。 使用下列命令解除安裝這些項目。

### 若要解除安裝 AD RMS Client 和 RMS 共用應用程式

-   使用下列命令：

    -   若為 64 位元 Windows：

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   若為 32 位元 Windows：

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### 解除安裝 Office 增益集

-   使用下列命令：

    -   若為 64 位元版本的 Office：

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   32 位元版本的 Office：

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## 隱藏自動更新
根據預設，如果有更新版本的 RMS 共用應用程式，系統會通知使用者，並提示您下載它。 您可以藉由編輯下列登錄隱藏此通知：

1.  巡覽至 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC**，如果不存在的話，請建立名為 **RmsSharingApp** 的新金錀。.

2.  選取 **RmsSharingApp**，建立新的 DWORD 值 **AllowUpdatePrompt**，並將值設定為 **0**。.

因為 WSUS 不支援 RMS 共用應用程式，您可以使用下列技巧來測試任何新版本的 RMS 共用應用程式，再將它部署至所有使用者：

1.  在所有使用者的電腦上，執行指令碼來隱藏自動更新。 在系統管理員用來測試新版本的電腦上，請勿執行此指令碼。

2.  當有新版本可用時，系統管理員會下載並進行測試。

3.  當測試完成並已解決任何問題，請使用本指南中的自動部署指示，將最新版本部署到所有使用者。

## 僅 Azure RMS：設定文件追蹤
如果您有[支援文件追蹤的訂用帳戶](https://technet.microsoft.com/en-us/dn858608)，您的組織預設會替所有使用者啟用文件追蹤網站。  文件追蹤會顯示資訊，像是嘗試存取使用者共用之受保護文件的人的電子郵件地址、這些人何時嘗試存取它們、他們的位置等。 如果基於隱私權需求您的組織禁止顯示這項資訊，您可以使用 [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) Cmdlet 停用對文件追蹤網站的存取。 您隨時可以使用 [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 重新啟用對網站的存取，且可以使用 [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) 檢查目前是啟用或停用存取。.

若要執行這些 Cmdlet，您至少必須有適用於 Windows PowerShell 的 Azure RMS 模組的最新版本 **2.3.0.0**。  如需安裝指示，請參閱 [安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。.

> [!TIP]
> 如果您先前已下載及安裝此模組，請執行下列命令來檢查版本號碼： `(Get-Module aadrm –ListAvailable).Version`

必須允許下列用於文件追蹤的 URL (例如，若您使用增強安全性的 Internet Explorer，將其加入您的信任網站)：

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > 此 URL 是 Bing 地圖。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## 僅限 AD RMS：支援貴組織內有多個電子郵件網域
如果您使用 AD RMS，且貴組織中的使用者有多個電子郵件網域，或許是導因於合併或收購，您就必須進行下列登錄編輯：

1.  巡覽至 **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC**，如果不存在的話，請建立名為 **RmsSharingApp** 的新金錀。.

2.  選取 **RmsSharingApp**，建立新的名為 **FederatedDomains** 的多字串值，然後加入您的組織使用的所有網域和子網域。 不支援萬用字元。

    例如：Coho Vineyard &amp; Winery 公司有標準電子郵件網域 **cohovineyardandwinery.com**，但因為合併的關係，也使用電子郵件網域 **cohowinery.com**、**eastcoast.cohowinery.com** 和 **cohovineyard**。 系統管理員在 **FederatedDomains** 值資料輸入 **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

如果您不做此登錄變更，使用者可能無法使用受到組織中其他使用者保護的內容。 如果您使用 Azure RMS，就不需要進行此登錄編輯。


## 後續步驟
如需包含說明保護層級 (原生和一般) 之間的差異、支援的檔案類型和檔案名稱副檔名，以及如何變更預設的保護層級的詳細技術資訊，請參閱 [Rights Management 共用應用程式的技術概觀](sharing-app-admin-guide-technical.md)。.



<!--HONumber=Apr16_HO4-->


