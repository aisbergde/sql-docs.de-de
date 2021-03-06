---
title: SQLEndTran (Cursor Library) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f713f9a0c96aaf3798cf160e648404470e3a4363
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064501"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (Cursorbibliothek)
> [!IMPORTANT]  
>  Dieses Feature wird in einer zukünftigen Version von Windows entfernt werden. Zu vermeiden Sie, verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Änderung von Anwendungen, die derzeit auf dieses Feature verwenden möchten. Microsoft empfiehlt die Verwendung von Cursor-Funktionalität des Treibers.  
  
 In diesem Thema erläutert die Verwendung von der **SQLEndTran** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLEndTran**, finden Sie unter [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 Die Cursorbibliothek keine Transaktionen unterstützt, und übergibt Sie Aufrufe von **SQLEndTran** direkt an den Treiber. Die Cursorbibliothek unterstützt die Commit- und Rollback-Verhalten von Cursorn jedoch von der Datenquelle mit den Informationstypen SQL_CURSOR_ROLLBACK_BEHAVIOR und SQL_CURSOR_COMMIT_BEHAVIOR zurückgegeben:  
  
-   Für Datenquellen, die die Cursor über Transaktionen hinweg beibehalten werden, werden Änderungen, die in der Datenquelle zurückgesetzt werden nicht in die Cursorbibliothek-Cache zurückgesetzt. Damit wird den Cache mit den Daten in der Datenquelle übereinstimmen, muss die Anwendung schließen und erneut öffnen des Cursors.  
  
-   Für Datenquellen, die Schließen der Cursor an den Begrenzungen der Transaktion, die Cursorbibliothek die Cursor schließt und löscht die Zwischenspeicher für alle Anweisungen für die Verbindung.  
  
-   Für Datenquellen, die vorbereitete Anweisungen an den Begrenzungen der Transaktion zu löschen, muss die Anwendung alle vorbereitete Anweisungen für die Verbindung, bevor sie reexecuting reprepare.
