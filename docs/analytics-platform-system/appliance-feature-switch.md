---
title: Feature-Switch (Analytics Platform System)
description: Zeigt Informationen zu den zwei Features, die in Analytics Platform System AU7 eingeführt werden.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 4e9929d4729cc1027c82b61c9fab6ebfcddbd54d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961519"
---
# <a name="appliance-feature-switches"></a>Funktionsschalter Appliance

Die **Featureschalter** Seite zeigt Informationen zu den Features, die in Analytics Platform System AU7 und höher eingeführt wurden. Verwenden Sie diese Seite zu aktualisieren oder zu aktivieren/deaktivieren Features und Einstellungen in Analytics Platform System.

> [!NOTE]
> Änderungen an Werten für Feature-Switch erfordert einen Neustart des Diensts.

![DWConfig-Anwendung-Feature-Switch](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConfig-Anwendung-Feature-Switch")

## <a name="autostatsenabled"></a>AutoStatsEnabled

Steuert das statistikfeature automatisch. Dieses Feature-Switch nastaven NA hodnotu True, wird standardmäßig nach dem Upgrade auf AU7. Alle nach dem Upgrade erstellte Datenbank übernimmt die automatische Erstellung und asynchronen Aktualisieren von Statistiken. Datenbankadministratoren können für vorhandene Datenbanken automatisch Statistiken mit [ALTER DATABASE (Parallel Data Warehouse)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw). Weitere Informationen zu Statistiken finden Sie unter [Statistiken](../relational-databases/statistics/statistics.md).

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

Wählen Sie die Maxdop-Einstellungen, die größer als 1 für Insert/Select-Vorgänge ermöglicht. Optionen für diese Einstellung sind 0, 1, 2 und 4, Standardwert 1.

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

Verbessert die abfrageleistung durch Eliminierung der datenverschiebung für allgemeine Teilausdruck in SQL-Abfrageoptimierer. Ausführliche Erläuterung dieser Funktion finden Sie [hier](common-sub-expression-elimination.md).

## <a name="usecatalogqueries"></a>UseCatalogQueries

Mithilfe von Katalogobjekten für einige Metadaten-Aufrufe anstelle von SMO wurde die Verbesserung der Leistung erläutert. Auf "true" in CU7.1, diese Option standardmäßig festgelegt ist, steuert dieses Verhalten.

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

Steuert die Zeit, die Data Movement Service (DMS) wartet auf einem ausgelasteten System synchronisiert werden soll, wenn eine Abfrage, die im Zusammenhang mit der datenverschiebung abgebrochen wird. Aktualisieren auf AU7 wird standardmäßig dieser Wert auf 900 Sekunden (15 Minuten). Der gültige Bereich ist 0 – 3600 Sekunden.
