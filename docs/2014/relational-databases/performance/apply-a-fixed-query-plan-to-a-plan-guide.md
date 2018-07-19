---
title: Anwenden eines festen Abfrageplans auf eine Planhinweisliste | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ac69187ec760c8ca9af0e7346a2f8b4c88fd5af3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419449"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>Anwenden eines festen Abfrageplans auf eine Planhinweisliste
  Sie können einen festen Abfrageplan auf eine Planhinweisliste des Typs OBJECT oder SQL anwenden. Planhinweislisten, die einen festen Abfrageplan anwenden, sind hilfreich, wenn Sie wissen, dass ein vorhandener Ausführungsplan für eine bestimmte Abfrage bessere Ergebnisse erzielt als der vom Abfrageoptimierer ausgewählte Ausführungsplan.  
  
 Im folgenden Beispiel wird eine Planhinweisliste für eine einfache Ad-hoc-SQL-Anweisung erstellt. Der gewünschte Abfrageplan für diese Anweisung wird in der Planhinweisliste durch die direkte Angabe des XML-Showplans für die Abfrage im `@hints` -Parameter bereitgestellt. Im Beispiel wird zunächst die SQL-Anweisung ausgeführt, um einen Plan im Plancache zu erzeugen. Dabei wird davon ausgegangen, dass der erzeugte Plan dem gewünschten Plan entspricht und keine weitere Optimierung der Abfrage erforderlich ist. Der XML-Showplan wird durch eine Abfrage der dynamischen Verwaltungssichten `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`und `sys.dm_exec_text_query_plan` sys.dm_exec_query_stats abgerufen und der Variablen `@xml_showplan` zugewiesen. Die `@xml_showplan` -Variable wird dann im `sp_create_plan_guide` -Parameter an die `@hints` -Anweisung übergeben. Alternativ können Sie die gespeicherte Prozedur [sp_create_plan_guide_from_handle](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql) verwenden, um eine Planhinweisliste aus einem Abfrageplan im Plancache zu erstellen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  