---
title: Aufrufen von SQLCloseCursor | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 447a0892049317813fa9fe6986e6219922a11e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068692"
---
# <a name="calling-sqlclosecursor"></a>Aufrufen von SQLCloseCursor
Da **SQLCloseCursor** ist fast identisch mit **SQLFreeStmt** mit SQL_CLOSE, führt der Treiber-Manager diese Funktion nicht zugeordnet. Ersatzfunktionen zugeordnet sind, sodass vorhandene ODBC *2.x* Anwendungen können ganz einfach in ODBC verschieben *3.x* mithilfe der neuen Funktionen. Eine solche Verschiebung erleichtert das für solche Anwendungen, auf die Verwendung neuer ODBC *3.x* -Funktionen in bedingten Code auf modulare Weise. **SQLCloseCursor** stellt keine neuen Funktionen dar. Eine Anwendung ist nicht bietet alle Vorteile Wechsel zur **SQLCloseCursor** aus **SQLFreeStmt** mit SQL_CLOSE.
