---
title: MSSQLSERVER_10519 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e23a11e1fdd2bef3e9fe646ad2b5e59d1aa03456
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068268"
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10519|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Meldungstext|Die Planhinweisliste „%.\*ls“ kann nicht erstellt werden, weil die in **@hints** festgelegten Hinweise nicht auf die mit **@stmt** oder **@statement_start_offset** angegebene Anweisung angewendet werden können. Vergewissern Sie sich, dass die Hinweise auf die Anweisung angewendet werden können.|  
  
## <a name="explanation"></a>Erklärung  
Die in **@hints** festgelegten Hinweise können nicht auf die mit **@stmt** oder **@statement_start_offset** angegebene Anweisung angewendet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Legen Sie Hinweise fest, die auf die Anweisung angewendet werden können.  
  
## <a name="see-also"></a>Weitere Informationen  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
