---
title: Verbinden von Komponenten mit Pfaden | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a75a9717345d1d0dc4c2fe30bf7fc441cb91ddc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060387"
---
# <a name="connect-components-with-paths"></a>Verbinden von Komponenten mit Pfaden
  Den Datenfluss in einem Paket erstellen Sie auf der Entwurfsoberfläche der Registerkarte **Datenfluss** im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer. Falls ein Datenfluss zwei Datenflusskomponenten enthält, können Sie diese verbinden, indem Sie die Ausgabe einer Quelle oder Transformation mit der Eingabe einer Transformation oder eines Zieles verbinden. Der Konnektor zwischen den beiden Datenflusskomponenten wird als Pfad bezeichnet.  
  
 Im folgenden Diagramm wird ein einfacher Datenfluss mit einer Quellkomponente, zwei Transformationen, einer Zielkomponente und den Pfaden, die diese verbinden, angezeigt.  
  
 ![Data flow](media/mw-dts-08.gif "Data flow")  
  
 Wenn zwei Komponenten verbunden sind, können Sie die Metadaten der Daten, die über den Pfad verschoben werden, und die Eigenschaften des Pfades in **Datenflusspfad-Editor**anzeigen. Weitere Informationen finden Sie unter [Integration Services Paths](data-flow/integration-services-paths.md).  
  
 Sie können Pfaden auch Daten-Viewer hinzufügen. Mit einem Daten-Viewer können Sie Daten anzeigen, die zwischen Datenflusskomponenten verschoben werden, wenn das Paket ausgeführt wird.  
  
### <a name="to-connect-components-in-a-data-flow"></a>So verbinden Sie Komponenten in einem Datenfluss  
  
-   [Verbinden von Komponenten in einem Datenfluss](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-path-properties"></a>So legen Sie Pfadeigenschaften fest  
  
-   [Festlegen der Eigenschaften eines Pfads mithilfe des Datenflusspfad-Editors](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>So zeigen Sie Pfadmetadaten an  
  
-   [Anzeigen von Pfadmetadaten im Datenflusspfad-Editor](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>So zeigen Sie Pfadmetadaten an  
  
-   [Hinzufügen eines Daten-Viewers zu einem Datenfluss](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datenflusstask](control-flow/data-flow-task.md)   
 [Datenfluss](data-flow/data-flow.md)   
 [Transformieren von Daten mit Transformationen](data-flow/transformations/transform-data-with-transformations.md)   
 [Fehlerbehandlung in Daten](data-flow/error-handling-in-data.md)  
  
  
