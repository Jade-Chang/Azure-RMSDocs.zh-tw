---
# required metadata

title: 安裝及設定伺服器 | Azure RMS
description: 安裝和設定 RMS 伺服器以測試具備權限的應用程式。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** 這個 SDK 內容不是最新版本。 很快就可以在 MSDN 上找到文件的[目前版本](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)。 **
# 安裝及設定伺服器

本主題包含安裝和設定 RMS 伺服器以測試具備權限的應用程式的步驟。

**重要**：如果您要藉由在 RMS ISV 整合環境上執行應用程式來測試它，您不需要安裝 RMS 伺服器，因為已在整合環境上安裝和設定了一部。
如需 AD RMS ISV 整合環境的詳細資訊，請參閱[設定測試環境](how-to-set-up-your-test-environment.md)。

 

## 指示

### 步驟 1︰設定您的 RMS 伺服器

下列步驟可引導您設定 RMS 伺服器而且包括︰

-   設定登錄
-   安裝伺服器
-   註冊伺服器

1.  **設定登錄**

    若要指定您正在使用生產前憑證階層，請設定下列登錄值。

    **注意**：如果您使用 Windows Server 2008 R2 或 Windows Server 2008，請在安裝 AD RMS 服務之前設定登錄值。

    如果您正在 Windows Server 2008 R2 上使用 AD RMS，您必須設定下列 **REG\_DWORD** 值。 將此值變更為 0 (零)，以切換到生產階層。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    如果您正在 Windows Server 2008 R2 上使用 AD RMS，而另一個 AD RMS 服務已部署在 Active Directory 中做為生產前服務，請將下列空字串值新增至登錄。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    如果您正在 Windows Server 2008 上使用 AD RMS，您必須設定下列 **REG\_DWORD** 值。 將此值變更為 0 (零)，以切換到生產階層。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    如果您正在 Windows Server 2008 上使用 AD RMS，而另一個 AD RMS 服務已部署在 Active Directory 中做為生產前服務，請將下列空字串值新增至登錄。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **安裝伺服器**

    Active Directory Rights Management Services (AD RMS) 由不同的用戶端和伺服器元件所組成。 實作伺服器元件做為一組 web 服務，可用來管理 RMS 基礎結構、發行授權給內容取用者和發行者，並發行憑證至電腦和使用者。

    從 Windows Server 2008 開始，用戶端和伺服器元件都包含在作業系統中。 您可以從下列位置下載優先作業系統的伺服器元件。

    -   [RMS 伺服器 v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    若要在 Windows Server 2008 上設定伺服器元件，您必須安裝 AD RMS 角色。 不過在這麼做之前，您必須設定登錄以指定您將使用生產前憑證階層，而不是生產階層。 不過，如果您正針對優先伺服器作業系統開發應用程式，請在安裝 RMS 伺服器 v1.0 SP2 之後，但在佈建 RMS 服務之前設定登錄。

    如需詳細資訊，請參閱上一個步驟，也就是步驟 1 的「設定登錄」。

3.  **註冊伺服器**

    您必須註冊 Rights Management Services (RMS) 伺服器，以在生產前或生產階層中識別它。 註冊程序會將伺服器授權人憑證保留在伺服器電腦上。 此憑證會鏈結回信任的 Microsoft 根。 註冊伺服器的方式取決於您所使用的 RMS 版本。

    -   **自行註冊**

        從 Windows Server 2008 開始，您可以在適當的階層架構中註冊 RMS 伺服器，無需傳送資訊給 Microsoft。 當您安裝 RMS 角色時，也會安裝自行註冊憑證和私密金鑰。 這些內容可用來自動建立伺服器授權人憑證。 不會與 Microsoft 交換任何資訊。

    -   **線上註冊**如果您使用 AD RMS v1.0 SP2，您可以在線上註冊伺服器。 註冊會於佈建程序期間在幕後進行，但您必須具有網際網路連線，而且您必須指定適當的登錄值，以識別您在哪些階層中註冊伺服器。 若要在生產前階層中註冊，請新增下列 **REG\_SZ** 值並佈建伺服器。 若要在生產階層中註冊，請清除此值並佈建伺服器。

        如需詳細資訊，請參閱上一個步驟，也就是步驟 1 的「設定登錄」。

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## 相關主題

* [如何使用](how-to-use-msipc.md)
 

 





<!--HONumber=Jun16_HO1-->


