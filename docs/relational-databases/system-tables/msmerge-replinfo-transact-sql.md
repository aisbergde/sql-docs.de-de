---
title: MSmerge_replinfo (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 045f9ab13b701b8dbd5e0895531932c21767853f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909058"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_replinfo** -Tabelle enthält eine Zeile für jedes Abonnement. In dieser Tabelle werden Informationen zu Abonnements nachverfolgt. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|Die eindeutige ID für das Replikat.|  
|**use_interactive_resolver**|**bit**|Gibt an, ob der interaktive Konfliktlöser während der Abgleichung verwendet wird.<br /><br /> **0** = es wird den interaktiven Konfliktlöser nicht verwendet.<br /><br /> **1** = Verwendung des interaktiven Konfliktlösers.|  
|**validation_level**|**int**|Überprüfungstyp, der für das Abonnement durchgeführt wird. Die angegebene Überprüfungsebene kann einen der folgenden Werte haben:<br /><br /> **0** = keine Überprüfung.<br /><br /> **1** = nur Überprüfung der Zeilenanzahl.<br /><br /> **2** = Überprüfung der Zeilenanzahl und Prüfsumme.<br /><br /> **3** = Überprüfung der Zeilenzählung und binären Prüfsumme.|  
|**resync_gen**|**bigint**|Die Generierungsnummer, die für die erneute Synchronisierung des Abonnements verwendet wird. Der Wert **-1** gibt an, dass das Abonnement nicht für die erneute Synchronisierung markiert ist.|  
|**login_name**|**sysname**|Der Name des Benutzers, der das Abonnement erstellt hat.|  
|**hostname**|**sysname**|Der Wert, der beim Generieren der Partition für das Abonnement von den parametrisierten Zeilenfiltern verwendet wird.|  
|**der Standard**|**binary(16)**|Die ID des Mergeauftrags für dieses Abonnement.|  
|**sync_info**|**int**|Intern-nur zur Verwendung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
