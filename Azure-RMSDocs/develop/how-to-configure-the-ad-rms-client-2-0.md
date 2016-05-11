---
# required metadata

title: 設定用戶端 | Azure RMS
description: 如何設定 Active Directory Rights Management Services Client 2.1 的相關指示。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58051d42-5a0a-4b65-9e02-bcdbf17d3262

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 設定用戶端

本主題包含如何設定 Active Directory Rights Management Services Client 2.1 的相關指示。

重要：如果您要透過在 RMS ISV 整合環境上執行應用程式來測試它，您不需要設定 AD RMS Client 2.1。 如需詳細資訊，請參閱[測試具備權限的應用程式](running-your-first-application.md)。

 

### 先決條件

-   您必須在您將測試應用程式的電腦上安裝 AD RMS Client 2.1。

    -   如果您將在開發電腦上測試您的應用程式，您應該已安裝 Rights Management Services SDK 2.1。 AD RMS Client 2.1 此時會以無訊息模式安裝。

        如需如何安裝 RMS SDK 2.1 的資訊，請參閱[安裝 SDK](create-your-first-rights-aware-application.md)。

    -   如果您要在開發電腦以外的其他電腦上測試應用程式，您可以在該電腦上從 [AD RMS Client 2.1 下載頁面](http://www.microsoft.com/en-us/download/details.aspx?id=38396)安裝 AD RMS Client 2.1。
        注意：如果應用程式使用伺服器 API 模式 (IPC\_API\_MODE\_SERVER)，您不需要使用應用程式資訊清單。 您可以對生產 RMS 伺服器測試應用程式，而且不需要在切換到生產環境時取得生產授權。 如需伺服器模式應用程式的詳細資訊，請參閱[應用程式類型](application-types.md)。

         

-   您必須安裝並設定 RMS 伺服器才能在生產前環境中運作。 如需相關資訊，請參閱[安裝及設定伺服器](how-to-install-and-configure-an-rms-server.md)。

指示

### 步驟 1︰如何為生產前憑證階層設定 RMS Client 2.1

下列步驟描述如何安裝開發人員執行階段、設定用戶端以使用 ISV 憑證 (生產前) 階層，並設定用戶端上的服務探索。

1.  從 %MSIPCSDKDIR%\\bin\\x86 (適用於 32 位元版 Windows) 或 %MSIPCSDKDIR\\bin\\x64 (適用於 64 位元版 Windows) 將開發人員執行階段 Ipcsecproc\_isv.dll 複製到 C:\\Program Files\\Active Directory Rights Management Services Client 2.1。

    重要  如果您在 64 位元版 Windows 上執行 32 位元應用程式，您必須從 %MSIPCSDKDIR%\\bin\\x86 將 Ipcsecproc\_isv.dll 複製到 C:\\Program Files(x86)\\Active Directory Rights Management Services Client 2.1。

     

2.  藉由將階層 登錄機碼值設為 1，來設定 AD RMS Client 2.1 以使用 ISV 憑證 (生產前環境) 階層。

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    注意  登錄中沒有出現階層值，在功能上等於它的值設為 0 (零)，表示 RMS SDK 2.1 將會以運作模式運作。 如需金鑰和憑證鏈結的詳細資訊，請參閱[了解憑證鏈結](understanding-certificate-chains.md)。

    **重要**  
    如果您在 64 位元版 Windows 上執行 32 位元應用程式，您必須在下列機碼位置中設定階層值︰

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  設定伺服器端或用戶端探索來啟用 AD RMS Client 2.1，以探索並建立與生產前 RMS 伺服器間的通訊。

    -   在伺服器端探索中，系統管理員會向 Active Directory 登錄生產前 RMS 根叢集的服務連接點 (SCP)，而用戶端會查詢 Active Directory 以探索 SCP，並建立與伺服器之間的連線。
    -   在用戶端探索中，您可以在執行 AD RMS Client 2.1 的電腦上設定登錄中的 RMS 服務探索設定。 這些設定會將 AD RMS Client 2.1 指向要使用的 RMS 伺服器。 當其存在時，不會執行伺服器端探索。

    若要設定用戶端探索，您可以設定下列登錄機碼，以指向您的生產前 RMS 伺服器。 如需如何設定服務端探索的相關資訊，請參閱 [RMS Client 2.0 部署注意事項](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)。

|金鑰|值|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(預設)：<br><br> [http&#124;https]:// RMSClusterName /_wmcs/Certification|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(預設)：<br><br> [http&#124;https]:// RMSClusterName /_wmcs/Licensing|


注意   根據預設，這些機碼不存在登錄中，必須加以建立。
     
**重要**  
    如果您在 64 位元版 Windows 上執行 32 位元應用程式，您必須在下列機碼位置中設定這些機碼︰


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### 備註

本主題中的指引並不完整。 如需如何設定 AD RMS Client 2.1 的詳細資訊，請參閱 [RMS Client 2.0 部署注意事項](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)。

### 相關主題


* [如何使用](how-to-use-msipc.md)
* [RMS Client 2.0 部署注意事項](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [安裝 SDK](create-your-first-rights-aware-application.md)
* [安裝及設定伺服器](how-to-install-and-configure-an-rms-server.md)
* [測試具備權限的應用程式](running-your-first-application.md)
* [了解憑證鏈結](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO3-->


