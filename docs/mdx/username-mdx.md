---
title: UserName (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097274"
---
# <a name="username-mdx"></a>UserName (MDX)


  Gibt den Domänennamen und den Benutzernamen der aktuellen Verbindung zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>Hinweise  
 Der zurückgegebene Wert ist eine Zeichenfolge folgenden Formats:  
  
 *domain-name\user-name*  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Benutzername des Benutzers zurückgegeben, der die Abfrage ausführt.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
