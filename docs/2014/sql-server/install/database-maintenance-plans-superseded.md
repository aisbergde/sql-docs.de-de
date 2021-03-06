---
title: Datenbank-Wartungspläne ersetzt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d41763582632a92b3a38bdbd67ee55b65f95b6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095758"
---
# <a name="database-maintenance-plans-superseded"></a>Außer Kraft gesetzte Datenbank-Wartungspläne
    
## <a name="component"></a>Komponente  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent  
  
## <a name="description"></a>Description  
 Vorhandene Datenbank-Wartungspläne werden aktualisiert und funktionieren weiterhin. Sie können allerdings keine neuen Datenbank-Wartungspläne mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Um die Wartungspläne im Objekt-Explorer anzuzeigen, erweitern Sie Verwaltung und dann Legacy. Sie können die vorhandene Datenbank-Wartungspläne in das neue Format migrieren, durch Auswahl **migrieren** aus dem Kontextmenü für alle Datenbank-Wartungsplan. Da die neue Wartungsplanfunktion kein direkter Ersatz der Datenbank-Wartungspläne ist, stehen möglicherweise einige Funktionen nach der Migration nicht mehr zur Verfügung. Bei der Migration eines Datenbank-Wartungsplans wird der alte Plan nicht gelöscht, sodass Sie seine Funktionalität als Wartungsplan testen können, bevor Sie den alten Plan entfernen.  
  
 Die folgenden Funktionen werden innerhalb der Datenbank-Wartungspläne nicht mehr unterstützt:  
  
-   Protokollversand  
  
-   Die **versuchen, eine kleinere Probleme beheben** Möglichkeit, die **Datenbankintegrität überprüfen** Aufgabe  
  
## <a name="corrective-action"></a>Korrekturmaßnahme  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verhindert ein Einschließen des Protokollversands in Datenbankwartungspläne. Weitere Informationen finden Sie unter "Protokollversand" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
  
