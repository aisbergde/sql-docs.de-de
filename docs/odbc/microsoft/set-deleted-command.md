---
title: Befehl SET DELETED | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997735"
---
# <a name="set-deleted-command"></a>SET DELETED-Befehl
Gibt an, ob zum Löschen markierte Datensätze verarbeitet wurden und ob sie für die Verwendung in anderen Befehlen verfügbar.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 (Standard für den Treiber; der Standardwert für Visual FoxPro ist OFF). Gibt an, die Befehle, die ausgeführt werden (einschließlich der Datensätze in verknüpften Tabellen) Datensätze mit einem Bereich zum Löschen markierte Einträge ignoriert.  
  
 OFF  
 Gibt an, dass Datensätze markiert, für das Löschen von Befehlen zugegriffen werden kann, die auf Datensätze (einschließlich der Datensätze in verknüpften Tabellen) verwendet werden. verwenden einen Bereich.  
  
## <a name="remarks"></a>Hinweise  
 Fragt, dass verwenden (gelöscht), zum Testen des Status von Datensätzen mithilfe von Visual FoxPro-Rushmore-Technologie, wenn die Tabelle indiziert ist, auf die gelöschte () optimiert werden kann.  
  
> [!IMPORTANT]  
>  Legen Sie gelöscht wird ignoriert, wenn der Standardbereich für den Befehl des aktuellen Datensatzes ist oder wenn Sie einen Bereich eines einzelnen Datensatzes einschließen. INDEX wird immer ignoriert wird, legen Sie gelöscht und alle Datensätze in der Tabelle indiziert.  
  
## <a name="see-also"></a>Siehe auch  
 [DELETE (SQL-Befehl)](../../odbc/microsoft/delete-sql-command.md)
