---
title: srv_willconvert (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_willconvert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0af2ec4471dc24af0fdb02576adad312ed35069f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740700"
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert (API für erweiterte gespeicherte Prozeduren)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Bestimmt, ob eine bestimmte Datentypkonvertierung innerhalb der ODS-Bibliothek verfügbar ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
  
```  
  
## <a name="arguments"></a>Argumente  
 *srctype*  
 Gibt den Datentyp der zu konvertierenden Daten an. Dieser Parameter kann ein beliebiger in der API für erweiterte gespeicherte Prozeduren verfügbarer Datentyp sein.  
  
 *desttype*  
 Gibt den Datentyp an, in den die Quelldaten konvertiert werden. Dieser Parameter kann ein beliebiger in der API für erweiterte gespeicherte Prozeduren verfügbarer Datentyp sein.  
  
## <a name="returns"></a>Rückgabewert  
 TRUE, wenn die Datentypkonvertierung unterstützt wird; FALSE, wenn die Datentypkonvertierung nicht unterstützt wird.  
  
## <a name="remarks"></a>Hinweise  
 Eine Beschreibung der einzelnen Datentypen finden Sie in [Data Types (Extended Stored Procedure API) (Datentypen (API für erweiterte gespeicherte Prozeduren))](data-types-extended-stored-procedure-api.md).  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Siehe auch  
 [srv_convert (API für erweiterte gespeicherte Prozeduren)](srv-convert-extended-stored-procedure-api.md)  
  
  
