---
title: Abrufen und Aktualisieren von Rowsets (ODBC) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb0055e8ed8c17679c824fdf6cbf96c1a42c7531
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939585"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Abfragen und Aktualisieren von Rowsets (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>So können Sie Rowsets abfragen und aktualisieren  
  
1.  Rufen Sie optional [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) mit SQL_ROW_ARRAY_SIZE so ändern Sie die Anzahl der Zeilen (R) im Rowset.  
  
2.  Rufen Sie [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) oder [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) auf, um ein Rowset abzurufen.  
  
3.  Bei der Verwendung von gebundenen Spalten verwenden Sie die Datenwerte und Datenlängen, die nun in den Puffern mit gebundenen Spalten für das Rowset verfügbar sind.  
  
     Bei der Verwendung von ungebundenen Spalten rufen Sie für jede Zeile [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) mit SQL_POSITION auf, um die Cursorposition festzulegen. Gehen Sie anschließend bei jeder ungebundenen Spalte wie folgt vor:  
  
    -   Rufen Sie [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) einmal oder mehrere Male auf, um die Daten für ungebundene Spalten nach der letzten gebundenen Spalte des Rowsets abzurufen. [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) muss in zunehmender Spaltenzahlfolge aufgerufen werden.  
  
    -   Rufen Sie [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) mehrere Male auf, um Daten aus einer text- oder image-Spalte abzurufen.  
  
4.  Richten Sie alle Data-at-Execution-text- oder Data-at-Execution-image-Spalten ein.  
  
5.  Rufen Sie [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) oder [SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398) auf, um die Cursorposition festzulegen und Zeilen im Rowset zu aktualisieren, zu löschen oder hinzuzufügen.  
  
     Data-at-Execution-text- oder Data-at-Execution-image-Spalten, die zum Aktualisieren oder Hinzufügen verwendet werden, müssen verarbeitet werden.  
  
6.  Sie können eine positionierte UPDATE- oder DELETE-Anweisung ausführen und dabei den Cursornamen angeben (über [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)abrufbar) und für dieselbe Verbindung ein anderes Anweisungshandle verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Cursorn Gewusst-wie-Themen &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
