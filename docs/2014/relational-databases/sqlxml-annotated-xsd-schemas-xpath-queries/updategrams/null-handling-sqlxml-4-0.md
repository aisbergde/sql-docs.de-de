---
title: NULL (SQLXML 4.0) behandeln | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f7ca96ca65ae23202b84030140e0eaef945de2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014691"
---
# <a name="null-handling-sqlxml-40"></a>Behandlung von NULL (SQLXML 4.0)
  XML-Syntax deutet NULL als eine Abwesenheit. (Z. B. wenn ein Attribut- oder Elementwert Wert NULL ist, das Attribut bzw. Element nicht vorhanden ist aus dem XML-Dokument.) In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, die `updg:nullvalue` Attribut ermöglicht die Angabe von NULL für ein Element oder Attribut-Wert.  
  
 Z. B. das folgende Updategram stellt sicher, dass die **Titel** -Wert eines Kontakts mit **ContactID** von 64 NULL ist, und aktualisiert dann die **Titel** Wert auf "Mr." auf "Mr.".  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Wenn Parameter an ein Updategram übergeben werden, kann NULL als Parameterwert übergeben werden. Dies wird erreicht, indem das `nullvalue`-Attribut im `<updg:header>`-Block angegeben wird. Ein Beispiel finden Sie unter [übergeben von Parametern an Updategrams &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategramms &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
