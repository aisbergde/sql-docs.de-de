---
title: MSSQLSERVER_3937 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4289b3e41de0e1652bd9cc033b2fab6ae8f42a60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043561"
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|MSSQLSERVER|  
|Ereignis-ID|3937|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Meldungstext|Fehler beim Benachrichtigen des FILESTREAM-Filtertreibers über das Rollback einer Transaktion. Fehlercode: 0x%0x.|  
  
## <a name="explanation"></a>Erklärung  
Beim Ausgeben einer Rollbackbenachrichtigung für eine Transaktion wurde vom RsFx-Treiber ein Fehler zurückgegeben. Dieser Fehler kann auftreten, wenn nicht genügend Ressourcen zur Verfügung stehen. Hierdurch kann ein geringfügiger Speicherverlust im RsFx-Filtertreiber entstehen, jedoch nur bis zum Ende des sqlservr.exe-Prozesses, durch den die Transaktion erstellt wurde.  
  
## <a name="user-action"></a>Benutzeraktion  
