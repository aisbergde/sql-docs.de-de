---
title: Sp_help_fulltext_system_components (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_components_TSQL
- sp_help_fulltext_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_system_components
ms.assetid: ac1fc7a0-7f46-4a12-8c5c-8d378226a8ce
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 949d22b0acdd4cc6d1e9d865f4f65e847d87aa46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055050"
---
# <a name="sphelpfulltextsystemcomponents-transact-sql"></a>sp_help_fulltext_system_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Gibt Informationen über die registrierten Wörtertrennungen, Filter und Protokollhandler zurück. **Sp_help_fulltext_system_components** gibt auch eine Liste der Bezeichner von Datenbanken und Volltextkatalogen, die die angegebene Komponente verwendet haben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_fulltext_system_components   
         { 'all'| [ @component_type = ] 'component_type' }  
    , [ @param = ] 'param'  
```  
  
## <a name="arguments"></a>Argumente  
 'all'  
 Gibt Informationen für alle Volltextkomponenten zurück.  
  
`[ @component_type = ] component_type` Gibt den Typ der Komponente. *Component_type* kann einen der folgenden sein:  
  
-   **wörtertrennung**  
  
-   **filter**  
  
-   **Protokollhandler**  
  
-   **fullpath**  
  
 Wenn ein vollständiger Pfad angegeben wird, *Param* muss auch angegeben werden, durch den vollständigen Pfad zur Komponenten-DLL, oder es wird eine Fehlermeldung zurückgegeben.  
  
`[ @param = ] param` Abhängig vom Komponententyp kann dies ist eine der folgenden: ein Gebietsschemabezeichner (LCID), die Dateierweiterung mit "." Präfix, der vollständige Komponentenname des protokollhandlers oder der vollständige Pfad zur Komponenten-DLL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Folgendes Resultset wird für die Systemkomponenten zurückgegeben.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|Typ der Komponente. Einer der folgenden Typen:<br /><br /> Filter<br /><br /> Protokollhandler<br /><br /> Wörtertrennung|  
|**componentname**|**sysname**|Name der Komponente.|  
|**clsid**|**uniqueidentifier**|Klassenbezeichner der Komponente.|  
|**fullpath**|**nvarchar(256)**|Pfad zum Speicherort der Komponente.<br /><br /> NULL = Aufrufer ist kein Mitglied der festen Serverrolle **serveradmin** .|  
|**version**|**nvarchar(30)**|Version der Komponente.|  
|**Hersteller**|**sysname**|Name des Herstellers der Komponente.|  
  
 Das folgende Resultset wird nur zurückgegeben, wenn ein oder mehr als ein Volltextkatalog vorhanden ist, verwendet *Component_type*.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|Die ID der Datenbank.|  
|**ftcatid**|**int**|ID des Volltextkatalogs.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **öffentliche** Rolle Benutzer sehen jedoch nur Informationen zu den Volltextkatalogen, die für die sie die VIEW DEFINITION-Berechtigung verfügen. Nur Mitglieder der der **Serveradmin** Serverrolle sehen Werte in der **Fullpath** Spalte.  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode ist besonders beim Vorbereiten eines Upgrades wichtig. Führen Sie die gespeicherte Prozedur innerhalb einer bestimmten Datenbank aus, und ermitteln Sie mithilfe der Ausgabe, ob das Upgrade Auswirkungen auf einen bestimmten Katalog haben wird.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-all-full-text-system-components"></a>A. Auflisten aller Volltextsystemkomponenten  
 Im folgenden Beispiel werden alle Volltextsystemkomponenten aufgeführt, die auf der Serverinstanz registriert wurden.  
  
```  
EXEC sp_help_fulltext_system_components 'all';  
GO  
```  
  
### <a name="b-listing-word-breakers"></a>B. Auflisten von Wörtertrennungen  
 Im folgenden Beispiel sind alle auf der Dienstinstanz registrierten Wörtertrennungen aufgeführt.  
  
```  
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```  
  
### <a name="c-determining-whether-a-specific-word-breaker-is-registered"></a>C. Bestimmen, ob eine bestimmte Wörtertrennung registriert ist  
 Im folgenden Beispiel wird die Wörtertrennung für die türkische Sprache (LCID = 1055) aufgeführt, wenn diese auf dem System installiert und auf der Dienstinstanz registriert wurde. In diesem Beispiel gibt an, den Parameternamen, **@component_type** und **@param** .  
  
```  
EXEC sp_help_fulltext_system_components @component_type = 'wordbreaker', @param = 1055;  
GO  
```  
  
 In der Standardeinstellung ist diese Wörtertrennung nicht installiert, das Resultset ist daher leer.  
  
### <a name="d-determining-whether-a-specific-filter-has-been-registered"></a>D. Bestimmen, ob ein bestimmter Filter registriert wurde  
 Im folgenden Beispiel wird der Filter für die .xdoc-Komponente aufgeführt, wenn dieser manuell auf dem System installiert und auf der Serverinstanz registriert wurde.  
  
```  
EXEC sp_help_fulltext_system_components 'filter', '.xdoc';  
GO  
```  
  
 In der Standardeinstellung ist dieser Filter nicht installiert, das Resultset ist daher leer.  
  
### <a name="e-listing-a-specific-dll-file"></a>E. Auflisten einer bestimmten DLL-Datei  
 Im folgenden Beispiel wird die DLL-Datei `nlhtml.dll` aufgeführt, die in der Standardeinstellung installiert ist.  
  
```  
EXEC sp_help_fulltext_system_components 'fullpath',   
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\nlhtml.dll';  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen oder Ändern von registrierten filtern und Wörtertrennungen](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Volltextsuche und semantische Suche von gespeicherten Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
