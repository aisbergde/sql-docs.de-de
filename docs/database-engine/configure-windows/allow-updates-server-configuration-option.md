---
title: Updates zulassen (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3cccccebcbbd9054752aa8aa4e65f3f2bc17b342
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013147"
---
# <a name="allow-updates-server-configuration-option"></a>Updates zulassen (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Diese Option ist in der gespeicherten Prozedur **sp_configure** weiterhin vorhanden, obwohl ihre Funktionalität nicht in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zur Verfügung steht. (Die Einstellung hat keine Auswirkungen.) Für Systemtabellen werden keine direkten Updates unterstützt.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Wird die Option **Updates zulassen** geändert, führt dies zu einem Fehler bei der RECONFIGURE-Anweisung. Änderungen an der Option **Updates zulassen** sollten aus allen Skripts entfernt werden.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
