---
title: Umgekehrter Schrägstrich (Zeilenfortsetzung) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- escape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 54e1dcd9735610f7cc8f109f00aa56fa7728ce04
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495441"
---
# <a name="backslash-line-continuation-transact-sql"></a>Umgekehrter Schrägstrich (Zeilenfortsetzung) (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

`\` teilt eine lange Zeichenfolgen- oder Binärzeichenfolgenkonstante in mindestens zwei Zeilen auf, um die Lesbarkeit zu erhöhen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>Argumente  
 \<erster Abschnitt der Zeichenfolge>  
 Ist der Anfang einer Zeichenfolge.  
  
 \<fortgesetzter Abschnitt der Zeichenfolge>  
 Ist die Fortsetzung einer Zeichenfolge.  
  
## <a name="remarks"></a>Bemerkungen  
Dieser Befehl gibt den ersten und den fortgesetzten Abschnitt der Zeichenfolge ohne den umgekehrten Schrägstrich als eine einzige Zeichenfolge zurück. Die neue Zeile nach dem umgekehrten Schrägstrich muss entweder ein Zeilenvorschubzeichen (U+000A) oder eine Kombination aus Wagenrücklaufzeichen (U+000D) und Zeilenvorschub (U+000A) in dieser Reihenfolge sein. 

## <a name="examples"></a>Beispiele  

### <a name="a-splitting-a-character-string"></a>A. Teilen einer Zeichenfolge  

Im folgenden Beispiel werden ein umgekehrter Schrägstrich und ein Wagenrücklauf verwendet, um eine Zeichenfolge in zwei Zeilen zu teilen.  
  
```  
SELECT 'abc\  
def' AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    

### <a name="b-splitting-a-binary-string"></a>B. Teilen einer Binärzeichenfolge  

Im folgenden Beispiel werden ein umgekehrter Schrägstrich und ein Wagenrücklauf verwendet, um eine Binärzeichenfolge in zwei Zeilen zu teilen.  

```  
SELECT 0xabc\
def AS [ColumnResult];  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 0xABCDEF
 ```    

## <a name="see-also"></a>Weitere Informationen  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40;Division&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40;Division Assignment&#41; &#40;Transact-SQL&#41; ((Divisionszuweisung) (Transact-SQL))](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Compound Operators &#40;Transact-SQL&#41; (Verbundoperatoren (Transact-SQL))](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  
