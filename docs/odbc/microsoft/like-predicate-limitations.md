---
title: WIE Prädikat Einschränkungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119709"
---
# <a name="like-predicate-limitations"></a>Einschränkungen des LIKE-Prädikats
Wenn Daten in einer Spalte mehr als 255 Zeichen ist, wird der Vergleich mit LIKE nur auf die ersten 255 Zeichen basieren.  
  
 Eine ähnliche verwendet wird, eine Prozedur wird nur mit Konstantenmuster unterstützt. Die Desktop-Datenbanktreiber unterstützt SQL-92 wie Mustervergleich.  
  
 Verwenden einer Escape-Klausel in einer LIKE-Prädikat wird nicht unterstützt.  
  
 Ein Vergleich mit LIKE sollte nicht für eine Spalte mit Daten eines Datentyps der numerischen oder "float" ausgeführt werden. Die Ergebnisse möglicherweise nicht vorhersehbar sein. Weitere Informationen finden Sie unter den *Microsoft Jet-Datenbank-Engine Handbuch für Programmierer*.
