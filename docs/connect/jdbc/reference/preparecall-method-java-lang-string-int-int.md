---
title: prepareCall-Methode (java.lang.String, int, int) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7b51cbe470169459469959448208b3aa53b18cce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976257"
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall-Methode (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Erstellt ein [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)-Objekt, mit dem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekte mit dem angegebenen Typ und der Parallelität generiert werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sql*  
  
 Eine **Zeichenfolge**, die eine SQL-Anweisung enthält.  
  
 *resultSetType*  
  
 Ein Wert vom Typ **int** zur Angabe des Resultsettyps.  
  
 *resultSetConcurrency*  
  
 Ein Wert vom Typ **int** zur Angabe des Parallelitätstyps des Resultsets.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein CallableStatement-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Bemerkungen  
 Diese prepareCall-Methode wird von der prepareCall-Methode in der Java. SQL. Connection-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Weitere Informationen  
 [prepareCall-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
