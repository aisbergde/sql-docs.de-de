---
title: Datamining-Erweiterungen (DMX)-Funktionsreferenz | Microsoft-Dokumentation
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d57ac2db4149178a61424affef5e8948de0063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070956"
---
# <a name="data-mining-extensions-dmx-function-reference"></a>Data Mining-Erweiterungen (DMX) - Funktionsreferenz
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] werden mehrere Funktionen in der Sprache Data Mining-Erweiterungen (Data Mining Extensions, DMX) unterstützt. Die Funktionen erweitern die Ergebnisse einer Vorhersageabfrage, sodass diese Informationen enthalten, die die Vorhersage näher beschreiben. Darüber hinaus steuern die Funktionen, wie die Ergebnisse der Vorhersage zurückgegeben werden. In der folgenden Tabelle werden Links zu Ressourcen bereitgestellt, die erläutern, wie Funktionen in DMX verwendet werden.  
  
|Funktion|Beschreibung|  
|--------------|-----------------|  
|[Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)|Listet Funktionen auf, die mit allen Modelltypen verwendet werden können, und stellt Links zu weiteren Informationen bereit, wie bestimmte Typen von Miningmodellen abgefragt werden.|  
|[Structure and Usage of DMX Prediction Queries (Struktur und Verwendung von DMX-Vorhersageabfragen)](../dmx/structure-and-usage-of-dmx-prediction-queries.md)|Stellt eine Übersicht bereit, wie eine Vorhersageabfrage unter Verwendung von DMX erstellt wird.|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Gibt eine Tabelle zurück, die eine bestimmte Anzahl von untersten Zeilen in aufsteigender Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
  
 In der folgenden Tabelle sind die Funktionen aufgeführt, die DMX unterstützt.  
  
|Funktion|Beschreibung|  
|--------------|-----------------|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|Gibt eine Tabelle zurück, die in aufsteigender Reihenfolge auf der Grundlage eines Rangausdrucks die letzten &lt;n&gt; Elementzeilen des Tabellenausdrucks enthält.|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|Gibt eine Tabelle zurück, die die kleinste Anzahl von untersten Zeilen, die einem angegebenen Prozentausdruck entsprechen, in aufsteigender Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
|[BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)|Gibt eine Tabelle zurück, die die kleinste Anzahl von untersten Zeilen, die einem angegebenen Summenausdruck entsprechen, in aufsteigender Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
|[Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)|Gibt den Cluster zurück, der mit der höchsten Wahrscheinlichkeit den Eingabefall enthält.|  
|[ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)|Gibt die Wahrscheinlichkeit zurück, mit der der Eingabefall zum Cluster gehört.|  
|[Vorhanden &#40;DMX&#41;](../dmx/exists-dmx.md)|Gibt "True" zurück, wenn das von der angegebenen SELECT-Anweisung zurückgegebene Ergebnis mindestens eine Zeile enthält.|  
|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Zeigt an, ob der aktuelle Knoten ein untergeordneter Knoten des angegebenen Knotens ist.|  
|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|Zeigt an, ob der angegebene Knoten den Fall enthält.|  
|[IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|Gibt an, ob ein Fall zu der Menge der Testfälle gehört.|  
|[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)|Gibt an, ob ein Fall zu der Menge der Trainingsfälle gehört.|  
|[Lag &#40;DMX&#41;](../dmx/lag-dmx.md)|Gibt die Zeitscheibe zwischen dem Datum des aktuellen Falls und dem letzten Datum in den Daten zurück.|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|Führt eine Vorhersage für eine angegebene Spalte aus.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)|Gibt die angepasste Wahrscheinlichkeit für die angegebene vorhersagbare Spalte zurück.|  
|[PredictAssociation &#40;DMX&#41;](../dmx/predictassociation-dmx.md)|Sagt eine assoziative Mitgliedschaft in einer Spalte voraus.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md)|Gibt die Wahrscheinlichkeit, die ein Eingabefall in das vorhandene Modell passen. Diese Funktion kann nur mit Clustermodellen verwendet werden.|  
|[PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md)|Gibt eine Tabelle zurück, die dem Histogramm für eine angegebene Spalte entspricht.|  
|[PredictNodeId &#40;DMX&#41;](../dmx/predictnodeid-dmx.md)|Gibt die Knoten-ID für einen ausgewählten Fall zurück.|  
|[PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)|Gibt die Wahrscheinlichkeit für die angegebene Spalte zurück.|  
|[PredictSequence &#40;DMX&#41;](../dmx/predictsequence-dmx.md)|Sagt die nächsten Werte in einer Reihenfolge voraus.|  
|[PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)|Ruft den Wert für die Standardabweichung einer angegebenen Spalte ab.|  
|[PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)|Gibt den Unterstützungswert der Spalte zurück.|  
|[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)|Sagt die zukünftigen Werte für eine Zeitreihe voraus.|  
|[PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)|Gibt den Wert für die Varianz der angegebenen Spalte zurück.|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Gibt den oberen Wert des vorhergesagten Buckets zurück, der für eine angegebene diskretisierte Spalte ermittelt wird.|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)|Gibt den mittleren Wert des vorhergesagten Buckets zurück, der für eine angegebene diskretisierte Spalte ermittelt wird.|  
|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|Gibt den unteren Wert des vorhergesagten Buckets zurück, der für eine angegebene diskretisierte Spalte ermittelt wird.|  
|[StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)|Gibt den Wert der festgelegten Miningstrukturspalte der Tabelle an.|  
|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|Gibt eine Tabelle zurück, die eine bestimmte Anzahl von obersten Zeilen in einer absteigenden Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|Gibt eine Tabelle zurück, die die kleinste Anzahl von obersten Zeilen, die einem angegebenen Prozentausdruck entsprechen, in einer absteigenden Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|Gibt eine Tabelle zurück, die die kleinste Anzahl von obersten Zeilen, die einem angegebenen Summenausdruck entsprechen, in einer absteigenden Rangreihenfolge auf der Grundlage eines Rangausdrucks enthält.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40;DMX&#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; -Syntaxkonventionen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Syntaxelemente](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struktur und Verwendung von DMX-Vorhersageabfragen](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Understanding the DMX Select Statement (Grundlegendes zur SELECT-Anweisung)](../dmx/understanding-the-dmx-select-statement.md)  
  
  
