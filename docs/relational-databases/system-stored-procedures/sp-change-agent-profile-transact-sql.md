---
title: sp_change_agent_profile (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_agent_profile
- sp_change_agent_profile_TSQL
helpviewer_keywords:
- sp_change_agent_profile
ms.assetid: e73acf8d-0be8-4197-ba11-fe798d0e2820
author: stevestein
ms.author: sstein
ms.openlocfilehash: c49a710b25bad0cf36115afadc439cbe793981c3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768923"
---
# <a name="spchangeagentprofile-transact-sql"></a>sp_change_agent_profile (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Ändert einen Parameter eines Replikations-Agentprofils, das in der [MSagent_profiles &#40;-&#41; Transact-SQL-](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) Tabelle gespeichert ist. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## <a name="arguments"></a>Argumente  
`[ @profile_id = ] profile_id`Die ID des Profils. *profile_id* ist vom Datentyp **int**und hat keinen Standardwert.  
  
`[ @property = ] 'property'`Der Name der Eigenschaft. *Property* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @value = ] 'value'`Der neue Wert der-Eigenschaft. der Wert ist vom Datentyp **nvarchar (3000)** und hat keinen Standard *Wert* .  
  
 In dieser Tabelle werden die Profileigenschaften beschrieben, die geändert werden können.  
  
|Eigenschaft|Beschreibung|  
|--------------|-----------------|  
|**description**|Beschreibung für das Profil.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **sp_change_agent_profile** wird für alle Replikations Typen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Server Rolle **sysadmin** können **sp_change_agent_profile**ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_agent_profile &#40;(Transact-SQL)&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
