---
title: sys. DM _pdw_exec_requests (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 72af3975378b2450e51b3880e8814705bb514c1a
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811398"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Anforderungen, die derzeit oder vor [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]kurzem in aktiv sind. Es wird eine Zeile pro Anforderung/Abfrage aufgelistet.  
  
|Spaltenname|Datentyp|Beschreibung|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Der Schlüssel für diese Ansicht. Eindeutige numerische ID, die der Anforderung zugeordnet ist.|Eindeutig für alle Anforderungen im System.|  
|session_id|**nvarchar(32)**|Eindeutige numerische ID, die der Sitzung zugeordnet ist, in der die Abfrage ausgeführt wurde. Weitere Informationen finden Sie unter [sys. DM &#40;_pdw_exec_sessions&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Aktueller Status der Anforderung.|"Wird ausgeführt", "angehalten", "abgeschlossen", "abgebrochen", "fehlerhaft".|  
|submit_time|**datetime**|Der Zeitpunkt, zu dem die Anforderung zur Ausführung übermittelt wurde.|Gültiger **DateTime** -Wert, der kleiner oder gleich der aktuellen Uhrzeit und start_time ist.|  
|start_time|**datetime**|Der Zeitpunkt, zu dem die Ausführung der Anforderung gestartet wurde.|NULL bei Anforderungen in der Warteschlange; Andernfalls ist ein gültiger **DateTime** -Wert kleiner oder gleich der aktuellen Zeit.|  
|end_compile_time|**datetime**|Der Zeitpunkt, zu dem die Engine das Kompilieren der Anforderung abgeschlossen hat.|NULL für Anforderungen, die noch nicht kompiliert wurden. andernfalls ein gültiger **DateTime** -Wert, der kleiner als start_time und kleiner oder gleich der aktuellen Uhrzeit ist.|
|end_time|**datetime**|Der Zeitpunkt, zu dem die Ausführung der Anforderung abgeschlossen wurde, fehlgeschlagen ist oder abgebrochen wurde.|NULL für Warteschlangen-oder aktive Anforderungen; andernfalls ein gültiger **DateTime** -Wert, der kleiner oder gleich der aktuellen Zeit ist.|  
|total_elapsed_time|**int**|Verstrichene Zeit seit dem Start der Anforderung in Millisekunden.|Zwischen 0 und dem Unterschied zwischen start_time und end_time.</br></br> Wenn total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, ist total_elapsed_time weiterhin der Höchstwert. Mit dieser Bedingung wird die Warnung "der Höchstwert wurde überschritten" generiert.</br></br> Der maximale Wert in Millisekunden entspricht 24,8 Tagen.|  
|ETI|**nvarchar(255)**|Optionale Zeichnungs Zeichenfolge, die einigen SELECT-Abfrage Anweisungen zugeordnet ist.|Eine beliebige Zeichenfolge, die "a-z", "a-z", "0-9", "_" enthält.|  
|error_id|**nvarchar (36)**|Eindeutige ID des Fehlers, der der Anforderung zugeordnet ist, sofern vorhanden.|Weitere Informationen finden Sie unter [sys. DM &#40;_pdw_errors&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); auf NULL festgelegt, wenn kein Fehler aufgetreten ist.|  
|database_id|**int**|Der Bezeichner der vom expliziten Kontext verwendeten Datenbank (z. b. use DB_X).|Siehe ID in [sys. Datenbanken &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|Befehl|**nvarchar(4000)**|Enthält den vollständigen Text der Anforderung, wie er vom Benutzer gesendet wurde.|Jeder gültige Abfrage-oder Anforderungs Text. Abfragen, die länger als 4000 Bytes sind, werden abgeschnitten.|  
|resource_class|**nvarchar (20)**|Die Ressourcen Klasse für diese Anforderung. Weitere Informationen finden Sie unter Related **concurrency_slots_used** in [sys. DM &#40;_pdw_resource_waits&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).  Weitere Informationen zu Ressourcen Klassen finden Sie unter [Ressourcen Klassen &](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) workloadverwaltung. |Statische Ressourcenklassen</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Dynamische Ressourcenklassen</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|Die Wichtigkeits Einstellung, mit der die Anforderung übermittelt wurde. Anforderungen mit niedrigerer Wichtigkeit bleiben im angehaltenen Zustand, wenn Anforderungen höherer Wichtigkeit übermittelt werden.  Anforderungen mit höherer Wichtigkeit werden vor Anforderungen niedrigerer Wichtigkeit ausgeführt, die zuvor übermittelt wurden.  Weitere Informationen zur Wichtigkeit finden Sie unter [Wichtigkeit der Arbeitsauslastung](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance).  |NULL</br>low</br>below_normal</br>Normal (Standard)</br>above_normal</br>high|
|group_name| |Für die interne Verwendung vorgesehen.</br>Betrifft: Azure SQL Data Warehouse|
|resource_allocation_percentage| |Für die interne Verwendung vorgesehen.</br>Betrifft: Azure SQL Data Warehouse|
|result_set_cache|**bit**|Gibt an, ob eine abgeschlossene Abfrage ein Ergebnis Cache Treffer (1) oder nicht (0) war.|0,1|
||||
  
 Informationen über die maximale Anzahl von Zeilen, die in dieser Sicht beibehalten werden, finden Sie im Abschnitt "Metadaten" im Thema [Kapazitäts Limits](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .   
  
## <a name="permissions"></a>Berechtigungen

 Erfordert die VIEW SERVER STATE-Berechtigung.  
  
## <a name="security"></a>Sicherheit

 sys. DM _pdw_exec_requests filtert die Abfrageergebnisse nicht nach datenbankspezifischen Berechtigungen. Anmeldungen mit der View Server State-Berechtigung können Ergebnisse-Abfrageergebnisse für alle Datenbanken abrufen.  
  
>[!WARNING]  
>Ein Angreifer kann sys. DM _pdw_exec_requests verwenden, um Informationen zu bestimmten Datenbankobjekten abzurufen, indem er einfach die View Server State-Berechtigung und keine datenbankspezifische Berechtigung besitzt.  
  
## <a name="see-also"></a>Siehe auch

 [SQL Data Warehouse und parallele Data Warehouse dynamischen Verwaltungs Sichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
