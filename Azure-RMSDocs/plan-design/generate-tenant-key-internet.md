---
# required metadata

title: 產生並傳輸您的租用戶金鑰 – 透過網際網路 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 產生並傳輸您的租用戶金鑰 – 透過網際網路

*適用於︰Azure Rights Management、Office 365*

若您決定要[管理您自己的租用戶金鑰](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-)，並透過網際網路傳輸金鑰，而非至 Microsoft 機構親自轉交租用戶金鑰，請使用下列程序：


## 準備連線網際網路的工作站
若要準備連線至網際網路的工作站，請執行以下 3 個步驟：

-   [步驟 1：安裝 Azure Rights Management 的 Windows PowerShell](#step-1-install-windows-powershell-for-azure-rights-management)

-   [步驟 2：取得您的 Azure Active Directory 租用戶識別碼](#step-2-get-your-azure-active-directory-tenant-id)

-   [步驟 3：下載 BYOK 工具組](#step-3-download-the-byok-toolset)

### 步驟 1：安裝 Azure Rights Management 的 Windows PowerShell
從連線網際網路的工作站，下載並安裝 Azure Rights Management 的 Windows PowerShell 模組。

> [!NOTE]
> 如果您先前已下載此 Windows PowerShell 模組，請執行下列命令來檢查版本號碼至少為 2.1.0.0： `(Get-Module aadrm -ListAvailable).Version`

如需安裝指示，請參閱 [安裝 Windows PowerShell for Azure Rights Management](../deploy-use/install-powershell.md)。.

### 步驟 2：取得您的 Azure Active Directory 租用戶識別碼
使用 [ **以系統管理員身分執行** ] 選項啟動 Windows PowerShell，然後執行下列命令：

-   使用 [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) 指令程式來連線 Azure RMS 服務：

    ```
    Connect-AadrmService
    ```
    出現提示時，輸入您的 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 租用戶系統管理員認證 (通常需要使用 Azure Active Directory 或 Office 365 的全域系統管理員帳戶)。

-   使用 [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 指令程式來顯示租用戶的設定：

    ```
    Get-AadrmConfiguration
    ```
    從輸出中，儲存第一行的 GUID (BPOSId)。 這是您的 Azure Active Directory 租用戶識別碼，您於稍後準備上傳租用戶金鑰時會用到。

-   使用 [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) 指令程式來中斷連線 Azure RMS 服務，直到準備好上傳金鑰為止：

    ```
    Disconnect-AadrmService
    ```

請勿關閉 Windows PowerShell 視窗。

### 步驟 3：下載 BYOK 工具組
移至 Microsoft 下載中心，並 [下載您地區的 BYOK 工具組](http://go.microsoft.com/fwlink/?LinkId=335781) ：

|地區|封裝名稱|
|----------|----------------|
|北美|AzureRMS-BYOK-tools-UnitedStates.zip|
|歐洲|AzureRMS-BYOK-tools-Europe.zip|
|亞洲|AzureRMS-BYOK-tools-AsiaPacific.zip|
工具組包含下列組件：

-   名稱開頭為 **BYOK-KEK-pkg-** 的金鑰互換 (KEK) 封裝.

-   名稱開頭為 **BYOK-SecurityWorld-pkg-** 的安全園地封裝.

-   名為 **verifykeypackage.py** 的 Python 指令碼.

-   名為 **KeyTransferRemote.exe** 的命令列可執行檔、名為 **KeyTransferRemote.exe.config** 的中繼資料檔案，以及相關聯的 DLL。

-   名為 **vcredist_x64.exe** 的 Visual C++ 可轉散發套件.

將封裝複製到 USB 磁碟機或其他可攜式儲存裝置。

## 準備中斷連線的工作站
若要準備未連線至網路 (網際網路或您的內部網路) 的工作站，請執行以下 2 個步驟：

-   [步驟 1：使用 Thales HSM 準備中斷連線的工作站](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [步驟 2：在中斷連線的工作站上安裝 BYOK 工具組](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### 步驟 1：使用 Thales HSM 準備中斷連線的工作站
在中斷連線的工作站，於 Windows 電腦上安裝 nCipher (Thales) 支援軟體，然後將 Thales HSM 連接至該電腦。

確定 Thales 工具位於您的路徑 **(%nfast_home%\bin** 和 **%nfast_home%\python\bin**) 中。 例如，鍵入下列命令：

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
如需詳細資訊，請參閱 Thales HSM 隨附的使用者指南，或造訪 Azure RMS 的 Thales 網站，網址為 [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### 步驟 2：在中斷連線的工作站上安裝 BYOK 工具組
從 USB 磁碟機或其他可攜式儲存裝置中複製 BYOK 工具組封裝，然後執行下列動作：

1.  從下載的封裝中將檔案解壓縮至任何資料夾。

2.  從該資料夾中執行 vcredist_x64.exe。

3.  依照指示安裝 Visual Studio 2012 的 Visual C++ 執行階段元件。

## 產生您的租用戶金鑰
在中斷連線的工作站上，執行下列 3 個步驟以產生您自己的租用戶金鑰：

-   [步驟 1：建立安全園地](#step-1-create-a-security-world)

-   [步驟 2：驗證下載的封裝](#step-2-validate-the-downloaded-package)

-   [步驟 3：建立新金鑰](#step-3-create-a-new-key)

### 步驟 1：建立安全園地
啟動命令提示字元並執行 Thales new-world 程式。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
此程式會在 %NFAST_KMDATA%\local\world 中建立與 C:\ProgramData\nCipher\Key Management Data\local 資料夾對應的**安全園地**檔案。 您可為仲裁使用不同值，但在我們的範例中，系統會提示您為每個值輸入三張卡片和 Pin 碼。 然後，任兩張卡片必須具有系統管理權限來存取安全園地 (您指定的仲裁)。  這些卡片將成為新安全園地的 **系統管理員卡組** 。 在這個階段，您可以為每一張 ACS 卡片指定密碼或 PIN，或稍後以命令來新增。

> [!TIP]
> 您可以使用 `nkminfo` 命令，確認您 HSM 的目前組態狀態。

然後執行下列動作：

1.  依照 Thales 文件的說明安裝 Thales CNG 提供者，並進行設定以使用新安全園地。

2.  備份 **%nfast_kmdata%\local** 中的園地檔案。 保護園地檔案、系統管理員卡及其 Pin 碼，並確定沒有一個人可存取多張卡。

### 步驟 2：驗證下載的封裝
這是選用性步驟，但建議您使用以驗證下列情況：

-   已從正版 Thales HSM 中產生工具組所包含的「金鑰互換」。

-   已在正版 Thales HSM 中產生工具組中包含的「Azure RMS 安全園地」雜湊。

-   金鑰互換無法匯出。

> [!NOTE]
> 若要驗證下載的封裝，必須連接 HSM 並開機，且必須具有安全園地 (如您剛才建立的一個安全園地)。

#### 若要驗證下載的封裝

1.  依據您的地區輸入下列一項，以執行 verifykeypackage.py 指令碼：

    -   適用於北美：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   適用於歐洲：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   適用於亞洲：

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Thales 軟體包含 Python 解釋器，位於 %NFAST_HOME%\python\bin

2.  確認看到下列表示成功驗證的結果： **結果：成功**

此指令碼會驗證簽章者鏈結，最高至 Thales 根金鑰。 此根金鑰的雜湊內嵌於指令碼中，且其值必須為 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**。 您亦可造訪 [Thales 網站](http://www.thalesesec.com/)，個別確認此值.

您現在準備建立新金鑰，它將是您的 RMS 租用戶金鑰。

### 步驟 3：建立新金鑰
使用 Thales **generatekey** 和 **cngimport** 程式來產生 CNG 金鑰。

執行下列命令以產生金鑰：

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
執行此命令時，請使用下列指示：

-   參數 **protect** 必須設定為值 **module**，如此處所示。 這會建立模組保護的金鑰。 BYOK 工具組不支援 OCS 保護的金鑰。

-   對於金鑰大小，我們建議設為 2048，但對於擁有此類金鑰並正在移轉至 Azure RMS 的現有 AD RMS 客戶，也支援 1024 位元 RSA 金鑰。

-   以任何字串值取代 *ident* 和 **plainname** 的 **contosokey** 值。 為了盡可能降低系統管理負擔並降低錯誤風險．我們建議您對二者使用相同值，並全部使用小寫字元。

-   此範例中的 pubexp 保留空白 (預設值)，但您可以指定特定值。 如需詳細資訊，請參閱 Thales 文件。

接著執行下列命令，將金鑰匯入至 CNG：

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
執行此命令時，請使用下列指示：

-   以*產生您的租用戶金鑰*一節的[步驟 1：建立安全園地](#step-1-create-a-security-world)中指定的相同值來取代 *contosokey*。

-   使用 **-M** 選項，使金鑰適用於此案例。 若未執行此動作，導出的金鑰將是目前使用者的使用者特定金鑰。

-   **appname** 選項是金鑰檔中報告的應用程式名稱。 如果您使用這些指示來建立新的金鑰，我們會使用命令中所示的簡單值。 不過，如果您要將 AD RMS 移轉的現有受 HSM 保護金鑰移轉到 Azure RMS，請在此命令中指定您的現有名稱，若後續命令也使用 appname 選項，也請指定現有名稱。

此命令會在您的 %NFAST_KMDATA%\local 資料夾中建立信號化金鑰檔案，檔案名稱的開頭為 **key_caping_`_`**，後面接著 SID。 例如：**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**。 此檔案包含加密的金鑰。

> [!TIP]
> 您可以使用 `nkminfo –k` 命令，查看您金鑰的目前組態狀態。

在安全的位置備份此信號化金鑰檔案。

> [!IMPORTANT]
> 當您稍後將金鑰傳輸至 Azure RMS 時，Microsoft 無法將此金鑰回傳給您，因此請務必安全地備份您的金鑰和安全園地。 如需備份金鑰的指引及最佳作法，請連絡 Thales。

您現在準備好將租用戶金鑰傳輸至 Azure RMS。

## 準備您的租用戶金鑰進行傳輸
在中斷連線的工作站上，執行下列 4 個步驟以準備您自己的租用戶金鑰：

-   [步驟 1：以降低的權限建立金鑰複本](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [步驟 2：檢查金鑰的新複本](#step-2-inspect-the-new-copy-of-the-key)

-   [步驟 3：使用 Microsoft 的金鑰互換來加密您的金鑰](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [步驟 4：將您的金鑰傳輸封裝複製至連線網際網路的工作站](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### 步驟 1：以降低的權限建立金鑰複本
若要降低租用戶金鑰上的權限，請執行下列動作：

-   視您的地區而定，從命令提示字元執行下列其中一項：

    -   適用於北美：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   適用於歐洲：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   適用於亞洲：

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

當您執行此命令時，以*產生您的租用戶金鑰*一節的[步驟 1：建立安全園地](##step-1-create-a-security-world)中指定的相同值來取代 *contosokey*。

系統會要求您插入安全園地 ACS 卡片，並詢問其密碼或 PIN (如果指定的話)。

命令完成時，您會看到 **[結果: 成功]**，並將在名為 key_xferacId_*&lt;contosokey&gt;* 的檔案中看到降低權限的租用戶金鑰複本.

### 步驟 2：檢查金鑰的新複本
選擇性執行 Thales 公用程式來確認新租用戶金鑰上的最低權限：

-   aclprint.py：

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe：

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

當您執行這些命令時，以*產生您的租用戶金鑰*一節的[步驟 1：建立安全園地](##step-1-create-a-security-world)中指定的相同值來取代 *contosokey*。

### 步驟 3：使用 Microsoft 的金鑰互換來加密您的金鑰
視您的地區而定，執行下列其中一個命令：

-   適用於北美：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   適用於歐洲：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   適用於亞洲：

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

執行此命令時，請使用下列指示：

-   以*產生您的租用戶金鑰*一節的[步驟 1：建立安全園地](##step-1-create-a-security-world)中用來產生金鑰的識別碼來取代 *contosokey*。

-   以您在*準備連線網際網路的工作站*一節的[步驟 2：取得您的 Azure Active Directory 租用戶識別碼](#step-2-get-your-azure-active-directory-tenant-id)中所擷取 Azure Active Directory 租用戶識別碼來取代 *GUID*。

-   以將用於輸出檔案名稱的標籤來取代 *ContosoFirstKey* 。

成功完成時會顯示**結果︰成功**，而且在目前資料夾中會有下列名稱的新檔案︰TransferPackage-*ContosoFirstkey*.byok。

### 步驟 4：將您的金鑰傳輸封裝複製至連線網際網路的工作站
使用 USB 磁碟機或其他可攜式儲存裝置，將輸出檔案從上一個步驟 (KeyTransferPackage-*ContosoFirstkey*.byok) 複製到連線網際網路的工作站。

> [!NOTE]
> 安全性作法可用來保護檔案，因為其中包含您的私密金鑰。

## 將租用戶金鑰傳輸至 Azure RMS
在連線網際網路的工作站上，執行下列 3 個步驟將新租用戶金鑰傳輸至 Azure RMS：

-   [步驟 1：連線至 Azure RMS](#step-1-connect-to-azure-rms)

-   [步驟 2：上傳金鑰封裝](#step-2-upload-the-key-package)

-   [步驟 3：列舉您的租用戶金鑰 - 視需要](#step-3-enumerate-your-tenant-keys-as-needed)

### 步驟 1：連線至 Azure RMS
返回 Windows PowerShell 視窗並鍵入下列命令：

1.  重新連線至 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 服務：

    ```
    Connect-AadrmService
    ```

2.  使用 [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) 指令程式來查看目前的租用戶金鑰設定：

    ```
    Get-AadrmKeys
    ```

### 步驟 2：上傳金鑰封裝
使用 [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) 指令程式，上傳從中斷連線的工作站中複製的金鑰傳輸封裝：

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> 系統會提示您確認此動作。 請務必瞭解此動作是無法還原的。 當您上傳租用戶金鑰時，它會自動成為您組織的主要租用戶金鑰，且使用者在保護文件和檔案時將開始使用此租用戶金鑰。

若上傳成功，您會看到下列訊息： **Rights Management 服務已成功新增金鑰。**

將變更傳播到所有 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 資料中心時預期會發生複寫延遲。

### 步驟 3：列舉您的租用戶金鑰 - 視需要
再次使用 Get-AadrmKeys 指令程式來查看租用戶金鑰中的變更，並查看您的租用戶金鑰清單。 隨即顯示租用戶金鑰，包含 Microsoft 為您產生的初始租用戶金鑰，及您新增的任何租用戶金鑰：

```
Get-AadrmKeys
```
標示為 [ **作用中** ] 的租用戶金鑰是您組織目前用來保護文件和檔案的金鑰。

您現在已完成透過網際網路整合您自己金鑰的所有必要步驟，可移至後續步驟開始規劃及實作您的租用戶金鑰。


> [!div class="button"]
[後續步驟 >>](plan-implement-tenant-key.md#next-steps)




<!--HONumber=Apr16_HO4-->


