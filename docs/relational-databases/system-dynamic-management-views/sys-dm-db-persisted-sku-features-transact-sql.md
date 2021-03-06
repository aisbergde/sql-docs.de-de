---
title: sys. DM _db_persisted_sku_features (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server]
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1e9f56c4321ca0289f6e6a456586f418c1e4dbb
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123073"
---
# <a name="sysdm_db_persisted_sku_features-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Einige Features von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ändern die Art und Weise [!INCLUDE[ssDE](../../includes/ssde-md.md)] , in der Informationen in den Datenbankdateien gespeichert werden. Diese Funktionen sind nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Datenbank, die diese Funktionen enthält, kann nicht in eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben werden, die sie nicht unterstützt. Verwenden Sie die dynamische Verwaltungs Sicht sys. DM _db_persisted_sku_features, um Editions spezifische Funktionen aufzulisten, die in der aktuellen Datenbank aktiviert sind.
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Externer Name der Funktion, die in der aktuellen Datenbank aktiviert ist, aber nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird. Diese Funktion muss entfernt werden, bevor die Datenbank zu allen verfügbaren Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migriert werden kann.|  
|feature_id|**int**|Funktions-ID, die der Funktion zugeordnet ist. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]. installiert haben.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die Datenbank.  
  
## <a name="remarks"></a>Hinweise  
 Wenn von der Datenbank keine Features verwendet werden, die möglicherweise durch eine bestimmte Edition eingeschränkt sind, gibt die Sicht keine Zeilen zurück.  
  
 sys. DM _db_persisted_sku_features kann die folgenden Daten Bank veränderlichen Features auflisten, die auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bestimmte Editionen beschränkt sind:  
  
-   **Changecapture**: Gibt an, dass für eine Datenbank Change Data Capture aktiviert ist. Um Change Data Capture zu entfernen, verwenden Sie die gespeicherte Prozedur [sys. sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) . Weitere Informationen finden Sie unter [Informationen zu Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **Columnstoreindex**: Gibt an, dass mindestens eine Tabelle über einen columnstore--Index verfügt. Damit eine Datenbank in eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben werden kann, die dieses Feature nicht unterstützt, verwenden Sie die Anweisung [Drop Index](../../t-sql/statements/drop-index-transact-sql.md) oder [Alter Index](../../t-sql/statements/alter-index-transact-sql.md) , um den columnstore--Index zu entfernen. Weitere Informationen finden Sie unter [columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **Komprimierung**: Gibt an, dass mindestens eine Tabelle oder ein Index die Datenkomprimierung oder das vardecimal--Speicherformat verwendet. Damit eine Datenbank in eine Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben werden kann, die diese Funktion nicht unterstützt, verwenden Sie die [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) -oder [Alter Index](../../t-sql/statements/alter-index-transact-sql.md) -Anweisung, um die Datenkomprimierung zu entfernen. Um das vardecimal-Speicherformat zu entfernen, verwenden Sie die sp_tableoption-Anweisung. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **Multiplefscontainers**: Gibt an, dass die Datenbank mehrere FILESTREAM-Container verwendet. Die Datenbank verfügt über eine FILESTREAM-Datei Gruppe mit mehreren Containern (Dateien). Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **Inmemoryoltp**: Gibt an, dass die Datenbank in-Memory-OLTP verwendet. Die Datenbank verfügt über eine MEMORY_OPTIMIZED_DATA-Dateigruppe. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **Aufteilung.** Gibt an, dass die Datenbank partitionierte Tabellen, partitionierte Indizes, partitionierte Schemas oder Partitionsfunktionen enthält. Damit eine Datenbank in eine andere Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als die Enterprise oder Developer Edition verlagert werden kann, genügt es nicht, die Tabelle dahingehend abzuändern, dass sie sich in einer einzigen Partition befindet. Sie müssen die partitionierte Tabelle entfernen. Wenn die Tabelle Daten enthält, verwenden Sie SWITCH PARTITION, um jede Partition in eine nicht partitionierte Tabelle zu konvertieren. Löschen Sie dann die partitionierte Tabelle, das Partitionsschema und die Partitionsfunktion.  
  
-   **TransparentDataEncryption.** Gibt an, dass eine Datenbank mit transparenter Datenverschlüsselung verschlüsselt wird. Um die transparente Datenverschlüsselung zu entfernen, verwenden Sie die ALTER DATABASE-Anweisung. Weitere Informationen finden Sie unter [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> Ab Service [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Pack 1 sind diese Features mit Ausnahme von **transparentdataencryption.** sind für mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editionen verfügbar und nicht nur für die Enterprise oder Developer Edition.

 Wenn Sie feststellen möchten, ob in einer Datenbank Funktionen verwendet werden, die nur in bestimmten Editionen verfügbar sind, führen Sie die folgende Anweisung in der Datenbank aus:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungs Sichten &#40;in Verbindung mit der Datenbank Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Editionen und unterstützten Funktionen von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Editionen und unterstützten Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
