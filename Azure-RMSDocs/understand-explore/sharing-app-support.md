---
# required metadata

title: 適用於 Windows 和行動平台的 RMS 共用應用程式 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# 適用於 Windows 和行動平台的 RMS 共用應用程式
RMS 共用應用程式是一個免費、可下載的應用程式，這是支援 Office 2010 的必要應用程式，也建議在 Windows 電腦、Mac 電腦和行動裝置上使用。 它的其中一個好處就是可以針對原本不支援 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的應用程式和檔案套用一般保護，也就是說可以保護所有檔案。 如需不同保護層級的詳細資訊，請參閱《[Rights Management 共用應用程式系統管理員指南](../rms-client/sharing-app-admin-guide.md)》中的[保護層級 – 原生和一般](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)一節。

使用者使用 RMS 共用應用程式保護檔案時，可以同時追蹤他們所保護的文件，而且可以撤銷對檔案的存取權 (如有必要)。 使用 [文件追蹤網站](http://go.microsoft.com/fwlink/?LinkId=529562)便可以這麼做。

對 Windows 電腦來說，RMS 共用應用程式會暗中與使用者已使用的應用程式整合並增強那些應用程式：

-   會安裝一個適用於 Word、Excel、PowerPoint 及 Outlook 的 Office 增益集。 這可在功能區上為使用者提供 [共用保護] 按鈕，這個按鈕會叫用一個易於使用的對話方塊，其中包含用於保護通過電子郵件傳送之檔案的最常用設定。 使用這個按鈕還可以快速存取文件追蹤網站。

-   一個新的檔案總管滑鼠右鍵選項。 這可為使用者提供 [就地保護] 選項，這個選項會叫用一個易於使用的對話方塊，其中包含用於保護儲存在磁碟上之檔案的最常用設定。

-   一個可開啟已受 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 保護之檔案的檢視器。 當沒有安裝任何其他可開啟受保護檔案的應用程式時，便會自動叫用這個檢視器。

-   可讓來自 Office 2010 套件的 Word、Excel、PowerPoint 及 Outlook 與 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] 一起順暢運作的 Office 2010 後端設定。

雖然您可以使用 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)來針對單一電腦下載及安裝適用於 Windows 的 RMS 共用應用程式，不過它也支援透過企業部署來進行無訊息安裝和自訂設定。 如需詳細資訊，請參閱下列資源：

-   [Rights Management 共用應用程式系統管理員指南 (英文)](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共用應用程式使用者指南 (英文)](../rms-client/sharing-app-user-guide.md)

適用於行動裝置的 RMS 共用應用程式支援最常用的行動裝置，例如 iPad 和 iPhone、Android、Windows Phone 及 Windows RT。 使用者可以從相關的市集下載這個應用程式，從 [Microsoft Rights Management 頁面](http://go.microsoft.com/fwlink/?LinkId=303970)即可取得這些相關連結。

如果您有 Microsoft Intune：由於 RMS 共用應用程式包括 Microsoft Intune 應用程式軟體開發套件，因此您可以使用下列選項︰

-   部署及管理已由 Intune 註冊的 iOS 和 Android 裝置適用的應用程式。

-   管理未由 Intune 註冊的 Android 裝置的應用程式。


## 後續步驟
若要查看其他應用程式和服務如何支援 Azure Rights Management，請參閱[應用程式如何支援 Azure Rights Management](applications-support.md)。



<!--HONumber=Apr16_HO3-->


