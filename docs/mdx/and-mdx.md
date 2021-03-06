---
title: UND (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 930fe19abe7b1d783b4c69ef54b9b2550a05d538
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017095"
---
# <a name="and-mdx"></a>AND (MDX)


  Führt eine logische Konjunktion zweier numerischer Ausdrücke aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parameter  
 *Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen numerischen Wert zurückgibt.  
  
 *Expression2*  
 Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der gibt "true", wenn beide Parameter ausgewertet **"true"** ist, andernfalls **"false"** .  
  
## <a name="remarks"></a>Hinweise  
 Die **und** -Operator behandelt beide Ausdrücke als boolesche Werte (null, 0 (null) als **"false"** ist, andernfalls **"true"** ), bevor der Operator die logische Konjunktion ausführt. In der folgende Tabelle wird veranschaulicht, wie die **und** -Operator führt die logische Konjunktion.  
  
|*Expression1*|*Expression2*|Rückgabewert|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**false**|  
|**false**|**true**|**false**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Beispiel  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for clothing sales where the GPM is between 20% and 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .3 AND   
      [Measures].[Gross Profit Margin] >= .2,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT NON EMPTY  
    [Sales Territory].[Sales Territory Country].Members ON 0,  
    [Product].[Category].[Clothing] ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
