---
title: Sp_monitor (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: stevestein
ms.author: sstein
ms.openlocfilehash: d91f774973588096ea73675d9b0e9ebf6368f1ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022326"
---
# <a name="spmonitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt statistische Informationen zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Beschreibung|  
|-----------------|-----------------|  
|**last_run**|Zeit **Sp_monitor** zuletzt ausgeführt wurde.|  
|**current_run**|Zeit **Sp_monitor** ausgeführt wird.|  
|**Sekunden**|Die Anzahl der Sekunden seit **Sp_monitor** ausgeführt wurde.|  
|**cpu_busy**|Die Anzahl von Sekunden, während derer von der CPU des Servercomputers für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Vorgänge ausgeführt wurden.|  
|**io_busy**|Die Anzahl von Sekunden, während derer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Eingabe- und Ausgabevorgänge ausgeführt wurden.|  
|**Im Leerlauf**|Die Anzahl von Sekunden, während derer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sich im Leerlauf befand.|  
|**packets_received**|Die Anzahl von Eingabepaketen, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelesen wurden.|  
|**packets_sent**|Die Anzahl der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geschriebenen Ausgabepakete.|  
|**packet_errors**|Die Anzahl von Fehlern, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Lesen und Schreiben von Paketen festgestellt wurden.|  
|**total_read**|Die Anzahl von Lesevorgängen durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_write**|Die Anzahl von Schreibvorgängen durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**total_errors**|Die Anzahl von Fehlern, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Lesen und Schreiben festgestellt wurden.|  
|**Verbindungen**|Die Anzahl von Anmeldungen oder versuchten Anmeldungen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden mithilfe einer Reihe von Funktionen quantitative Angaben über die ausgeführten Vorgänge gespeichert. Ausführen von **Sp_monitor** zeigt die aktuellen Werte, die von diesen Funktionen zurückgegeben werden, und zeigt, wie viel sie seit dem letzten geändert haben die Prozedur ausgeführt wurde.  
  
 Für jede Spalte wird die Statistik im Formular gedruckt *Anzahl*(*Anzahl*)-*Anzahl*% oder *Anzahl*(*Anzahl*). Die erste *Anzahl* bezieht sich auf die Anzahl von Sekunden (für **Cpu_busy**, **Io_busy**, und **im Leerlauf**) oder die Gesamtanzahl (für die anderen Variablen) seit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurde neu gestartet. Die *Anzahl* in Klammern bezieht sich auf die Anzahl von Sekunden oder die Gesamtanzahl seit dem letzten **Sp_monitor** ausgeführt wurde. Der Prozentsatz wird der Prozentsatz der Zeit seit **Sp_monitor** zuletzt ausgeführt wurde. Wenn der Bericht zeigt z. B. **Cpu_busy** als 4250 (215)-68 % die CPU wurde 4250 Sekunden seit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuletzt gestartet, 215 Sekunden seit **Sp_monitor** wurde die letzte Ausführung und 68 Prozent der der Gesamtzeit seit **Sp_monitor** zuletzt ausgeführt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zur Auslastung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgegeben.  
  
```  
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
||||  
|-|-|-|  
|**last_run**|**current_run**|**Sekunden**|  
|Mar 29 1998 11:55AM|Apr 4 1998 2:22 PM|561|  
  
||||  
|-|-|-|  
|**cpu_busy**|**io_busy**|**Im Leerlauf**|  
|190(0)-0%|187(0)-0%|148(556)-99%|  
  
||||  
|-|-|-|  
|**packets_received**|**packets_sent**|**packet_errors**|  
|16(1)|20(2)|0(0)|  
  
|||||  
|-|-|-|-|  
|**total_read**|**total_write**|**total_errors**|**Verbindungen**|  
|141(0)|54920(127)|0(0)|4(0)|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
