---
title: CREATE SET-Anweisung (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f8d522f7832a280aa8b280bbe912640b566974a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893744"
---
# <a name="mdx-data-definition---create-set"></a>MDX-Datendefinition – CREATE SET


  Erstellt eine benannte Menge mit Sitzungsbereich für den aktuellen Cube.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen des Cubes bereitstellt.  
  
 *Set_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Namen für die zu erstellende benannte Menge bereitstellt.  
  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Property_Name*  
 Eine gültige Zeichenfolge, die den Namen einer Mengeneigenschaft bereitstellt.  
  
 *Property_Value*  
 Ein gültiger Skalarausdruck, der den Wert der Mengeneigenschaft definiert.  
  
## <a name="remarks"></a>Hinweise  
 Eine benannte Menge ist eine Menge von Dimensionselementen (oder ein Ausdruck, der eine Menge definiert), die Sie erstellen, um sie später wieder zu verwenden. Mit einer benannten Menge können Sie beispielsweise eine Menge von Dimensionselementen definieren, die aus den 10 umsatzstärksten Geschäften besteht. Diese Menge kann statisch oder mithilfe einer Funktion wie [TopCount](../mdx/topcount-mdx.md)definiert werden. Diese benannte Menge kann dann überall verwendet werden, wo die Menge der ersten 10 Geschäfte benötigt wird.  
  
 Die CREATE SET-Anweisung erstellt eine benannte Menge, die während der gesamten Sitzung verfügbar bleibt und somit in mehreren Abfragen innerhalb einer Sitzung verwendet werden kann. Weitere Informationen finden Sie unter [Erstellen &#40;von MDX&#41;-Elementen für berechnete](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members)Elemente im Sitzungs Bereich.  
  
 Sie können auch eine benannte Menge zum Verwenden in einer einzelnen Abfrage definieren. Zur Definition einer solchen Menge verwenden Sie die WITH-Klausel in der SELECT-Anweisung. Weitere Informationen zur with-Klausel finden Sie unter [Erstellen von benannten Mengen &#40;mit Abfrage Bereich und MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets).  
  
 Die *set_expression* -Klausel kann jede beliebige Funktion enthalten, die MDX-Syntax unterstützt. Mengen, die mit der CREATE SET-Anweisung ohne Angabe der SESSION-Klausel erstellt wurden, haben die Sitzung als Bereich. Verwenden Sie die WITH-Klausel, um eine Menge mit Abfragebereich zu erstellen.  
  
 Die Angabe eines anderen als des aktuell verbundenen Cubes verursacht einen Fehler. Daher sollten Sie den aktuellen Cube mithilfe von CURRENTCUBE statt mit dem Cubenamen angeben.  
  
## <a name="scope"></a>Bereich  
 Eine benutzerdefinierte Menge kann in einem der Bereiche auftreten, die in der folgenden Tabelle aufgeführt sind.  
  
 Bereich einer Abfrage  
 Die Sichtbarkeit und Lebensdauer der Menge ist auf die Abfrage beschränkt. Die Menge ist in einer einzelnen Abfrage definiert. Der Abfragebereich hat Vorrang vor dem Sitzungsbereich. Weitere Informationen finden Sie unter [Erstellen von benannten Mengen mit benannten Mengen &#40;(MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets)).  
  
 Bereich einer Sitzung  
 Die Sichtbarkeit und Lebensdauer der Menge ist auf die Sitzung beschränkt, in der die Menge erstellt wurde. (Die Lebensdauer ist kleiner als die Sitzungsdauer, wenn eine Drop Set-Anweisung für die Menge ausgegeben wird.) Die CREATE SET-Anweisung erstellt eine Menge mit Sitzungs Bereich. Verwenden Sie die WITH-Klausel, um eine Menge mit Abfragebereich zu erstellen.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Menge mit dem Namen Core Products erstellt. Die SELECT-Abfrage veranschaulicht, wie die neu erstellte Menge aufgerufen wird. Die CREATE SET-Anweisung muss vor der SELECT-Abfrage ausgeführt werden – es können nicht beide im gleichen Batch ausgeführt werden.  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>Mengenauswertung  
 Die Mengenauswertung kann so definiert werden, dass sie auf unterschiedliche Weise ausgeführt wird, nämlich entweder einmal bei der Mengenerstellung oder bei jeder Verwendung der Menge.  
  
 STATIC  
 Gibt an, dass die Menge nur einmal ausgewertet wird, nämlich, wenn die CREATE SET-Anweisung ausgewertet wird.  
  
 DYNAMIC  
 Gibt an, dass die Menge bei jeder Verwendung in einer Abfrage ausgewertet wird.  
  
## <a name="set-visibility"></a>Sichtbarkeit der Menge  
 Die Menge kann für andere Benutzer, die den Cube abfragen, sichtbar oder unsichtbar sein.  
  
 HIDDEN  
 Gibt an, dass die Menge für Benutzer, die den Cube abfragen, nicht sichtbar ist.  
  
## <a name="standard-properties"></a>Standardeigenschaften  
 Jede Menge verfügt über Standardeigenschaften. Wenn eine Client Anwendung mit [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]verbunden ist, werden die Standardeigenschaften entweder unterstützt, oder Sie können unterstützt werden, wenn der Administrator dies auswählt.  
  
|Eigenschaftsbezeichner|Bedeutung|  
|-------------------------|-------------|  
|CAPTION|Eine Zeichenfolge, die von der Clientanwendung als Beschriftung für die Menge verwendet wird.|  
|DISPLAY_FOLDER|Eine Zeichenfolge, die den Pfad des Anzeigeordners angibt, der von der Clientanwendung zum Anzeigen der Menge verwendet wird. Das Trennzeichen für Ordnerebenen wird von der Clientanwendung definiert. Bei den von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]bereitgestellten Tools und Clients ist der umgekehrte schräg\\Strich () das ebenendtrennzeichen. Um mehrere Anzeigeordner für eine definierte Menge bereitzustellen, verwenden Sie ein Semikolon (;) als Trennzeichen für die Ordner.|  
  
## <a name="see-also"></a>Siehe auch  
 [Drop Set- &#40;Anweisung (MDX)&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [MDX für MDX &#40;-Daten Definitions Anweisungen&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
