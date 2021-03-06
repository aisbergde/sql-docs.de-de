---
title: ALTER EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ebab091b0e674339141c4ee2ea6d7c7993ccbabf
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893683"
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

Ändert einen externen Resource Governor-Pool, in dem Ressourcen angegeben werden, die von externen Prozessen verwendet werden können. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Für [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] in [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] kontrolliert der externe Pool `rterm.exe`, `BxlServer.exe` und andere Prozesse, die von diesen Anwendungen erzeugt wurden.
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Für [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] kontrolliert der externe Pool `rterm.exe`, `python.exe`, `BxlServer.exe` und andere Prozesse, die von diesen Anwendungen erzeugt wurden.
::: moniker-end

![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Syntax

```
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]
    [ [ , ] MAX_PROCESSES = value ]
    )
]
[ ; ]
  
<CPU_range_spec> ::=
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]
```  
  
## <a name="arguments"></a>Argumente

{ *pool_name* | "default" }  
Der Name eines vorhandenen benutzerdefinierten externen Ressourcenpools oder der externe Standardressourcenpool, der bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wird.
"default" muss bei Verwendung mit `ALTER EXTERNAL RESOURCE POOL` in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, um einen Konflikt mit `DEFAULT` zu vermeiden, das ein vom System reserviertes Wort darstellt.

MAX_CPU_PERCENT = *value*  
Gibt die maximale durchschnittliche CPU-Bandbreite an, die allen Anforderungen im externen Ressourcenpool zugewiesen werden können, wenn CPU-Konflikte bestehen. *value* ist ein Integer. Der zulässige Bereich für *value* liegt zwischen 1 und 100.

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}  
Fügt den externen Ressourcenpool an bestimmte CPUs an.

AFFINITY CPU = **(** \<CPU_range_spec> **)** ordnet den externen Ressourcenpool den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-CPUs zu, die durch die angegebenen CPU_ID-Argumente identifiziert werden. Wenn Sie AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** verwenden, wird der externe Ressourcenpool den physischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-CPUs zugeordnet, die dem angegebenen NUMA-Knoten oder dem Bereich von Knoten entsprechen.

MAX_MEMORY_PERCENT =*value*  
Gibt den gesamten Serverspeicher an, der für Anforderungen in diesem externen Ressourcenpool verwendet werden kann. *value* ist ein Integer. Der zulässige Bereich für *value* liegt zwischen 1 und 100.

MAX_PROCESSES = *value*  
Gibt die maximale Anzahl von Prozessen an, die für den externen Ressourcenpool zulässig ist. Geben Sie 0 an, um einen unbegrenzten Schwellenwert für den Pool festzulegen, der anschließend nur durch Computerressourcen gebunden ist.

## <a name="remarks"></a>Bemerkungen

Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementiert den Ressourcenpool, wenn Sie die [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md)-Anweisung ausführen.

Allgemeine Informationen zu Ressourcenpools finden Sie unter [Resource Governor-Ressourcenpool](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) und [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  

Informationen zur Verwendung von externen Ressourcenpools, mit denen Sie Machine Learning-Aufträge kontrollieren können, finden Sie unter [Resource governance for machine learning in SQL Server (Ressourcenkontrolle für Machine Learning in SQL Server)](../../advanced-analytics/r/resource-governance-for-r-services.md).
## <a name="permissions"></a>Berechtigungen

Erfordert die `CONTROL SERVER`-Berechtigung.

## <a name="examples"></a>Beispiele

Durch die folgende Anweisung wird ein externer Pool so geändert, dass die CPU-Auslastung auf 50 Prozent und der maximale Arbeitsspeicher auf 25 Prozent des verfügbaren Arbeitsspeichers auf dem Computer beschränkt wird.
  
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Siehe auch

+ [Resource governance for machine learning in SQL Server (Ressourcenkontrolle für Machine Learning in SQL Server)](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Externe Skripts aktiviert (Serverkonfigurationsoption)](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
+ [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
+ [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
+ [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
+ [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
+ [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
+ [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
