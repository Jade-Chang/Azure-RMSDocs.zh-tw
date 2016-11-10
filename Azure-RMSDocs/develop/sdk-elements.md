---
title: "開發環境檔案 | Azure RMS"
description: "本主題說明開發環境檔案和其在您電腦上的相對安裝位置。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4e96ba043584c5d8c140d6804c72cf63362f58c5
ms.openlocfilehash: a251723b6c42058091d57067724e89a1816bcaa1


---

# 開發環境檔案

本主題說明開發環境檔案和其在您電腦上的相對安裝位置。

Rights Management Services SDK 2.1 包含下列檔案，皆安裝在您電腦上的預設位置或您指定安裝的位置：%MsipcSDKDir%。

|檔案|路徑|描述|
|----|----|-----------|
|ReadMe.htm| \ | 包含連至 RMS 說明和[版本資訊](release-notes-rtm.md)的連結。|
|Isvtier5appsigningprivkey.dat|\bin|包含私密金鑰，此金鑰用來產生「具 RMS 功能的應用程式」開發期間所使用的資訊清單。|
|Isvtier5appsigningpubkey.dat|\bin|包含公開金鑰，此金鑰用來產生「具 RMS 功能的應用程式」開發期間所使用的資訊清單。|
|Isvtier5appsignsdk_client.xml|\bin|用來產生「具 RMS 功能的應用程式」開發期間所使用的資訊清單。|
|YourAppName.isv.mcf|\bin|重複使用的資訊清單設定檔，可用來產生「具 RMS 功能的應用程式」開發期間所使用的資訊清單。|
|Ipcsecproc_isv.dll|\bin\x86|內部使用的 DLL，適用於 x86 應用程式，Active Directory Rights Management Services Client 2.1 在 ISV 階層中運作時會使用。|
|Ipcsecproc_ssp_isv.dll|\bin\x86|內部使用的 DLL，適用於 x86 應用程式，AD RMS 2.1 在 ISV 階層中運作時會使用。|
|Ipcsecproc_isv.dll|\bin\x64|內部使用的 DLL，適用於 x64 應用程式，AD RMS Client 2.1 在 ISV 階層中運作時會使用。|
|Ipcsecproc_ssp_isv.dll|\bin\x64|內部使用的 DLL，適用於 x64 應用程式，AD RMS Client 2.1 在 ISV 階層中運作時會使用。|
|Msipc.h|\inc|RMS SDK 2.1 的主要包含檔。|
|Ipcprot.h|\inc|包含 RMS SDK 2.1 匯出的公用介面。|
|Ipcbase.h|\inc|包含 RMS SDK 2.1 匯出的基本類型和 協助程式。|
|Ipcerror.h|\inc|包含 RMS SDK 2.1 匯出的公用錯誤碼。|
|Ipcfile.h|\inc|包含 RMS SDK 2.1 匯出的檔案 API 介面。|
|Msipc.lib|\lib|當使用 RMS SDK 2.1 建置 x86 應用程式時要連結的程式庫。|
|Msipc_s.lib|\lib|提供 x86 應用程式的 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 進入點。|
|Msipc.lib|\lib\x64|當使用 RMS SDK 2.1 建置 x64 應用程式時要連結的程式庫。|
|Msipc_s.lib|\lib\x64|提供 x64 應用程式的 [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) 進入點。|
|Genmanifest.exe|\tools|產生「具 RMS 功能的應用程式」開發期間所使用的資訊清單。|
 

 

 



<!--HONumber=Oct16_HO3-->


