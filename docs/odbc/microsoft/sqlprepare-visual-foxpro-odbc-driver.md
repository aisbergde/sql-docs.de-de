---
title: SQLPrepare (Visual FoxPro-ODBC-Treiber) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5835ddaf27d097dcfff608649f50c1f7f41a93df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996303"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro-ODBC-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Visual FoxPro-ODBC-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC-API-Referenz](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Unterstützung: Vollständig  
  
 ODBC-API-Übereinstimmung: Kern-Ebene  
  
 Bereitet eine SQL-Anweisung durch die Planung So optimieren, und führen Sie die Anweisung vor. Die SQL-Anweisung kompiliert wird, für die Ausführung von [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 Wenn Ihre Tabelle, Sicht oder Feldnamen Leerzeichen enthalten, schließen Sie die Namen im Anführungszeichen (') ein. Z. B. wenn die Datenbank eine Tabelle namens "Meine Tabelle" und "das Feld mein Feld enthält, müssen Sie jedes Element des Bezeichners wie folgt:  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 Weitere Informationen finden Sie unter [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) in die *ODBC Programmer's Reference*.
