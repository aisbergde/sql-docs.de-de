---
title: MSpeer_conflictdetectionconfigrequest (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2ecd4ef541422b1241689f17ab5c4f1a53bcc0a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115041"
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird in der Peer-zu-Peer-Replikation verwendet, um topologieübergreifende Konfigurationsanforderungen für eine Veröffentlichung zu verfolgen. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifiziert eine Konfliktkonfigurationsanforderung. Die Spalte Request_id in [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) verwendet diesen Wert.|  
|publication|**sysname**|Name der Veröffentlichung, aus der die Konfliktkonfigurationsanforderung stammt.|  
|sent_date|**datetime**|Datum und Uhrzeit der Initiierung der Konfliktkonfigurationsanforderung.|  
|timeout|**int**|Zeitraum, den eine Prozedur verstreichen lassen sollte, bis alle Peers Konfliktinformationen zurückgeben.|  
|modified_date|**datetime**|Datum und Uhrzeit, zu der eine Phase abgeschlossen wurde.|  
|progress_phase|**nvarchar(32)**|Identifiziert die aktuelle Phase der Verarbeitung mit einem der folgenden Werte:<br /><br /> Gestartet<br /><br /> Topologie wird durchsucht<br /><br /> Status wird erfasst<br /><br /> Status erfasst|  
|phase_timed_out|**bit**|Gibt an, ob für die aktuelle Phase ein Timeout eingetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
