---
title: Status-Eigenschaft (ADO Recordset) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d91c3e92be7679ad6fbbb4a4ee7bd1bb6a48422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916840"
---
# <a name="status-property-ado-recordset"></a>Status-Eigenschaft (ADO-Recordset)
Gibt den Status des aktuellen Datensatzes in Bezug auf die Batch-Updates oder andere Massenvorgänge an.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt die Summe aus einem oder mehreren zurück [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) Werte.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Status** Eigenschaft, um anzuzeigen, welche Änderungen ausstehen für Datensätze, die während des BatchUpdates geändert. Können Sie auch die **Status** Eigenschaft, um den Status der Datensätze anzeigen, bei denen bei Massenvorgängen, z. B. beim Aufruf der [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), oder [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) Methoden für eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt, oder legen Sie die [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft für eine **Recordset** Objekt in ein Array von Lesezeichen. Mit dieser Eigenschaft können Sie bestimmen, wie ein bestimmter Datensatz Fehler und lösen Sie ihn entsprechend.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Status-Eigenschaft – Beispiel (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status-Eigenschaft – Beispiel (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
