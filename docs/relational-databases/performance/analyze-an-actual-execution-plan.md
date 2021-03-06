---
title: Analysieren eines tatsächlichen Ausführungsplans | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: e0f23ceb75856db921e4c6303a8013d351f364e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "68219594"
---
# <a name="analyze-an-actual-execution-plan"></a>Analysieren eines tatsächlichen Ausführungsplans
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Thema wird das Analysieren tatsächlicher grafischer Ausführungspläne mithilfe des Plananalysefeatures von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] beschrieben. 

> [!NOTE]
> Tatsächliche Ausführungspläne werden nach der Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen oder -Batches generiert. Deshalb enthält ein tatsächlicher Ausführungsplan Laufzeitinformationen wie die tatsächliche Anzahl der Zeilen, Nutzungsmetriken der Ressourcen oder Laufzeitwarnungen (falls vorhanden). Weitere Informationen finden Sie unter [Anzeigen eines tatsächlichen Ausführungsplans](../../relational-databases/performance/display-an-actual-execution-plan.md).
  
Die Problembehandlung der Abfrageleistung erfordert umfangreiche Kenntnisse im Verständnis der Abfrageverarbeitung und Ausführungspläne, um die Grundursachen tatsächlich finden und beheben zu können.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] beinhaltet Funktionen, die einen gewissen Automatisierungsgrad bei der Analyse des tatsächlichen Ausführungsplans umsetzen, insbesondere für große und komplexe Pläne. Ziel ist es, das Auffinden von Szenarien ungenauer [Kardinalitätsschätzungen](../../relational-databases/performance/cardinality-estimation-sql-server.md) zu erleichtern und Empfehlungen zu erhalten, welche möglichen Minderungen verfügbar sein könnten.

> [!IMPORTANT]
> Stellen Sie sicher, dass die vorgeschlagenen Minderungsmaßnahmen ordnungsgemäß getestet werden, bevor Sie sie in Produktionsumgebungen anwenden.
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>So analysieren Sie einen Ausführungsplan für eine Abfrage  
  
1.  Öffnen Sie eine zuvor gespeicherte Abfrageausführungsplan-Datei (SQLPLAN-Datei) mithilfe des Menüs **Datei**, und klicken Sie auf **Datei öffnen**, oder ziehen Sie eine Plandatei in das [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]-Fenster. Wenn Sie soeben eine Abfrage ausgeführt und sich für die Anzeige ihres Ausführungsplans entschieden haben, navigieren Sie alternativ zur Registerkarte **Ausführungsplan** im Ergebnisbereich. 

2.  Klicken Sie mit der rechten Maustaste in einem leeren Bereich des Ausführungsplans, und klicken Sie dann auf **Tatsächlichen Ausführungsplan analysieren**. 

    ![Rechtsklick auf „Tatsächlichen Ausführungsplan analysieren“](../../relational-databases/performance/media/plananalysismenuoption.png "Rechtsklick auf „Tatsächlichen Ausführungsplan analysieren“")   

3.  Das Fenster **Showplan-Analyse** wird im unteren Bereich geöffnet. Die Registerkarte **Mehrere Anweisungen** ist beim Analysieren von Plänen mit mehreren Anweisungen nützlich, weil sie erlaubt, dass die richtige Anweisung analysiert wird.

4.  Wählen Sie die Registerkarte „Szenarien“ aus, um Details zu den Problemen anzuzeigen, die für den tatsächlichen Ausführungsplan gefunden wurden. Für jeden aufgelisteten Operator im linken Bereich zeigt der rechte Bereich Details zum Szenario im Link *Klicken Sie hier, um weitere Informationen zu diesem Szenario zu erhalten* sowie mögliche Gründe an, um dieses Szenario zu erläutern.

    ![Ergebnisse der Ausführungsplananalyse](../../relational-databases/performance/media/plananalysis-scenarios.png "Ergebnisse der Ausführungsplananalyse") 
