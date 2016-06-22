---
# required metadata

title: 具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 具有 Windows Server 檔案分類基礎結構 (FCI) 的 RMS 保護

*適用於︰Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

使用這份文件作為指示，以及搭配 RMS 保護工具來使用 Rights Management (RMS) 用戶端的指令碼，以設定檔案伺服器資源管理員和檔案分類基礎結構 (FCI)。

這個解決方案可讓您自動保護執行 Windows Server 的檔案伺服器上的資料夾中的所有檔案，或自動保護符合特定準則的檔案。 例如，已分類為包含機密或敏感資訊的檔案。 這個解決方案會使用 Azure Rights Management (Azure RMS) 來保護檔案，所以您必須在組織中部署這項技術。

> [!NOTE] 雖然 Azure RMS 包含支援檔案分類基礎結構的[連接器](../deploy-use/deploy-rms-connector.md)，但是該解決方案僅支援原生保護，例如 Office 檔案。
> 
> 若要支援具有檔案分類基礎結構的所有檔案類型，您必須使用 Windows PowerShell **RMS 保護** 模組，如本文所述。 RMS 保護 Cmdlet，像是 RMS 共用應用程式，支援一般保護以及原生保護，這表示可以保護所有檔案。 如需不同保護層級的詳細資訊，請參閱 [Rights Management 共用應用程式系統管理員指南](sharing-app-admin-guide.md)中的[保護層級 – 原生和一般](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)一節。

接下來的指示適用於 Windows Server 2012 R2 或 Windows Server 2012。 如果您執行其他支援的 Windows 版本，您可能需要針對您的作業系統版本和本文所述版本之間的差異，調整一些步驟。

## 具有 Windows Server FCI 之 Azure RMS 保護的必要條件
這些指示的必要條件：

-   在您於其中執行具有檔案分類基礎結構的檔案資源管理員的每個檔案伺服器：

    -   您已安裝檔案伺服器資源管理員做為檔案服務角色的其中一個角色服務。

    -   您已識別包含要使用 Rights Management 保護的檔案的本機資料夾。 例如，C:\FileShare。

    -   您已安裝 RMS 保護工具，包括工具 (例如 RMS 用戶端) 和 Azure RMS (例如服務主體帳戶) 的必要條件。 如需詳細資訊，請參閱 [RMS 保護 Cmdlet](https://msdn.microsoft.com/library/azure/mt433195.aspx)。

    -   如果您想要針對特定副檔名變更 RMS 保護的預設層級 (原生或一般)，則編輯登錄，如[檔案 API 組態](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx)頁面所述。

    -   您有網際網路連接，如果 Proxy 伺服器需要，電腦設定也已進行設定。 例如： `netsh winhttp import proxy source=ie`

-   您已經為您的 Azure Rights Management 部署設定額外必要條件，如 [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)中所述。 具體而言，您使用服務主體時有下列值來連接至 Azure RMS：

    -   BposTenantId

    -   AppPrincipalId

    -   對稱金鑰

-   您已同步處理您的內部部署 Active Directory 使用者帳戶與 Azure Active Directory 或 Office 365，包括其電子郵件地址。 所有使用者都需要此項，才能存取受到 FCI 和 Azure RMS 保護的檔案。 如果你未執行此步驟 (例如，在測試環境中)，使用者可能會被阻止存取這些檔案。 如果您需要此帳戶組態的詳細資訊，請參閱[準備 Azure Rights Management](../plan-design/prepare.md)。

-   您已識別要使用的 Rights Management 範本，它會保護檔案。 請確定您知道此範本的識別碼，方法是使用 [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) Cmdlet。

## 設定 Azure RMS 保護的檔案伺服器資源管理員 FCI 的指示
請遵循這些指示以使用 Windows PowerShell 指令碼做為自訂工作，來自動保護資料夾中的所有檔案。 以下列順序執行這些程序：

1.  儲存 Windows PowerShell 指令碼

2.  建立 Rights Management (RMS) 的分類屬性

3.  建立分類規則 (針對 RMS 分類)

4.  設定分類排程

5.  建立自訂檔案管理工作 (使用 RMS 保護檔案)

6.  以手動方式執行規則和工作來測試組態

在這些指示的結尾，您選取的資料夾中的所有檔案會分類為 RMS 的自訂屬性，然後這些檔案會受到 Rights Management 的保護。 對於選擇性保護某些檔案而不保護其他檔案的較複雜設定，您可以建立或使用不同的分類屬性和規則，具有僅保護這些檔案的檔案管理工作。

### 儲存 Windows PowerShell 指令碼

1.  使用檔案伺服器資源管理員來複製 [Windows PowerShell Script](fci-script.md) for Azure RMS 保護的內容。 將指令碼的內容貼上至您自己的電腦，並且將檔案命名為 **RMS-Protect-FCI.ps1**。

2.  檢閱指令碼並且進行下列變更：

    -   搜尋下列字串並且以您用於 [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) Cmdlet 的 AppPrincipalId 取代，以連線至 Azure RMS：

        ```
        <enter your AppPrincipalId here>
        ```
        例如，指令碼可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   搜尋下列字串並且以您用於 [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) Cmdlet 的對稱金鑰取代，以連線至 Azure RMS：

        ```
        <enter your key here>
        ```
        例如，指令碼可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   搜尋下列字串並且以您用於 [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) Cmdlet 的 BposTenantId (租用戶 ID) 取代，以連線至 Azure RMS：

        ```
        <enter your BposTenantId here>
        ```
        例如，指令碼可能如下所示：

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   如果您的伺服器執行 Windows Server 2012，您可能必須在指令碼開頭手動載入 RMSProtection 模組。 新增下列命令 (或同等命令，如果 "Program Files" 資料夾是在 C: 磁碟機以外的磁碟機上：

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  簽署指令碼。 如果您未簽署指令碼 (較安全)，您必須在執行它的伺服器上設定 Windows PowerShell。 例如，使用 **[以系統管理員身分執行]** 選項來執行 Windows PowerShell 工作階段，然後輸入：**Set-ExecutionPolicy RemoteSigned**。 不過，這種設定會讓所有未簽署的指令碼在儲存於此伺服器時執行 (較不安全)。

    如需有關簽署 Windows PowerShell 指令碼的詳細資訊，請參閱 PowerShell 文件庫中的 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) 。

4.  在其中執行具有檔案分類基礎結構的檔案資源管理員的每個檔案伺服器上，本機儲存檔案： 例如，將檔案儲存在 **C:\RMS-Protection**。 藉由使用 NTFS 權限來保護此檔案，這樣未經授權的使用者就不能修改它。

您現在可以開始設定檔案伺服器資源管理員。

### 建立 Rights Management (RMS) 的分類屬性

-   在 [檔案伺服器資源管理員]、[分類管理] 中，建立新的本機屬性：

    -   **名稱**：輸入 **RMS**

    -   **描述**： 輸入 **Rights Management 保護**

    -   **屬性類型**︰選取 [是/否]

    -   **值**︰選取 [是]

我們現在可以建立使用這個屬性的分類規則。

### 建立分類規則 (針對 RMS 分類)

-   建立新的分類規則：

    -   在 [一般]  索引標籤上：

        -   **名稱**：輸入 **針對 RMS 分類**

        -   **[已啟用]**：保留預設值，預設值為選取此核取方塊。

        -   **描述**：輸入**針對 Rights Management 分類 &lt;資料夾名稱&gt; 資料夾中的所有檔案**。

            將 *&lt;資料夾名稱&gt;* 取代為您選擇的資料夾名稱。 例如，**針對 Rights Management 分類 C:\FileShare 資料夾中的所有檔案**

        -   **範圍**：新增您選擇的資料夾。 例如，**C:\FileShare**。

            請不要選取任何核取方塊。

    -   在 [分類]  索引標籤上：

    -   **分類方法**：選取 [資料夾分類器] 

    -   **屬性** 名稱：選取 [RMS] 

    -   屬性 **值**：選取 [是] 

雖然您可以手動執行分類規則，但是對於進行中的作業，您會想要排程執行此規則，讓新的檔案以 RMS 屬性進行分類。

### 設定分類排程

-   在 [自動分類]  索引標籤上：

    -   **啟用固定排程**：選取此核取方塊。

    -   針對要執行的所有分類規則設定排程，其中包含我們以 RMS 屬性分類檔案的新規則。

    -   **允許對新檔案進行連續分類**：選取此核取方塊，便會分類新的檔案。

    -   選用：進行您想要的任何其他變更，例如設定報告和通知的選項。

現在您已經完成分類設定，您可以設定管理工作以將 RMS 保護套用至檔案。

### 建立自訂檔案管理工作 (使用 RMS 保護檔案)

-   在 [檔案管理工作] 中，建立新的檔案管理工作：

    -   在 [一般]  索引標籤上：

        -   **工作名稱**：輸入 **以 RMS 保護檔案**

        -   保持選取 [啟用]  核取方塊。

        -   **描述**：輸入**藉由使用 Windows PowerShell 指令碼，以 Rights Management 和範本保護 &lt;資料夾名稱&gt; 中的檔案**

            將 *&lt;資料夾名稱&gt;* 取代為您選擇的資料夾名稱。 例如，**藉由使用 Windows PowerShell 指令碼，以 Rights Management 和範本保護 C:\FileShare 中的檔案**

        -   **範圍**：選取您選擇的資料夾。 例如，**C:\FileShare**。

            請不要選取任何核取方塊。

    -   在 [動作]  索引標籤上：

        -   **類型**：選取 [自訂] 

        -   **可執行檔**：指定下列項目：

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            如果 Windows 不是在 C: 磁碟機上，修改此路徑或瀏覽至此檔案。

        -   **引數**：指定下列項目，提供您自己的 &lt;路徑&gt; 和 &lt;範本識別碼&gt; 值：

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            例如，如果您將指令碼複製到 C:\RMS-Protection，且您從必要條件識別的範本識別碼為 e6ee2481-26b9-45e5-b34a-f744eacd53b0，請指定下列項目：

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            在這個命令中，[來源檔案路徑] 和 [來源檔案擁有者電子郵件] 都是 FCI 特定變數，因此請在上述命令中如實輸入。 FCI 使用第一個變數以自動指定資料夾中的已識別檔案，第二個變數是讓 FCI 自動擷取已識別檔案之具名擁有者的電子郵件地址。 此命令會針對資料夾中的每個檔案重複，在我們的範例中，是 C:\FileShare 資料夾中的每個檔案，另外具有 RMS 做為檔案分類屬性。

            > [!NOTE]
            > **-OwnerMail [來源檔案擁有者電子郵件]** 參數和值可確保在檔案受到保護之後，檔案的原始擁有者已被授與為檔案的 Rights Management 擁有者。 這可確保原始檔案擁有者對其自己的檔案具有所有 Rights Management 權限。 當檔案是由網域使用者建立時，會使用檔案的 [擁有者] 屬性中的使用者帳戶名稱，自動從 Active Directory 擷取電子郵件地址。 若要做到這一點，檔案伺服器必須與使用者位於相同的網域或信任的網域中。
            > 
            > 請盡可能將原始的擁有者指派至受保護的文件，以確保這些使用者繼續擁有他們所建立之檔案的完整控制權。 不過，如果您使用上述的 [來源檔案擁有者電子郵件] 變數，且檔案沒有定義為擁有者的網域使用者 (例如，用於建立檔案的本機帳戶，讓使用者顯示 SYSTEM)，則指令碼將會失敗。
            > 
            > 對於沒有網域使用者做為擁有者的檔案，您可以自行以網域使用者身分複製及儲存這些檔案，如此您就會變成這些檔案的擁有者。 或者，如果您有權限，可以手動變更擁有者。  或者，您可以提供特定電子郵件地址 (例如您自己或 IT 部門的群組地址)，而不是 [來源檔案擁有者電子郵件] 變數，這表示您使用這個指令碼保護的所有檔案將會使用此電子郵件地址來定義新的擁有者。

    -   **命令執行身分**：選取 [本機系統] 

    -   在 [條件]  索引標籤上：

        -   **屬性**：選取 [是/否] **RMS**

        -   **運算子**：選取 [等於]

        -   **值**︰選取 [是]

    -   在 [排程]  索引標籤上：

        -   **執行身分**：設定您偏好的排程。

            允許充足的時間讓指令碼完成。 雖然這個解決方案會保護資料夾中的所有檔案，但是指令碼每次只會對每個檔案執行一次。 雖然這樣所花費的時間比同時保護所有檔案 (RMS 保護工具支援) 還久，但是針對 FCI 的此逐檔案組態功能更強大。 例如，當您使用 [來源檔案擁有者電子郵件] 變數時，受保護的檔案可以有不同的擁有者 (保留原始的擁有者)，而且如果您稍後將組態變更為選擇性保護檔案而不是資料夾中的所有檔案，則需要此逐檔案的動作。

        -   **持續在新檔案上執行**：選取此核取方塊。

### 以手動方式執行規則和工作來測試組態

1.  執行分類規則：

    1.  按一下 **[分類規則]** &gt; **[以所有規則立即執行分類]**

    2.  按一下 [等待分類完成] ，然後按一下 [確定] 。

2.  等候 [正在執行分類]  對話方塊關閉，然後再檢視自動顯示報告中的結果。 您應該會在 [屬性]  欄位和資料夾中的檔案數目看到 **1** 。 使用 [檔案總管] 進行確認，並且檢查您所選擇的資料夾中的檔案屬性。 在 [分類]  索引標籤上，您應該會看到屬性名稱為 [RMS]  ，其 [值]  為 [是] 。

3.  執行檔案管理工作：

    1.  按一下 **[檔案管理工作]** &gt; **[Protect files with RMS]** [以 RMS 保護檔案] &gt; **[Run File Management Task Now]** [立即執行檔案管理工作]

    2.  按一下 [等待工作完成] ，然後按一下 [確定] 。

4.  等候 [正在執行檔案管理工作]  對話方塊關閉，然後再檢視自動顯示報告中的結果。 您應該會在 [檔案]  欄位中看到您所選擇的資料夾中的檔案數目。 確認您所選擇的資料夾中的檔案現在受到 RMS 保護。 例如，如果您選擇的資料夾是 C:\FileShare，在 Windows PowerShell 工作階段中輸入下列項目，並確認沒有任何檔案具有 [未受保護] 狀態：

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP] 疑難排解秘訣：
    > 
    > -   如果您在報告中看到 **0** ，而不是資料夾中的檔案數目，這表示指令碼並未執行。 首先，檢查指令碼本身，方法是在 Windows PowerShell ISE 中載入指令碼以驗證指令碼內容，並嘗試執行以查看是否顯示任何錯誤。 不指定任何引數時，指令碼會嘗試連接和驗證至 Azure RMS。
    > 
    >     -   如果指令碼報告它無法連接至 Azure RMS，請檢查它針對服務主體帳戶顯示的值，這是您在指令碼中指定的值。  如需有關如何建立此服務主體帳戶的詳細資訊，請參閱 [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)中的第二個必要條件
    >     -   如果指令碼報告無法連線至 Azure RMS，接下來直接從伺服器上的 Windows PowerShell 執行 [Get-RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx)，確認它可以找到指定的範本。 您應該會看到結果中傳回指定的範本。
    > -   如果在 Windows PowerShell ISE 中執行的指令碼本身沒有錯誤，請嘗試如下所示從 PowerShell 工作階段執行它，指定要保護的檔案名稱而不指定 -OwnerEmail 參數：
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   如果指令碼在此 Windows PowerShell 工作階段中成功執行，請在檔案管理工作動作中檢查 [執行]  和 [引數]  的項目。  如果您已經指定 [-OwnerEmail [來源檔案擁有者電子郵件]]，請嘗試移除此參數。
    > 
    >         如果在沒有 [-OwnerEmail [來源檔案擁有者電子郵件]] 的情況下成功運作檔案管理工作，請檢查未受保護的檔案是否具有列為檔案擁有者而非 [SYSTEM] 的網域使用者。  若要做到這一點，請使用檔案屬性的 [安全] 索引標籤，然後按一下[進階]。 在檔案 [名稱] 之後，會立即顯示 [擁有者] 值。 同時，也會驗證檔案伺服器是否位於相同的網域或信任的網域中，以從 Active Directory 網域服務查閱使用者的電子郵件地址。
    > -   如果您在報告中看到正確的檔案數目，但是檔案未受保護，請嘗試使用 [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) Cmdlet 以手動方式保護檔案，來查看是否顯示任何錯誤。

當你確認這些工作已成功執行時，您可以關閉 [檔案資源管理器]。 新檔案將自動受到保護，而且所有檔案將在排程執行時再次受到保護。 重新保護檔案可確保對範本所做的任何變更都會套用至檔案。


## 修改指示以選擇性保護檔案
當前述的指示運作時，很容易就能加以修改，以便設定更複雜的組態。 例如，使用相同指令碼但是只針對包含個人識別資訊的檔案來保護檔案，並且也許選取具有更嚴格權限的範本。

若要這樣做，請使用其中一個內建分類屬性 (例如，**個人識別資訊**) 或建立您自己的新屬性。 然後建立使用這個屬性的新規則。 例如，您可能會選取 [內容分類器] ，選擇 [個人識別資訊]  屬性，其值是 [高] ，並且設定字串或運算式模式，識別要針對此屬性設定的檔案 (例如字串「**出生日期**」)。

現在您只需要建立新的檔案管理工作，它會使用相同指令碼但是或許會使用不同的範本，以及設定您剛才設定的分類屬性的條件。 例如，不是我們先前設定的條件 ([RMS] 屬性、[等於] 、[是] )，選取 [個人識別資訊]  屬性，[運算子]  值設為 [等於]  且 [值]  為 [高] 。



<!--HONumber=Jun16_HO2-->


