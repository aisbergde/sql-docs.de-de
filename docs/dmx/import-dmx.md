---
title: Importieren (DMX) | Microsoft-Dokumentation
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2141a4f8ccc6e34ec3010ad3ce8e8e3789d09132
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892752"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Lädt ein Miningmodell oder eine Miningstruktur aus einer ABF-Datei (Analysis Services Backup File) auf den Server.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumente  
 *Einfügen*  
 Eine Zeichenfolge, die den Namen und den Speicherort der Datei angibt, die importiert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Objekte angegeben sind, wird der gesamte Inhalt der DMB-Datei geladen. Wenn die DMB-Datei eine Datenbank enthält, die auf dem Server nicht vorhanden ist, wird die Datenbank erstellt.  
  
 Sie müssen Datenbank- oder Serveradministrator sein, damit Sie Objekte exportieren bzw. importieren können.  
  
## <a name="import-from-file-example"></a>Beispiel für das Importieren aus einer Datei  
 Im folgenden Beispiel wird der gesamte Inhalt der Datei, die das Zuordnungsmodell und die Struktur enthält, auf den aktuellen Server importiert.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining- &#40;Erweiterungen DMX&#41; -Daten Definitions Anweisungen](../dmx/dmx-statements-data-definition.md)   
 [Data Mining- &#40;Erweiterungen DMX&#41; -Daten Bearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#41; - &#40;Anweisungs Referenz für Data Mining-Erweiterungen](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORT &#40;DMX&#41;](../dmx/export-dmx.md)   
 [Exportieren und Importieren von Data Mining-Objekten](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
