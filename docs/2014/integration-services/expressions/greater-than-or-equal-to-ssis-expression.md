---
title: '&gt;= (Größer als oder gleich) (SSIS-Ausdruck) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- <= (less than or equal to operator)
- greater than or equal to (>=)
ms.assetid: 52ad504d-2f54-44de-b5e2-620577c0e289
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e4db32776e59c6100594933fd8706129e8652790
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769011"
---
# <a name="gt-greater-than-or-equal-to-ssis-expression"></a>&gt;= (Größer als oder gleich) (SSIS-Ausdruck)
  Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck größer oder gleich dem zweiten Ausdruck ist. Die Ausdrucksauswertung konvertiert viele Datentypen automatisch vor dem Vergleich.  
  
> [!NOTE]  
>  Vergleiche, die die Datentypen DT_TEXT, DT_NTEXT oder DT_IMAGE verwenden, werden von diesem Operator nicht unterstützt.  
  
 Für manche Datentypen muss jedoch der Ausdruck eine explizite Umwandlung einschließen, damit der Ausdruck erfolgreich ausgewertet werden kann. Weitere Informationen zu zulässigen Datentypumwandlungen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](cast-ssis-expression.md).  
  
> [!NOTE]  
>  Zwischen den beiden Zeichen in diesem Operator sind keine Leerzeichen vorhanden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
expression1 >= expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *expression1, expression2*  
 Ein gültiger Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_BOOL  
  
## <a name="remarks"></a>Hinweise  
 Wenn einer der Ausdrücke im Vergleich NULL ist, ist das Ergebnis des Vergleichs NULL. Wenn beide Ausdrücke NULL sind, ist das Ergebnis NULL.  
  
 Für die Ausdrucksgruppe ( *expression1* und *expression2*) muss eine der folgenden Regeln eingehalten werden:  
  
-   **Numerisch**   *expression1* und *expression2* müssen einen numerischen Datentyp aufweisen. Die Schnittmenge der Datentypen muss ein numerischer Datentyp gemäß den Regeln zu den impliziten numerischen Konvertierungen sein, die die Ausdrucksauswertung ausführt. Die Schnittmenge der beiden numerischen Datentypen darf nicht NULL sein. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
-   **Zeichen** : *expression1* und *expression2* müssen zu einem der Datentypen DT_STR oder DT_WSTR ausgewertet werden. Die beiden Ausdrücke können zu verschiedenen Zeichenfolgen-Datentypen ausgewertet werden.  
  
    > [!NOTE]  
    >  Bei Zeichenfolgenvergleichen wird nach Groß-/Kleinschreibung, Akzent, Kana und Breite unterschieden.  
  
-   **Date, Time oder Date/Time** Sowohl *expression1* als auch *expression2* muss in einen der folgenden Datentypen ausgewertet werden: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET oder DT_FILETIME.  
  
    > [!NOTE]  
    >  Das System unterstützt keine Vergleiche zwischen einem Ausdruck, der zu einem Uhrzeitdatentyp ausgewertet wird, und einem Ausdruck, der entweder zu einem Datums- oder zu einem Datums-/Uhrzeitdatentyp ausgewertet wird. In diesem Fall wird ein Fehler generiert.  
  
     Beim Vergleich der Ausdrücke werden die folgenden Konvertierungsregeln in der angegebenen Reihenfolge angewendet:  
  
    -   Wenn zwei Ausdrücke zu dem gleichen Datentyp ausgewertet werden, wird der Datentyp verglichen.  
  
    -   Wenn ein Ausdruck den DT_DBTIMESTAMPOFFSET-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIMESTAMPOFFSET konvertiert, und ein DT_DBTIMESTAMPOFFSET-Vergleich wird ausgeführt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
    -   Wenn ein Ausdruck den DT_DBTIMESTAMP2-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIMESTAMP2 konvertiert, und ein DT_DBTIMESTAMP2-Vergleich wird ausgeführt.  
  
    -   Wenn ein Ausdruck den DT_DBTIME2-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIME2 konvertiert, und ein DT_DBTIME2-Vergleich wird ausgeführt.  
  
    -   Wenn ein Ausdruck einen anderen Datentyp als DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 oder DT_DBTIME2 aufweist, werden die Ausdrücke vor dem Vergleichen in den DT_DBTIMESTAMP-Datentyp konvertiert.  
  
     Beim Vergleichen der Ausdrücke gelten folgende Annahmen:  
  
    -   Wenn jeder Ausdruck einen Datentyp aufweist, der Millisekunden umfasst, wird angenommen, dass bei dem Datentyp mit der geringsten Anzahl von Ziffern für Millisekunden die verbleibenden Ziffern Nullen sind.  
  
    -   Wenn jeder Ausdruck einen Datumsdatentyp aufweist, jedoch nur ein Ausdruck einen Zeitzonenoffset umfasst, wird angenommen, dass der Datumsdatentyp ohne Zeitzonenoffset in koordinierter Weltzeit (Coordinated Universal Time; UTC) ausgedrückt ist.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird zu TRUE ausgewertet, falls das aktuelle Datum der 4. Juli 2003 oder davor ist. Weitere Informationen finden Sie unter [GETDATE &#40;SSIS-Ausdruck&#41;](getdate-ssis-expression.md).  
  
```  
"7/4/2003" >= GETDATE()  
```  
  
 In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert in der **ListPrice** -Spalte größer oder gleich 500 ist.  
  
```  
ListPrice >= 500  
```  
  
 In diesem Beispiel wird die **LPrice**-Variable verwendet. Es wird zu TRUE ausgewertet, falls der Wert in der **LPrice** -Spalte größer oder gleich 500 ist. Der Datentyp der Variablen muss numerisch sein, damit der Ausdruck analysiert wird.  
  
```  
@LPrice >= 500  
```  
  
## <a name="see-also"></a>Siehe auch  
 [&#62; &#40;Größer als&#41; &#40;SSIS-Ausdruck&#41;](greater-than-ssis-expression.md)   
 [&#60; &#40;Kleiner als&#41; &#40;SSIS-Ausdruck&#41;](less-than-ssis-expression.md)   
 [&#60;= &#40;Kleiner als oder gleich&#41; &#40;SSIS-Ausdruck&#41;](less-than-or-equal-to-ssis-expression.md)   
 [Operatorenrangfolge und -assoziativität](operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](operators-ssis-expression.md)  
  
  
