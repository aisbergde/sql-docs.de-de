---
title: PowerShell-Referenz (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ed2e407b724f57d6ded518b864e3b1d78b4c489e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064965"
---
# <a name="database-engine-powershell-reference"></a>PowerShell-Referenz (Datenbank-Engine)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] beinhaltet eine Reihe von Windows PowerShell 2.0-Cmdlets zur Durchführung allgemeiner Aufgaben im [!INCLUDE[ssDE](../includes/ssde-md.md)]. Zudem können Abfrageausdrücke und Uniform Resource Names (URNs) in SQL Server PowerShell-Pfade konvertiert oder zum Angaben eines oder mehrerer Objekte im [!INCLUDE[ssDE](../includes/ssde-md.md)]verwendet werden.  
  
## <a name="database-engine-cmdlets"></a>Datenbank-Engine-Cmdlets  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] beinhaltet relativ wenige Cmdlets für das [!INCLUDE[ssDE](../includes/ssde-md.md)]. Die meisten PowerShell-Skripts, die mit dem [!INCLUDE[ssDE](../includes/ssde-md.md)] verwendet werden, nutzen den SQL Server PowerShell-Anbieter und die Verwaltbarkeitsobjektmodelle. Weitere Informationen finden Sie unter [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  
  
 Informationen zum Anfordern von Hilfe zu den SQL Server-Cmdlets in einer Windows PowerShell-Umgebung finden Sie unter [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="in-this-section"></a>In diesem Abschnitt  
 Dieser Abschnitt enthält Informationen zu den folgenden Cmdlets.  
  
|Description|Cmdlet|  
|-----------------|------------|  
|Führt Transact-SQL- und XQuery-Skripte aus, z. B. Skripts, die mit dem Hilfsprogramm `sqlcmd` ausgeführt werden können.|[Invoke-Sqlcmd-Cmdlet](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|Ermittelt, ob ein Datenbank-Engine-Objekt einer Richtlinie für die richtlinienbasierte Verwaltung entspricht.|[Invoke-PolicyEvaluation-Cmdlet](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>Informationen zu anderen Cmdlets  
 Das `Encode-Sqlname`-Cmdlet und das `Decode-Sqlname`-Cmdlet helfen Ihnen, SQL Server-Bezeichner mit Zeichen anzugeben, die in PowerShell-Pfaden nicht unterstützt werden. Weitere Informationen finden Sie unter [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md).  
  
 Mit dem `Convert-UrnToPath`-Cmdlet können Sie einen eindeutigen Ressourcennamen (Unique Resource Name, URN) für ein [!INCLUDE[ssDE](../includes/ssde-md.md)]-Objekt einen Pfad für den SQL Server PowerShell-Anbieter konvertieren. Weitere Informationen finden Sie unter [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Abfrageausdrücke und eindeutige Ressourcennamen  
 Bei Abfrageausdrücken handelt es sich um Zeichenfolgen, die eine ähnliche Syntax wie XPath nutzen, um eine Gruppe von Kriterien angeben, mit der ein oder mehrere Objekte in einer Objektmodellhierarchie aufgezählt werden. Ein eindeutiger Ressourcenname (Unique Resource Name, URN) ist ein spezieller Typ einer Abfrageausdrucks-Zeichenfolge, der ein einzelnes Objekt eindeutig kennzeichnet. Weitere Informationen finden Sie unter [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../powershell/sql-server-powershell.md)  
  
  
