---
title: Sys. time_zone_info (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 69bfcbb7e1eeaf6b456a2e10d1f3bfcc581c3d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106701"
---
# <a name="systimezoneinfo-transact-sql"></a>sys.time_zone_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Gibt Informationen zu unterstützten Zeitzonen. Alle auf dem Computer installierten Zeitzonen sind in der folgenden Registrierungsstruktur gespeichert:  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Zeitzone in Windows-Standardformat. Z. B. **beispielsweise "CEN" Ostaustralische Normalzeit** oder **Mitteleuropäische Zeit**.|  
|**current_utc_offset**|**nvarchar(12)**|Der aktuelle offset zur UTC. Z. B. **+ 01:00** oder **-07: 00**.|  
|**is_currently_dst**|**bit**|True, wenn die Sommerzeit derzeit beobachten.|  
  
## <a name="see-also"></a>Siehe auch  
 [GETUTCDATE &#40;Transact-SQL&#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [Katalogsichten für die serverweite Konfiguration &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
