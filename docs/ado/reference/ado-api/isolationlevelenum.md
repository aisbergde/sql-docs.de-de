---
title: IsolationLevelEnum | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15ae2aac2851c496b6cac9e47d37fe5fa26b8e34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918377"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Gibt die Ebene der Isolation jeder Transaktion für eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
|Konstante|Wert|Beschreibung|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|Gibt an, dass der Anbieter eine andere Isolationsstufe als angegeben verwendet, aber die Ebene nicht bestimmt werden kann.|  
|**adXactChaos**|16|Gibt an, dass die ausstehenden Änderungen von stärker isolierten Transaktionen nicht überschrieben werden kann.|  
|**adXactBrowse**|256|Gibt an, dass eine Transaktion Sie nicht gespeicherte Änderungen in anderen Transaktionen anzeigen können.|  
|**adXactReadUncommitted**|256|Identisch mit **AdXactBrowse**.|  
|**adXactCursorStability**|4096|Gibt an, von einer Transaktion aus Änderungen in anderen Transaktionen sehen nur, nachdem sie ein Commit ausgeführt wurde.|  
|**adXactReadCommitted**|4096|Identisch mit **AdXactCursorStability**.|  
|**adXactRepeatableRead**|65536|Gibt an, dass Sie nicht von einer Transaktion aus in anderen Transaktionen vorgenommene Änderungen sehen, Erneutes Abfragen kann jedoch auch Abrufen neuer **Recordset** Objekte.|  
|**adXactIsolated**|1048576|Gibt an, dass Transaktionen isoliert von anderen Transaktionen durchgeführte.|  
|**adXactSerializable**|1048576|Identisch mit **AdXactIsolated**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-äquivalent  
 Package: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>Gilt für  
 [IsolationLevel-Eigenschaft](../../../ado/reference/ado-api/isolationlevel-property.md)
