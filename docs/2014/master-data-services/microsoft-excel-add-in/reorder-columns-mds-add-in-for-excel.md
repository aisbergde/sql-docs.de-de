---
title: Neuanordnen von Spalten (MDS-Add-In für Excel) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ce4d9ab308f67a2f9629b4b6142ad3145ddbcf2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2018
ms.locfileid: "36057220"
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>Neuanordnen von Spalten (MDS-Add-In für Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]können Sie Spalten durch das Filtern der Liste vor dem Laden neu anordnen.  
  
 Wenn Sie Attribute im Dialogfeld **Filter** neu anordnen, werden die Daten mit der neuen Reihenfolge in Excel geladen. Wenn Sie jedoch die Attributdaten das nächste Mal filtern, wird die Reihenfolge des ursprünglichen Entwurfs wiederhergestellt. Um die Reihenfolge permanent zu ändern, sollte ein Administrator die Reihenfolge im Bereich **Systemverwaltung** von Master Data Manager ändern. Weitere Informationen finden Sie unter [Change the Order of Attributes](../change-the-order-of-attributes.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
### <a name="to-reorder-mds-managed-columns"></a>So ordnen Sie von MDS verwaltete Spalten neu an  
  
1.  Öffnen Sie Excel, und stellen Sie auf der Registerkarte **Masterdaten** eine Verbindung mit einem MDS-Repository her. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einem MDS-Repository &#40;MDS-Add-In für Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  Wählen Sie im Bereich **Master Data Explorer** ein Modell und eine Version aus. Die Liste der Entitäten wird aufgefüllt.  
  
    -   Wenn der Bereich **Master Data Explorer** nicht sichtbar ist, klicken Sie in der Gruppe **Verbinden und Laden** auf **Explorer anzeigen**.  
  
    -   Wenn der Bereich **Master Data Explorer** deaktiviert ist, liegt dies daran, dass das vorhandene Blatt bereits von MDS verwaltete Daten enthält. Um den Bereich zu aktivieren, öffnen Sie ein neues Arbeitsblatt.  
  
3.  Klicken Sie im Bereich **Master Data Explorer** auf eine Entität.  
  
4.  Klicken Sie in der Gruppe **Verbinden und Laden** auf **Filtern**.  
  
5.  Klicken Sie im Dialogfeld **Filtern** im Abschnitt **Spalten** in der Liste der Attribute auf das Attribut, das Sie bewegen möchten.  
  
6.  Klicken Sie rechts von der Liste auf den **Nach oben** - oder **Nach unten** -Pfeil, um das Attribut im Arbeitsblatt nach links und rechts zu verschieben.  
  
7.  Wiederholen Sie Schritt 7 für jedes Attribut, bis die Reihenfolge von oben nach unten die Reihenfolge von links nach rechts darstellt, die Sie im Arbeitsblatt wünschen.  
  
8.  Klicken Sie auf **Daten laden**. Das Blatt wird mit von MDS verwalteten Daten aufgefüllt, und die Spalten werden in der angegebenen Reihenfolge angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Laden von Daten &#40;MDS-Add-in für Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  