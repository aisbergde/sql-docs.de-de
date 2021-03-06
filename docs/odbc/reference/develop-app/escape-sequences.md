---
title: Escapesequenzen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001372"
---
# <a name="escape-sequences"></a>Escapesequenzen
ODBC definiert Escapesequenzen, die mit der standard-Grammatik für Datum, Uhrzeit, Zeitstempel und Datetime-Intervall-Literale, Aufrufe von Skalarfunktionen, **wie** Escape-Zeichen, äußere Joins und Prozeduraufrufe-Prädikat. Interoperable Anwendungen ausführen können, sollten diese Sequenzen an, wann immer möglich verwenden.  
  
 Um festzustellen, ob ein Treiber die Escapesequenzen für Datum, Uhrzeit, Timestamp- oder Datetime-Intervall-Literale unterstützt, eine Anwendung ruft **SQLGetTypeInfo**. Wenn die Datenquelle ein Datum, Uhrzeit, Timestamp- oder Datetime-Intervall-Datentyp unterstützt, muss es auch die entsprechende Escapesequenz unterstützen. Um zu bestimmen, ob die anderen Escapesequenzen unterstützt werden, eine Anwendung ruft **SQLGetInfo**.  
  
 Weitere Informationen finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)weiter unten in diesem Abschnitt.
