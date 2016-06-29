---
# required metadata

title: 產生和傳輸您的租用戶金鑰 – 親自轉交 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 產生和傳輸您的租用戶金鑰 – 親自轉交

*適用於︰Azure Rights Management、Office 365*


若您決定[管理自己的租用戶金鑰](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-)而且不想透過網際網路傳輸它，而是要親自轉交您的租用戶金鑰，請使用下列程序。

## 產生您的租用戶金鑰
若要產生您自己的租用戶金鑰，請執行下列 3 個步驟：

-   [步驟 1：使用 Thales HSM 準備工作站](#step-1-prepare-a-workstation-with-thales-hsm)

-   [步驟 2：建立安全園地](#step-2-create-a-security-world)

-   [步驟 3：建立新金鑰](#step-3-create-a-new-key)

### 步驟 1：使用 Thales HSM 準備工作站
在 Windows 電腦上安裝 nCipher (Thales) 支援軟體。 將 Thales HSM 附加至該電腦。 確定 Thales 工具位於您的路徑。 如需詳細資訊，請參閱 Thales HSM 隨附的使用者指南，或造訪 Azure RMS 的 Thales 網站，網址為 [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### 步驟 2：建立安全園地
啟動命令提示字元並執行 Thales new-world 程式。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
此程式會在 %NFAST_KMDATA%\local\world 中建立與 C:\ProgramData\nCipher\Key Management Data\local 資料夾對應的**安全園地**檔案。 您可為仲裁使用不同值，但在我們的範例中，系統會提示您為每個值輸入三張卡片和 Pin 碼。 接著，會將安全園地的完整存取權授予任兩張卡片。  這些卡片將成為新安全園地的 **系統管理員卡組** 。

然後執行下列動作：

1.  依照 Thales 文件的說明安裝 Thales CNG 提供者，並進行設定以使用新安全園地。

2.  備份園地檔案。 保護園地檔案、系統管理員卡及其 Pin 碼，並確定沒有一個人可存取多張卡。

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
cngimport --import –M --key=contosokey --appname=simple contosokey
```
執行此命令時，請使用下列指示：

-   以指定於步驟 1 中的相同值取代 *contosokey* 。

-   使用 **-M** 選項，使金鑰適用於此案例。 若未執行此動作，導出的金鑰將是目前使用者的使用者特定金鑰。

此命令會在您的 %NFAST_KMDATA%\local 資料夾中建立信號化金鑰檔案，檔案名稱的開頭為 **key_caping_`_`**，後面接著 SID。 例如：**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**。 此檔案包含加密的金鑰。

在安全的位置備份此信號化金鑰檔案。

> [!IMPORTANT]
> 稍後將金鑰傳輸至 Azure RMS 時，Microsoft 將具有您的金鑰複本，而且無法復原。 這表示沒有任何人可從 Microsoft 上的 HSM 擷取您的金鑰。 如此可讓您保有租用戶金鑰的專有控制權。 因此安全地備份您的金鑰及安全園地是極為重要的動作。 如需備份金鑰的指引及最佳作法，請連絡 Thales。

您現在準備好將租用戶金鑰傳輸至 Azure RMS。

## 將租用戶金鑰傳輸至 Azure RMS
產生您自己的金鑰後，必須先將它傳輸至 Azure RMS 再進行使用。 如需最高等級的安全性，您必須飛抵美國華盛頓州雷德蒙德的 Microsoft 辦事處以手動執行轉交程序。 若要完成此程序，請執行下列 3 個步驟：

-   [步驟 1：將您的金鑰帶到 Microsoft](#step-1-bring-your-key-to-microsoft)

-   [步驟 2：將您的金鑰傳輸至 Azure RMS 安全園地](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [步驟 3：關閉程序](#step-3-closing-procedures)

### 步驟 1：將您的金鑰帶到 Microsoft

-   連絡 Microsoft 客戶支援服務 (CSS) 來安排 Azure RMS 金鑰轉交事宜。 將下列物品攜至雷德蒙德的 Microsoft：

    -   系統管理卡的仲裁。 若您遵循[步驟 2：建立安全園地](#step-2-create-a-security-world)的前述指示，則為您三張卡片的任兩張。

    -   獲授權攜帶您的系統管理卡和 Pin 碼的人員，通常是兩人 (一人一張卡片)。

    -   您在 USB 磁碟機中的安全園地檔案 (%NFAST_KMDATA%\local\world)。

    -   您在 USB 磁碟機中的信號化金鑰檔案。

### 步驟 2：將您的金鑰傳輸至 Azure RMS 安全園地

1.  當您抵達 Microsoft 轉交您的金鑰時，會發生下列情況：

    -   Microsoft 提供您已連接 Thales HSM、已安裝 Thales 軟體，並已將 Azure RMS 安全園地檔案預先載入至 C:\Temp\Destination 資料夾的離線工作站。

    -   在此工作站上，您會將安全園地檔案和信號化金鑰檔案從您的 USB 磁碟機載入至 C:\Temp\Source 資料夾。

    -   Azure RMS 操作員會使用 Thales 公用程式，將您的金鑰安全地傳輸至 Azure RMS 安全園地。

    此程序與下列程序類似，在此範例中，會以您的信號化金鑰檔案名稱取代 key-xfer-im 的最後一個參數：

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram 將要求您和 Azure RMS 操作員插入其相對的系統管理員卡和 Pin 碼。 這些命令會在 C:\Temp\Destination 中輸出信號化金鑰檔案，包含您受 Azure RMS 安全園地所保護的金鑰。

### 步驟 3：關閉程序

-   Azure RMS 操作員會在您在場的情況下執行下列工作：

    -   執行 Microsoft 與 Thales 合作開發的工具，該工具會移除兩個權限：用來復原金鑰的權限，及用來變更權限的權限。 完成此動作後，會將此金鑰複本鎖定至 Azure RMS 安全園地。 Thales HSM 不會允許 Azure RM 操作員使用其系統管理員卡來復原您金鑰的純文字複本。

    -   將導出的金鑰檔案複製至 USB 磁碟機，於稍後上傳至 Azure RMS 服務。

    -   原廠會重設 HSM，並完全清理工作站。

您現在已完成親自轉交您自己金鑰所需的指示，並可回到您的組織執行接下來的步驟來規劃與實作您的租用戶金鑰。

> [!div class="button"]
[後續步驟 >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Apr16_HO4-->


