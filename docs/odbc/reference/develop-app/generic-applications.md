---
title: Allgemeiner Anwendungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6b1544f5562468db03a649c263993039a722a3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139300"
---
# <a name="generic-applications"></a>Allgemeine Anwendungen
Allgemeine Anwendungen manchmal eine hartcodierte Aufgabe ausführen, z. B. als Kalkulationstabelle, die Abrufen von Daten aus einer Datenbank. Sie können auch eine Vielzahl von benutzerdefinierten Aufgaben, z. B. eine Standardabfrage-Anwendung, die der Benutzer zum eingeben und Ausführen einer SQL-Anweisung ausführen. Was allgemeine Anwendungen gemeinsam haben, ist, dass sie mit einer Vielzahl von verschiedenen DBMS-Systeme funktionieren müssen und der Entwickler nicht im Voraus weiß, welche diese DBMS werden.  
  
 Aus diesem Grund müssen allgemeine Anwendungen hochgradig interoperabel sein. Der Entwickler muss stellen viele Optionen, trading aus Interoperabilität für Funktionen, und muss Code schreiben, der erwartet, Treiber dass, um eine Vielzahl von Funktionen zu unterstützen. Während allgemeine Anwendungen optimiert werden können, um mit beliebten DBMS zu arbeiten, enthalten sie selten treiberspezifische oder DBMS-spezifischen Code.
