---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ffd0ad4ddcdae91071811e57cdb8c5f6aaaea656
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476307"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Zeigt den verwendeten Speicherplatz im Resultsetcache für eine Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Datenbank.
  
![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol zum Themenlink") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Bemerkungen

Der `DBCC SHOWRESULTCACHESPACEUSED`-Befehl akzeptiert keine Parameter und gibt den verwendeten Speicherplatz der Datenbank zurück, für die der Befehl ausgeführt wird.

Die maximale Größe des Resultsetcaches beträgt 1 TB pro Datenbank.  Azure SQL Data Warehouse entfernt automatisch Einträge im Resultsetcache:

- Alle 48 Stunden, wenn das Resultset nicht verwendet wurde.
- Bei Annäherung an die maximale Größe für den Resultsetcache.

Benutzer können den Resultsetcache für eine Datenbank manuell leeren, indem sie das Feature für den Resultsetcache deaktivieren oder den Befehl `DBCC DROPRESULTSETCACHE` verwenden.   Das Anhalten einer Datenbank führt nicht dazu, dass der Resultsetcache geleert wird.  

## <a name="permissions"></a>Berechtigungen

Erfordert die VIEW SERVER STATE-Berechtigung.
  
## <a name="result-sets"></a>Resultsets  
  
|Spalte|Datentyp|und Beschreibung|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Insgesamt durch die Datenbank belegter Speicherplatz in KB. Diese Zahl ändert sich, wenn das zwischengespeicherte Resultset größer wird.|  
|data_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.|  
|index_space|BIGINT|Durch die Daten belegter Speicherplatz in KB.|  
|unused_space|BIGINT|Speicherplatz in KB, der zum reservierten Speicherplatz gehört und nicht verwendet wird.|  


## <a name="see-also"></a>Siehe auch

[ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)