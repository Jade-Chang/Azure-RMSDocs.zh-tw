---
# required metadata

title: 如何安裝和設定 RMS 伺服器以進行測試 |Azure RMS
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

# 如何：安裝和設定 RMS 伺服器以進行測試

本主題涵蓋連線到 RMS 伺服器或 Azure RMS 以測試已啟用權限應用程式的步驟。
 
## 指示

### 步驟 1︰設定您的 RMS 伺服器

下列步驟可引導您設定 RMS 伺服器而且包括︰

-   安裝伺服器
-   註冊伺服器

1.  **安裝伺服器**

    Active Directory Rights Management Services (AD RMS) 由不同的用戶端和伺服器元件所組成。 實作伺服器元件做為一組 web 服務，可用來管理 RMS 基礎結構、發行授權給內容取用者和發行者，並發行憑證至電腦和使用者。

    從 Windows Server 2008 開始，用戶端和伺服器元件都包含在作業系統中。 您可以從下列位置下載優先作業系統的伺服器元件。

    -   [RMS 伺服器 v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    若要在 Windows Server 2008 上設定伺服器元件，您必須安裝 AD RMS 角色。 如果您針對舊版伺服器作業系統開發應用程式，請在安裝 RMS 伺服器 v1.0 SP2 後、佈建 RMS 服務前設定登錄。

2.  **註冊伺服器**

    您必須註冊 Rights Management Services (RMS) 伺服器，以在生產前或生產階層中識別它。 註冊程序會將伺服器授權人憑證保留在伺服器電腦上。 此憑證會鏈結回信任的 Microsoft 根。 註冊伺服器的方式取決於您所使用的 RMS 版本。

    -   **自行註冊**

        從 Windows Server 2008 開始，您可以在適當的階層架構中註冊 RMS 伺服器，無需傳送資訊給 Microsoft。 當您安裝 RMS 角色時，也會安裝自行註冊憑證和私密金鑰。 這些內容可用來自動建立伺服器授權人憑證。 不會與 Microsoft 交換任何資訊。

    -   **線上註冊**

        如果您使用 AD RMS v1.0 SP2，可以在線上註冊伺服器。 在佈建程序期間，註冊會在幕後進行，但您必須具備網際網路連線。

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **使用 RMS 伺服器進行測試**

    若要使用 RMS 伺服器進行測試，請設定伺服器端或用戶端探索，讓 Rights Management Service Client 2.1 能夠探索並建立與 RMS 伺服器間的通訊。

    > [!Note] 不需要探索設定，就能使用 Azure RMS 進行測試。

  - 在伺服器端探索中，管理員會向 Active Directory 登錄 RMS 根叢集的服務連接點 (SCP)，而用戶端會查詢 Active Directory 以探索 SCP，並建立與伺服器之間的連線。
  - 在用戶端探索中，您可以在執行 RMS Client 2.1 的電腦上設定登錄中的 RMS 服務探索設定。 這些設定會將 RMS Client 2.1 指向要使用的 RMS 伺服器。 當其存在時，不會執行伺服器端探索。

  若要設定用戶端探索，您可以設定下列登錄機碼，以指向您的 RMS 伺服器。 如需如何設定服務端探索的相關資訊，請參閱 [RMS Client 2.0 部署注意事項](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)。

1. **EnterpriseCertification**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterpriseCertification

  **值**：(預設)：[**http|https**]://RMSClusterName/**_wmcs/Certification**

2. **EnterprisePublishing**
        HKEY_LOCAL_MACHINE        SOFTWARE          Microsoft            MSIPC              ServiceLocation                EnterprisePublishing **值**：(預設)：[**http|https**]://RMSClusterName/**_wmcs/Licensing**

>[!NOTE] 根據預設，登錄中沒有這些機碼，必須加以建立。

>[!IMPORTANT] 如果您在 64 位元版 Windows 上執行 32 位元應用程式，您必須在下列機碼位置中設定這些機碼︰<p>
  ```    
  HKEY_LOCAL_MACHINE
    SOFTWARE
      Wow6432Node
        Microsoft
          MSIPC
            ```

 

 


<!--HONumber=Jun16_HO2-->


