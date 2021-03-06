---
title: DIFFERENCE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe01e0d9465495cbf4943ba7867ebf262a1f3dd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135927"
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Diese Funktion gibt einen ganzzahligen Wert zurück, der den Unterschied zwischen den [SOUNDEX()](./soundex-transact-sql.md)-Werten von zwei unterschiedlichen Zeichenausdrücken misst.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*character_expression*  
Ein alphanumerischer [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der Zeichendaten. *character_expression* kann eine Konstante, Variable oder Spalte sein.  
  
## <a name="return-types"></a>Rückgabetypen  
**int**  
 
## <a name="remarks"></a>Bemerkungen  
`DIFFERENCE` vergleicht zwei verschiedene `SOUNDEX`-Werte und gibt einen ganzzahligen Wert zurück. Dieser Wert misst das Grad der Übereinstimmung der `SOUNDEX`-Werte auf einer Skala von 0 (null) bis 4. Ein Wert von 0 (null) gibt eine schwache oder fehlende Ähnlichkeit der SOUNDEX-Werte an. Ein Wert von 4 gibt eine starke Ähnlichkeit, wenn nicht sogar eine vollständige Übereinstimmung der SOUNDEX-Werte an.  
  
`DIFFERENCE` und `SOUNDEX` verfügen über Sortierungsempfindlichkeit.  
  
## <a name="examples"></a>Beispiele  
Im ersten Teil des folgenden Beispiels werden die `SOUNDEX`-Werte von zwei sehr ähnlichen Zeichenfolgen verglichen. Für eine Latin1_General-Sortierung gibt `DIFFERENCE` einen Wert von `4` zurück. Im zweiten Teil dieses Beispiels werden die `SOUNDEX`-Werte von zwei sehr unterschiedlichen Zeichenfolgen verglichen, wobei `DIFFERENCE` für eine Latin1_General-Sortierung den Wert `0` zurückgibt.  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

