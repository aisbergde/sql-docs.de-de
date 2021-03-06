---
title: sp_estimate_data_compression_savings (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
author: stevestein
ms.author: sstein
ms.openlocfilehash: 447f3cf0f304fb167b85ba49f5a8a583f08cd912
ms.sourcegitcommit: 2bc15f81d7a238c6fc409440800f1d6c7943a4b5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2019
ms.locfileid: "70059300"
---
# <a name="sp_estimate_data_compression_savings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die aktuelle Größe des angeforderten Objekts zurück und schätzt die Objektgröße für den angeforderten Komprimierungsstatus. Die Komprimierung kann für ganze Tabellen oder Teile von Tabellen ermittelt werden. Dazu zählen Heaps, gruppierte Indizes, nicht gruppierte Indizes, columnstore--Indizes, indizierte Sichten und Tabellen-und Index Partitionen. Die Objekte können mithilfe von Zeilen-, Seiten-, columnstore--oder columnstore--Archiv Komprimierung komprimiert werden. Wenn die Tabelle, der Index oder die Partition bereits komprimiert ist, können Sie mithilfe dieser Prozedur die Größe der erneut komprimierten Tabelle, des erneut komprimierten Index oder der erneut komprimierten Partition einschätzen.  
  
> [!NOTE]
> Komprimierung und **sp_estimate_data_compression_savings** sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Um die Größe des Objekts bei Verwendung der angeforderten Komprimierungseinstellung einzuschätzen, fragt diese gespeicherte Prozedur das Quellobjekt ab und lädt diese Daten in eine entsprechende Tabelle und einen entsprechenden Index in tempdb. Die Tabelle oder der Index, die bzw. der in tempdb erstellt wurde, wird anschließend entsprechend der angeforderten Einstellung komprimiert, und die Komprimierungseinsparungen werden berechnet.  
  
 Verwenden Sie die [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) -Anweisung oder die [Alter Index](../../t-sql/statements/alter-index-transact-sql.md) -Anweisung, um den Komprimierungs Status einer Tabelle, eines Indexes oder einer Partition zu ändern. Allgemeine Informationen zur Komprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
> [!NOTE]  
> Wenn die vorhandenen Daten fragmentiert sind, können Sie ihre Größe möglicherweise ohne Komprimierung verringern, indem Sie den Index neu erstellen. Für Indizes wird der Füllfaktor während der Neuerstellung des Indexes angewendet. Dadurch könnte die Größe des Indexes zunehmen.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [ @index_id = ] index_id   
   , [ @partition_number = ] partition_number   
   , [ @data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @schema_name=] '*schema_name*'  
 Der Name des Datenbankschemas, das die Tabelle oder die indizierte Sicht enthält. *schema_name* ist vom **Datentyp vom Datentyp sysname**. Wenn *schema_name* NULL ist, wird das Standardschema des aktuellen Benutzers verwendet.  
  
 [ @object_name=] '*object_name*'  
 Der Name der Tabelle oder der indizierten Sicht des Indexes. *database_name* ist vom Datentyp **sysname**.  
  
 [ @index_id=] *index_id*  
 Die ID des Indexes. *index_id* ist vom Datentyp **int**und kann einen der folgenden Werte aufweisen: die ID-Nummer eines Indexes, NULL oder 0, wenn *object_id* ein Heap ist. Geben Sie NULL an, wenn Informationen zu allen Indizes für eine Basistabelle oder Sicht zurückgegeben werden sollen. Wenn Sie NULL angeben, müssen Sie für *partition_number*auch NULL angeben.  
  
 [ @partition_number=] *partition_number*  
 Die Partitionsnummer im Objekt. *partition_number* ist vom Datentyp **int**und kann einen der folgenden Werte aufweisen: die Partitionsnummer eines Indexes oder Heaps, NULL oder 1 für einen nicht partitionierten Index oder Heap.  
  
 Um die Partition anzugeben, können Sie auch die [$Partition](../../t-sql/functions/partition-transact-sql.md) -Funktion angeben. Geben Sie NULL an, wenn Informationen zu allen Partitionen des besitzenden Objekts zurückgegeben werden sollen.  
  
 [ @data_compression=] '*DATA_COMPRESSION*'  
 Der Typ der Komprimierung, die ausgewertet werden soll. *DATA_COMPRESSION* kann einen der folgenden Werte aufweisen: None, Row, Page, columnstore oder COLUMNSTORE_ARCHIVE.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Das folgende Resultset wird zurückgegeben, damit Informationen zur aktuellen und geschätzten Größe von Tabelle, Index oder Partition bereitgestellt werden.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|Der Name der Tabelle oder indizierten Sicht.|  
|schema_name|**sysname**|Das Schema der Tabelle oder indizierten Sicht.|  
|index_id|**int**|Index-ID eines Index:<br /><br /> 0 = Heap<br /><br /> 1 = Gruppierter Index<br /><br /> > 1 = nicht gruppierter Index|  
|partition_number|**int**|Partitionsnummer. Gibt 1 für eine nicht partitionierte Tabelle oder einen Index zurück.|  
|size_with_current_compression_setting (KB)|**bigint**|Die Größe der angeforderten, vorhandenen Tabelle, des Indexes oder der Partition.|  
|size_with_requested_compression_setting (KB)|**bigint**|Die geschätzte Größe der Tabelle, des Indexes oder der Partition, die bzw. der die angeforderte Komprimierungseinstellung verwendet, und der vorhandene Füllfaktor (sofern zutreffend). Zudem wird vorausgesetzt, dass keine Fragmentierung vorliegt.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|Die Größe der Stichprobe mit der aktuellen Komprimierungseinstellung. Dies beinhaltet jegliche Fragmentierung.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|Die Größe der Stichprobe, die mithilfe der angeforderten Komprimierungseinstellung erstellt wird, mit vorhandenem Füllfaktor (sofern zutreffend) und ohne Fragmentierung.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden `sp_estimate_data_compression_savings` Sie, um die Einsparungen zu schätzen, die beim Aktivieren einer Tabelle oder einer Partition für die Zeilen-, Seiten-, columnstore--oder columnstore--Archiv Komprimierung auftreten können. Wenn beispielsweise die durchschnittliche Größe der Zeile um 40 Prozent verringert werden kann, können Sie die Größe des Objekts potenziell um 40 Prozent verringern. Möglicherweise erzielen Sie keine Platzeinsparung, weil dies vom Füllfaktor und von der Zeilengröße abhängt. Wenn Sie z. b. eine Zeile haben, die 8.000 Bytes lang ist, und Sie die Größe um 40 Prozent verringern, können Sie immer noch nur eine Zeile auf einer Datenseite anpassen. Daher werden keine Einsparungen erzielt.  
  
 Wenn die Ergebnisse der Ausführung `sp_estimate_data_compression_savings` von darauf hindeuten, dass die Tabelle vergrößert wird, bedeutet dies, dass viele Zeilen in der Tabelle fast die gesamte Genauigkeit der Datentypen verwenden und dass der für das komprimierte Format benötigte kleine mehr Aufwand größer ist als die Einsparung von komprimi. Aktivieren Sie in diesem seltenen Fall die Komprimierung nicht.  
  
 Wenn eine Tabelle für die Komprimierung aktiviert ist `sp_estimate_data_compression_savings` , verwenden Sie, um die durchschnittliche Größe der Zeile zu schätzen, wenn die Tabelle nicht komprimiert ist.  
  
 Eine (IS)-Sperre wird während dieses Vorgangs für die Tabelle abgerufen. Wenn keine (IS)-Sperre abgerufen werden kann, wird die Prozedur blockiert. Die Tabelle wird unter der Read Committed-Isolationsstufe gescannt.  
  
 Wenn die angeforderte Komprimierungseinstellung mit der aktuellen Komprimierungseinstellung identisch ist, gibt die gespeicherte Prozedur die geschätzte Größe ohne Fragmentierung und mit dem vorhandenen Füllfaktor zurück.  
  
 Wenn die Index- oder die Partitions-ID nicht vorhanden ist, werden keine Ergebnisse zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert `SELECT` die-Berechtigung für die Tabelle.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Vor SQL Server 2019 wurde dieses Verfahren nicht für columnstore--Indizes angewendet und akzeptierte daher nicht die Daten Komprimierungs Parameter columnstore-und COLUMNSTORE_ARCHIVE.  Ab SQL Server 2019 können columnstore--Indizes als Quell Objekt zur Schätzung und als angeforderter Komprimierungstyp verwendet werden.

## <a name="considerations-for-columnstore-indexes"></a>Überlegungen zu columnstore-Indizes
 Ab `sp_estimate_compression_savings` unter [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]stützt die Schätzung von columnstore--und columnstore--Archiv Komprimierung. Anders als bei der Seiten-und Zeilen Komprimierung muss beim Anwenden der columnstore--Komprimierung auf ein Objekt ein neuer columnstore--Index erstellt werden Aus diesem Grund wird bei Verwendung der columnstore--und COLUMNSTORE_ARCHIVE-Optionen dieser Prozedur der Typ des für die Prozedur bereitgestellten Quell Objekts bestimmt den Typ des columnstore--Indexes, der für die geschätzte Größen Schätzung verwendet wird. In der folgenden Tabelle werden die Verweis Objekte veranschaulicht, die zur Schätzung der Komprimierungs Einsparungen für jeden @data_compression Quell Objekttyp verwendet werden, wenn der Parameter auf columnstore oder COLUMNSTORE_ARCHIVE festgelegt ist.

 |Quell Objekt|Verweis Objekt|
 |-----------------|---------------|
 |Heap|Gruppierter Columnstore-Index|
 |Gruppierter Index|Gruppierter Columnstore-Index|
 |Nicht gruppierter Index|Nicht gruppierter columnstore--Index (einschließlich der Schlüssel Spalten und aller enthaltenen Spalten des bereitgestellten nicht gruppierten Indexes sowie der partitions Spalte der Tabelle, sofern vorhanden)|
 |Nicht gruppierter Columnstore-Index|Nicht gruppierter columnstore--Index (einschließlich der gleichen Spalten wie der angegebene nicht gruppierte columnstore--Index)|
 |Gruppierter Columnstore-Index|Gruppierter Columnstore-Index|

> [!NOTE]  
> Beim Schätzen der columnstore--Komprimierung aus einem rowstore-Quell Objekt (gruppierter Index, nicht gruppierter Index oder Heap), wenn Spalten im Quell Objekt vorhanden sind, die einen Datentyp aufweisen, der in einem columnstore--Index nicht unterstützt wird, sp_estimate_compression_savings schlägt mit einem Fehler fehl.

 Wenn der `@data_compression` -Parameter auf `NONE`, `ROW`oder `PAGE` festgelegt ist und das Quell Objekt ein columnstore--Index ist, werden in der folgenden Tabelle die verwendeten Verweis Objekte beschrieben.

 |Quell Objekt|Verweis Objekt|
 |-----------------|---------------|
 |Gruppierter Columnstore-Index|Heap|
 |Nicht gruppierter Columnstore-Index|Nicht gruppierter Index (einschließlich der Spalten, die im nicht gruppierten columnstore--Index als Schlüssel Spalten enthalten sind, und die Partitions Spalte der Tabelle, sofern vorhanden, als enthaltene Spalte)|

> [!NOTE]  
> Wenn Sie die rowstore-Komprimierung (None, Row oder Page) aus einem columnstore--Quell Objekt schätzen, stellen Sie sicher, dass der Quell Index nicht mehr als 32 Spalten enthält, da dies der Grenzwert ist, der in einem rowstore-Index (Nonclustered) unterstützt wird.
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Größe der `Production.WorkOrderRouting`-Tabelle geschätzt, wenn sie mit der `ROW`-Komprimierung komprimiert wird.  
  
```sql  
USE AdventureWorks2016;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Datenbank-Engine gespeicherter &#40;Prozeduren (Transact-SQL)&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Implementierung von Unicode-Komprimierung](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
