---
title: '* (Multiplizieren) (DMX) | Microsoft-Dokumentation'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 840dc41afe689b7beb6af4b2272f1851fdde72e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008275"
---
# <a name="-multiply-dmx"></a>* (Multiplikation) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine arithmetische Operation aus, bei der eine Zahl mit einer anderen Zahl multipliziert wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parameter  
 *Numeric_expression*  
 Ein gültiger DMX-Ausdruck (Data Mining-Erweiterungen), der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Wert, der den Datentyp des Parameters aufweist, der in der Rangfolge höher eingestuft ist.  
  
## <a name="remarks"></a>Hinweise  
 Beide Ausdrücke müssen denselben Datentyp haben, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren. Wenn ein Ausdruck zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Arithmetische Operatoren &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Datamining-Erweiterungen &#40;DMX&#41; Operator (Referenz)](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operatoren &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
