---
title: Sys. database_recovery_status (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_recovery_status_TSQL
- database_recovery_status
- sys.database_recovery_status
- sys.database_recovery_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_recovery_status catalog view
ms.assetid: 46fab234-1542-49be-8edf-aa101e728acf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e78b5a8640918291fc68e5b4882448b94a1b9d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079522"
---
# <a name="sysdatabaserecoverystatus-transact-sql"></a>sys.database_recovery_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile pro Datenbank. Wenn die Datenbank nicht geöffnet wird, versucht das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , sie zu starten.  
  
 Um die Zeile für eine andere Datenbank als die **master** - oder die **tempdb**-Datenbank anzeigen zu können, muss eine der folgenden Bedingungen erfüllt sein:  
  
-   Sie müssen der Besitzer der Datenbank sein.  
  
-   Sie müssen über die ALTER ANY DATABASE- oder VIEW ANY DATABASE-Berechtigung auf Serverebene verfügen.  
  
-   Sie müssen über die CREATE DATABASE-Berechtigung für die **master** -Datenbank verfügen.    
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank und innerhalb einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz eindeutig.|  
|**database_guid**|**uniqueidentifier**|Wird verwendet, um alle Datenbankdateien einer Datenbank miteinander in Verbindung zu bringen. Die Headerseiten aller Dateien müssen diesen GUID aufweisen, damit die Datenbank erwartungsgemäß gestartet wird. Es sollte immer nur eine Datenbank diesen GUID aufweisen. Duplikate können jedoch durch Kopieren und Anfügen von Datenbanken erstellt werden. Durch RESTORE wird immer ein neuer GUID erstellt, wenn Sie eine Datenbank wiederherstellen, die noch nicht vorhanden ist.<br /><br /> NULL= Die Datenbank ist offline, oder die Datenbank wird nicht gestartet.|  
|**family_guid**|**uniqueidentifier**|Bezeichner der "Sicherungsfamilie" für die Datenbank, der zum Erkennen von Dateien mit übereinstimmendem Wiederherstellungsstatus dient.<br /><br /> NULL= Die Datenbank ist offline, oder die Datenbank wird nicht gestartet.|  
|**last_log_backup_lsn**|**numeric(25,0)**|Die ab protokollfolgenummer der nächsten protokollsicherung.<br /><br /> Wenn der Wert NULL ist, kann nicht sichern ein Transaktionsprotokoll bis ausgeführt werden, da die Datenbank befindet sich im EINFACHEN Wiederherstellungsmodell oder keine aktuelle datenbanksicherung vorhanden ist.|  
|**recovery_fork_guid**|**uniqueidentifier**|Identifiziert den aktuell für die Datenbank aktiven Wiederherstellungs-Verzweigungspunkt.<br /><br /> NULL= Die Datenbank ist offline, oder die Datenbank wird nicht gestartet.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|Bezeichner für den ersten Wiederherstellungs-Verzweigungspunkt.<br /><br /> NULL= Die Datenbank ist offline, oder die Datenbank wird nicht gestartet.|  
|**fork_point_lsn**|**numeric(25,0)**|Wenn **first_recovery_fork_guid** ungleich (!=) **recovery_fork_guid**ist, entspricht **fork_point_lsn** der Protokollfolgenummer des aktuellen Wiederherstellungs-Verzweigungspunkts. Andernfalls ist der Wert NULL.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Datenbanken und Dateikatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
