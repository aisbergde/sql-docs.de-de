---
title: Einschränkungen der CREATE TABLE Anweisung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db5d2cb8decde9828acd3005551717ac9f6cef32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096592"
---
# <a name="create-table-statement-limitations"></a>Einschränkungen der CREATE TABLE-Anweisung
Wenn die Microsoft Access, Microsoft Excel oder Paradoxdriver verwendet wird, und die Länge einer Spalte Text- oder Binärformat nicht angegeben ist (oder als 0 angegeben ist), wird die Länge der Spalte auf 255 festgelegt.  
  
 Wenn die dBASE-Treiber verwendet wird, und die Länge einer Spalte Text- oder Binärformat nicht angegeben ist (oder als 0 angegeben ist), werden die Spaltenlänge und 254 festgelegt.  
  
 Es wird ein Maximum von 255 Spalten unterstützt.  
  
 Wenn der Microsoft Excel-Treiber auf einem keine Microsoft Excel 5.0, 7.0, oder ein Arbeitsblatt 97-Datenquelle verwendet wird kann nicht mit dem gleichen Namen wie einem Arbeitsblatt erstellt werden, die zuvor gelöscht wurde. Wenn der Microsoft Excel-Treiber auf einem Arbeitsblatt Version 5.0, 7.0 oder 97 verwendet wird, wird eine DROP TABLE-Anweisung löscht das Arbeitsblatt, aber den Arbeitsblattnamen werden nicht gelöscht.  
  
 Wenn die Paradox-Treiber verwendet wird, können keine Spalten hinzugefügt werden, nachdem ein Index für eine Tabelle definiert wurde. Wenn die erste Spalte der Argumentliste einer CREATE TABLE-Anweisung einen Index erstellt wird, kann keine zweite Spalte in der Argumentliste enthalten sein.
