---
title: "透過使用 Rights Management 共用應用程式從檔案移除保護 | Azure Information Protection"
description: "將先前使用 RMS 共用應用程式保護的檔案移除保護 (也就是將檔案解除保護) 的指示。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 3ef47e5dea1c6b56127e231ba6dba774c31cca90


---

# <a name="remove-protection-from-a-file-by-using-the-rights-management-sharing-application"></a>透過使用 Rights Management 共用應用程式從檔案移除保護

>*適用對象︰Active Directory Rights Management Services、Azure Information Protection、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

若要從先前使用 RMS 共用應用程式保護的檔案移除保護 (也就是取消保護檔案)，請從 [檔案總管] 使用 [ **移除保護** ] 選項。

> [!IMPORTANT]
> 您必須是檔案的擁有者才能移除保護。

## <a name="to-remove-protection-from-a-file"></a>從檔案移除保護

1.  在 [檔案總管] 中以滑鼠右鍵按一下檔案 (例如 Sample.ptxt)，選取 [以 RMS 保護]，按一下 [就地保護]，然後按一下 [移除保護]：

    ![移除 RMS 共用應用程式的 [保護] 功能表選項](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    系統不會提示您提供認證。

注意：如果您看不到這些選項，可能是您的電腦上未安裝 RMS 共用應用程式、未安裝最新版本，或您的電腦必須重新啟動以完成安裝。 如需如何安裝共用應用程式的詳細資訊，請參閱[下載及安裝 Rights Management 共用應用程式](install-sharing-app.md)。

原始受保護的檔案會遭到刪除 (例如，Sample.ptxt)，而且取代為具有相同名稱但沒有受保護副檔名的檔案 (例如，Sample.txt)。

## <a name="examples-and-other-instructions"></a>範例和其他指示
如需 Rights Management 共用應用程式的使用範例及作法指示，請參閱 Rights Management 共用應用程式使用者指南中下列各節：

-   [使用 RMS 共用應用程式的範例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [您想要做什麼？](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>另請參閱
[Rights Management 共用應用程式使用者指南 (英文)](sharing-app-user-guide.md)



<!--HONumber=Nov16_HO2-->


