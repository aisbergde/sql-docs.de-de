---
title: sys. PDW _materialized_view_column_distribution_properties (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 8713f0728f7afb8e86b693fe5f1e50652bbddf43
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811429"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql-preview"></a>sys.pdw_materialized_view_column_distribution_properties (Transact-SQL) (preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Zeigt Verteilungs Informationen für Spalten in einer materialisierten Sicht an.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID des Objekts, zu dem die Spalte gehört. |  
|column_id|**int**|Die ID der Spalte.|  
|distribution_ordinal|**tinyint**|0 = keine Verteilungs Spalte.</br> 1 = SQL Data Warehouse verwendet diese Spalte, um die materialisierte Sicht zu verteilen.|
 
## <a name="permissions"></a>Berechtigungen 

Erfordert die VIEW DATABASE STATE-Berechtigung.
 
## <a name="see-also"></a>Siehe auch

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse- und Parallel Data Warehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[In Azure SQL Data Warehouse unterstützte Systemsichten](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[In Azure SQL Data Warehouse unterstützte T-SQL-Anweisungen](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
