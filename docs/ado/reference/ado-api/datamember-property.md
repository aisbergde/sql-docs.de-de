---
title: DataMember-Eigenschaft | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 623f9b1f1e8873ddc4819bb8500c11edf09f5f76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919222"
---
# <a name="datamember-property"></a>DataMember-Eigenschaft
Gibt den Namen des Datenmembers, die aus abgerufen werden, wird die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) verwiesen wird, indem die [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) Eigenschaft.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert. Der Name ist nicht in der Groß-/Kleinschreibung beachtet.  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft wird verwendet, um datengebundene Steuerelemente mit der Data-Umgebung zu erstellen. Die Data-Umgebung verwaltet, Auflistungen von Daten (Datenquellen), enthält benannte Objekte (Datenmember), die als dargestellt werden ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
 Die **DataMember** und **DataSource** Eigenschaften müssen gemeinsam verwendet werden.  
  
 Die **DataMember** Eigenschaft bestimmt, welches Objekt vom angegebenen die **DataSource** Eigenschaft als dargestellt wird ein **Recordset** Objekt. Die **Recordset** Objekt muss geschlossen werden, bevor diese Eigenschaft festgelegt wird. Ein Fehler wird generiert, wenn die **DataMember** Eigenschaft nicht festgelegt ist, bevor die **DataSource** -Eigenschaft, oder, wenn die **DataMember** Name wurde nicht erkannt, von dem im angegebenen Objekt der **DataSource** Eigenschaft.  
  
## <a name="usage"></a>Verwendung  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataSource-Eigenschaft (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
