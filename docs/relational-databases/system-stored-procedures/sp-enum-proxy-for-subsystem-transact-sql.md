---
title: Sp_enum_proxy_for_subsystem (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 93a55b28325bd9b04af569120ad34baeb689e8f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124662"
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet die Berechtigungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Proxys für den Zugriff auf Subsysteme auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumente  
`[ @proxy_id = ] proxy_id` Die ID des Proxys für den Informationen aufgelistet. Die *Proxy_id* ist **Int**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
`[ @proxy_name = ] 'proxy_name'` Der Name des Proxys für den Informationen aufgelistet. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
`[ @subsystem_id = ] subsystem_id` Die ID des Subsystems, für das Informationen aufgelistet. Die *Subsystem_id* ist **Int**, hat den Standardwert NULL. Entweder die *Subsystem_id* oder *Subsystem_name* kann angegeben werden.  
  
`[ @subsystem_name = ] 'subsystem_name'` Der Name des Subsystems, für das Informationen aufgelistet. Die *Subsystem_name* ist **Sysname**, hat den Standardwert NULL. Entweder die *Subsystem_id* oder *Subsystem_name* kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|ID des Subsystems|  
|**subsystem_name**|**sysname**|Der Name des Subsystems.|  
|**proxy_id**|**int**|ID des Proxys.|  
|**proxy_name**|**sysname**|Der Name des Proxys.|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Parameter angegeben werden, **Sp_enum_proxy_for_subsystem** listet Informationen zu allen Proxys in der Instanz für jedes Subsystem.  
  
 Wenn eine Proxy-Id oder ein Proxyname angegeben wird, **Sp_enum_proxy_for_subsystem** Listen-Subsysteme, die der Proxy den Zugriff auf. Wenn eine Subsystem-Id oder ein subsystemname angegeben wird, **Sp_enum_proxy_for_subsystem** Proxys, die Zugriff auf dieses Subsystem aufgelistet.  
  
 Wenn sowohl Proxy- als auch Subsysteminformationen angegeben werden, gibt das Resultset eine Zeile zurück, falls der angegebene Proxy auf das angegebene Subsystem zugreifen kann.  
  
 Diese gespeicherte Prozedur befindet sich im **Msdb**.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Ausführungsberechtigungen für diese Prozedur erhalten standardmäßig Mitglieder der **Sysadmin** -Serverrolle sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-all-associations"></a>A. Auflisten aller Zuordnungen  
 Mit dem folgenden Beispiel werden alle Berechtigungen aufgelistet, die für die aktuelle Instanz zwischen Proxys und Subsystemen eingerichtet wurden.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. Bestimmen der Zugriffsmöglichkeiten eines Proxys für ein bestimmtes Subsystem  
 Das folgende Beispiel gibt eine Zeile zurück, falls der Proxy `Catalog application proxy` auf das `ActiveScripting`-Subsystem zugreifen kann. Andernfalls wird durch den Beispielcode ein leeres Resultset zurückgegeben.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
