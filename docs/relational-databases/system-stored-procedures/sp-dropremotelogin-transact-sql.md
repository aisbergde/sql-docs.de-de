---
title: Sp_dropremotelogin (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: c316f48f3e590fcba419e125f8e327b25ee1ede6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933824"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Remoteanmeldenamen, der einem lokalen Anmeldenamen zugeordnet ist, mit dem gespeicherte Remoteprozeduren auf dem lokalen Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt werden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Verwenden Sie stattdessen Verbindungsserver und gespeicherte Prozeduren verknüpfte Server.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @remoteserver = ] 'remoteserver'` Ist der Name des Remoteservers zugeordnet, die der Remoteanmeldung, die entfernt werden soll. *remoteserver* ist vom Datentyp **sysname**und hat keinen Standardwert. Der*remoteserver* muss bereits vorhanden sein.  
  
`[ @loginame = ] 'login'` Ist der optionale Anmeldename auf dem lokalen Server, der mit dem Remoteserver zugeordnet ist. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. *login* muss ggf. bereits vorhanden sein.  
  
`[ @remotename = ] 'remote_name'` Der optionale Name der Remoteanmeldung, die zugeordnet wird *Anmeldung* beim Anmelden vom Remoteserver. *remote_name* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn nur *remoteserver* angegeben wird, werden alle Remoteanmeldenamen für diesen Remoteserver vom lokalen Server entfernt. Wenn zusätzlich *login* angegeben wird, werden alle Remoteanmeldenamen von *remoteserver* , die diesem lokalen Anmeldenamen zugeordnet sind, vom lokalen Server entfernt. Wenn außerdem *remote_name* angegeben wird, wird nur der Remoteanmeldename für diesen Remotebenutzer von *remoteserver* vom lokalen Server entfernt.  
  
 Mithilfe von **sp_addlogin**fügen Sie Benutzer lokaler Server hinzu. Mithilfe von **sp_droplogin**entfernen Sie Benutzer lokaler Server.  
  
 Remoteanmeldenamen sind nur erforderlich, wenn Sie frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Version 7.0 und höher, werden stattdessen Anmeldenamen für den Verbindungsserver verwendet. Verwenden Sie **sp_addlinkedsrvlogin** und **sp_droplinkedsrvlogin** , um Verbindungsserver-Anmeldenamen hinzuzufügen und zu entfernen.  
  
 **sp_dropremotelogin** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder **securityadmin** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. Löschen sämtlicher Remoteanmeldenamen für einen Remoteserver  
 Im folgenden Beispiel wird der Eintrag für den Remoteserver `ACCOUNTS`entfernt. Dabei werden alle Zuordnungen zwischen Anmeldenamen auf dem lokalen Server und Remoteanmeldenamen auf dem Remoteserver entfernt.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. Löschen einer Anmeldenamenzuordnung  
 Im folgenden Beispiel wird der Eintrag entfernt, durch den Remoteanmeldenamen vom Remoteserver `ACCOUNTS` dem lokalen Anmeldenamen `Albert`zugeordnet werden.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. Löschen eines Remotebenutzers  
 Im folgenden Beispiel wird der Anmeldename für den Remoteanmeldenamen `Chris` auf dem Remoteserver `ACCOUNTS` entfernt, der dem lokalen Anmeldenamen `salesmgr`zugeordnet war.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
