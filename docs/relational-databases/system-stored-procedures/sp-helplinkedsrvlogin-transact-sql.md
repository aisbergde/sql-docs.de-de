---
title: Sp_helplinkedsrvlogin (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1728b3e5d4cd3189a8d9a01a8b72ecedaf7cb6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122462"
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu den für einen bestimmten Verbindungsserver definierten Anmeldenamenzuordnungen bereit, die für verteilte Abfragen und gespeicherte Remoteprozeduren verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @rmtsrvname = ] 'rmtsrvname'` Ist der Name des Verbindungsservers, der für die anmeldenamenzuordnung gilt. *Rmtsrvname* ist **Sysname**, hat den Standardwert NULL. Mit NULL werden alle Anmeldenamenzuordnungen zurückgegeben, die für alle auf dem lokalen Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definierten Verbindungsserver definiert werden.  
  
`[ @locallogin = ] 'locallogin'` Ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldenamen auf dem lokalen Server, die eine Zuordnung mit dem Verbindungsserver *Rmtsrvname*. *Locallogin* ist **Sysname**, hat den Standardwert NULL. NULL gibt an, dass alle anmeldenamenzuordnungen für definiert *Rmtsrvname* zurückgegeben werden. Wenn nicht NULL ist, eine Zuordnung für *Locallogin* zu *Rmtsrvname* muss bereits vorhanden sein. *Locallogin* kann eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldename oder ein Windows-Benutzer. Dem Windows-Benutzer müssen die Zugriffsrechte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erteilt worden sein. Dies kann entweder direkt oder über seine Mitgliedschaft in einer Windows-Gruppe erfolgen, der die Zugriffsrechte erteilt wurden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**Verbindungsserver**|**sysname**|Name des Verbindungsservers.|  
|**Lokale Anmeldung**|**sysname**|Lokaler Anmeldename, für den die Zuordnung gilt.|  
|**Self-Zuordnung**|**smallint**|0 = **local Login** zugeordnet **Remoteanmeldung** beim Herstellen einer Verbindung mit **Verbindungsserver**.<br /><br /> 1 = **local Login** auf dem gleichen Anmeldenamen und Kennwort zugeordnet ist, beim Herstellen einer Verbindung mit **Verbindungsserver**.|  
|**Remoteanmeldung**|**sysname**|Anmeldename auf **LinkedServer** , zugeordnet ist **LocalLogin** beim **IsSelfMapping** ist 0. Wenn **IsSelfMapping** ist 1, **RemoteLogin** ist NULL.|  
  
## <a name="remarks"></a>Hinweise  
 Bevor Sie anmeldenamenzuordnungen löschen, verwenden Sie **Sp_helplinkedsrvlogin** Verbindungsserver zu ermitteln, die beteiligt sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Es werden keine Berechtigungen geprüft.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>A. Anzeigen aller Anmeldenamenzuordnungen für alle Verbindungsserver  
 Im folgenden Beispiel werden alle Anmeldenamenzuordnungen für alle Verbindungsserver angezeigt, die auf dem lokalen Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiert sind.  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B. Anzeigen aller Anmeldenamenzuordnungen für einen Verbindungsserver  
 Im folgenden Beispiel werden alle lokal definierten Anmeldenamenzuordnungen für den `Sales`-Verbindungsserver angezeigt.  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C. Anzeigen aller Anmeldenamenzuordnungen für eine lokale Anmeldung  
 Im folgenden Beispiel werden alle lokal definierten Anmeldenamenzuordnungen für den Anmeldenamen `Mary` angezeigt.  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
