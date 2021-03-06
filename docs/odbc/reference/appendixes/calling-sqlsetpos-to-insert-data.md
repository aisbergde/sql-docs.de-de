---
title: Aufrufen von SQLSetPos zum Einfügen von Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037716"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Aufrufen von SQLSetPos zum Einfügen von Daten
Wenn eine ODBC *2.x* arbeiten mit einer ODBC-Anwendung *3.x* Treiber ruft **SQLSetPos** mit einer *Vorgang* Argument SQL_ADD, die Treiber-Manager lässt sich dieser Aufruf nicht zuordnen **SQLBulkOperations**. Wenn eine ODBC *3.x* Treiber können auf eine Anwendung, die Aufrufe **SQLSetPos** SQL_ADD, sollten der Treiber diesen Vorgang unterstützen.  
  
 Ein wesentlicher Unterschied im Verhalten beim **SQLSetPos** aufgerufen wird und SQL_ADD tritt auf, wenn sie sich im Zustand S6 aufgerufen wird. In ODBC *2.x*, S1010 zurückgegeben beim **SQLSetPos** aufgerufen wurde, wobei SQL_ADD Status S6 (nachdem Sie mit der Cursor positioniert ist **SQLFetch**). In ODBC *3.x*, **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD kann im Zustand S6 aufgerufen werden. Ein zweite wichtigster Unterschied ist, die **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD können sein, während er sich im Zustand S5 aufgerufen, **SQLSetPos** mit eine  **Vorgang** von SQL_ADD nicht möglich. Rufen Sie für die Anweisung Übergänge, die auftreten können, für den gleichen in ODBC *3.x*, finden Sie unter [Anhang B: ODBC-Übergang Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
