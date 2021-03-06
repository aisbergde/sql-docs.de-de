---
title: Zeile Status | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057107"
---
# <a name="row-status"></a>Zeilenstatus
> [!IMPORTANT]  
>  Dieses Feature wird in einer zukünftigen Version von Windows entfernt werden. Zu vermeiden Sie, verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Änderung von Anwendungen, die derzeit auf dieses Feature verwenden möchten. Microsoft empfiehlt die Verwendung von Cursor-Funktionalität des Treibers.  
  
 Die Cursorbibliothek erstellt einen Puffer in den Cache für den Zeilenstatus. Die Cursorbibliothek Ruft Werte für die zeilenstatusarray (angegeben mit der SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut) aus diesen Puffer ab. Für jede Zeile wird die Cursorbibliothek auf diesen Puffer festgelegt:  
  
-   SQL_ROW_DELETED, die beim Ausführen einer positionierte delete-Anweisung in der Zeile.  
  
-   SQL_ROW_ERROR beim Auftreten eines Fehlers beim Abrufen der zeilenupdates aus der Datenquelle mit **SQLFetch**.  
  
-   SQL_ROW_SUCCESS, wenn sie die Zeile wurde erfolgreich aus der Datenquelle mit abruft **SQLFetch**.  
  
-   SQL_ROW_UPDATED, wenn es eine positioniertes Update-Anweisung, in der Zeile ausführt.
