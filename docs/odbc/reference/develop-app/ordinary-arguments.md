---
title: Normale Argumente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 997604b4376656d36d2bc4bc31f1959aa6c8a229
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987826"
---
# <a name="ordinary-arguments"></a>Normale Argumente
Wenn ein Zeichenfolgenargument für Katalog-Funktion ein normales Argument ist, wird es als Zeichenfolgenliteral behandelt. Ein normales Argument akzeptiert, weder ein Zeichenfolgenmuster für die Suche als auch eine Liste von Werten. Ein normales Argument die Groß-/Kleinschreibung spielt und Anführungszeichen in der Zeichenfolge wörtlich genommen werden. Diese Argumente werden als normale Argumente behandelt, wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_FALSE festgelegt ist; Sie werden stattdessen als bezeichnerargumente behandelt, wenn dieses Attribut auf SQL_TRUE festgelegt ist.  
  
 Wenn ein normales Argument auf einen null-Zeiger festgelegt ist, und das Argument ein erforderliches Argument ist, gibt die Funktion SQL_ERROR zurück, und SQLSTATE HY009 (Ungültige Verwendung von null-Zeiger). Wenn ein normales Argument auf einen null-Zeiger festgelegt ist, und das Argument kein erforderliches Argument ist, ist das Argument des Verhalten treiberabhängig. Die erforderlichen Argumente werden in der folgenden Tabelle aufgeführt.  
  
|Funktion|Erforderliche Argumente|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
