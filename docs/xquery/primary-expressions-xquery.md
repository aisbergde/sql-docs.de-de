---
title: Primärausdrücke (XQuery) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
author: rothja
ms.author: jroth
ms.openlocfilehash: e8704a01d810477fd0359196cb622984da357cf6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946382"
---
# <a name="primary-expressions-xquery"></a>Primärausdrücke (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die XQuery-Primärausdrücke umfassen Literale, Variablenverweise, Kontextelementausdrücke, Konstruktoren und Funktionsaufrufe.  
  
## <a name="literals"></a>Literale  
 XQuery-Literale können numerische oder Zeichenfolgenliterale sein. Ein Zeichenfolgenliteral kann vordefinierte Entitätsverweise enthalten; ein Entitätsverweis ist eine Abfolge von Zeichen. Die Abfolge beginnt mit einem kaufmännischen Und-Zeichen, das ein einzelnes Zeichen darstellt, das anderenfalls syntaktische Signifikanz besitzen könnte. Darauf folgen die vordefinierten Entitätsverweise für XQuery.  
  
|Entitätsverweis|repräsentiert|  
|----------------------|----------------|  
|&lt;|\<|  
|&gt;|>|  
|&amp;|&|  
|&quot;|"|  
|&apos;|'|  
  
 Ein Zeichenfolgenliteral kann auch einen Zeichenverweis enthalten, einen Verweis im XML-Stil auf ein Unicode-Zeichen, das durch seinen dezimalen oder hexadezimalen Codepunkt identifiziert wird. Beispielsweise kann das Euro-Symbol dargestellt werden, durch den Zeichenverweis "&\#8364;".  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet XML, Version 1.0, als Basis für die Analyse.  
  
### <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen die Verwendung von Literalen sowie Entitäts- und Zeichenverweisen.  
  
 Dieser Code gibt einen Fehler zurück, weil die Zeichen `<'` und `'>` eine besondere Bedeutung besitzen.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 Wenn Sie stattdessen einen Entitätsverweis verwenden, funktioniert die Abfrage:  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 Das folgende Beispiel zeigt die Verwendung eines Zeichenverweises zur Darstellung des Euro-Symbols.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 Dies ist das Ergebnis.  
  
 `<a>€12.50</a>`  
  
 Im folgenden Beispiel wird die Abfrage durch Apostrophe getrennt. Daher wird der Apostroph im Zeichenfolgenwert durch zwei aufeinanderfolgende Apostrophe dargestellt.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 Dies ist das Ergebnis.  
  
 `<a>I don't know</a>`  
  
 Die integrierten booleschen Funktionen **True()"** und **" false()""** , zur Darstellung boolescher Werte verwendet werden können, wie im folgenden Beispiel gezeigt.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 Der direkte Elementkonstruktor gibt einen Ausdruck in geschweiften Klammern an. Dieser wird durch seinen Wert im sich ergebenden XML ersetzt.  
  
 Dies ist das Ergebnis.  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>Variablenverweise  
 Ein Variablenverweis in XQuery ist ein QName, dem ein $-Zeichen vorangestellt wurde. Diese Implementierung unterstützt nur Variablenverweise ohne Präfix. Die folgende Abfrage definiert z. B. die Variable `$i` im FLWOR-Ausdruck:  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 Die folgende Abfrage funktioniert nicht, weil dem Variablennamen ein Namespacepräfix hinzugefügt wurde.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="https://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 Sie können der SQL:Variable()-Funktion-Erweiterung verwenden, zum Verweisen auf SQL-Variablen, wie in der folgenden Abfrage gezeigt.  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 Dies ist das Ergebnis.  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Implementierungseinschränkungen sind zu beachten:  
  
-   Variablen mit Namespacepräfixen werden nicht unterstützt.  
  
-   Modulimport wird nicht unterstützt.  
  
-   Externe Variablendeklarationen werden nicht unterstützt. Dies ist die Verwendung der [SQL:Variable()-Funktion](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="context-item-expressions"></a>Kontextelementausdrücke  
 Das Kontextelement ist das Element, das aktuell im Kontext eines path-Ausdrucks verarbeitet wird. Es wird in einer XML-Datentypinstanz ungleich NULL mit dem Dokumentknoten initialisiert. Sie können auch von der Nodes()-Methode, im Kontext von XPath-Ausdrücken oder []-Prädikaten geändert werden.  
  
 Das Kontextelement wird von einem Ausdruck zurückgegeben, der einen Punkt (.) enthält. Die folgende Abfrage wird beispielsweise aus jedem Element <`a`> auf das Vorhandensein des Attributs `attr`. Wenn das Attribut vorhanden ist, wird das Element zurückgegeben. Beachten Sie, dass die Bedingung im Prädikat angibt, dass der Kontextknoten durch einen einzelnen Punkt angegeben wird.  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 Dies ist das Ergebnis.  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>Funktionsaufrufe  
 Sie können integrierte XQuery-Funktionen aufrufen und die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] SQL:Variable() und SQL:Column() Funktionen. Eine Liste der implementierten Funktionen, finden Sie unter [XQuery-Funktionen für den Xml-Datentyp](../xquery/xquery-functions-against-the-xml-data-type.md).  
  
#### <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Implementierungseinschränkungen sind zu beachten:  
  
-   Funktionsdeklaration im XQuery-Prolog wird nicht unterstützt.  
  
-   Funktionsimport wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Konstruktion &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
