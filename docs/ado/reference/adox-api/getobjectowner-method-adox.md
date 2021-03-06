---
title: GetObjectOwner-Methode (ADOX) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff85491cf7ca30e3f95526aa7043f321a65cccc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966276"
---
# <a name="getobjectowner-method-adox"></a>GetObjectOwner-Methode (ADOX)
Gibt zurück, den Besitzer eines Objekts in eine [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Zeichenfolge** Wert, der angibt der [Namen](../../../ado/reference/adox-api/name-property-adox.md) von der [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) oder [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) , die das Objekt besitzt.  
  
#### <a name="parameters"></a>Parameter  
 *ObjectName*  
 Ein **Zeichenfolge** Wert, der angibt, den Namen des Objekts, für das den Besitzer zurückgegeben.  
  
 *ObjectType*  
 Ein **lange** Wert möglich von der [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) Konstanten, der angibt, den Typ des Objekts, für das den Besitzer abgerufen.  
  
 *ObjectTypeId*  
 Optional. Ein **Variant** Wert, der angibt, die GUID für eine Anbieterobjekttyp nicht durch OLE DB-Spezifikation definiert. Dieser Parameter ist erforderlich, wenn *ObjectType* nastaven NA hodnotu **AdPermObjProviderSpecific**ist, andernfalls wird er nicht verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Anbieter, zurückgegebene Objektbesitzer nicht unterstützt wird, tritt ein Fehler auf.  
  
## <a name="applies-to"></a>Gilt für  
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [GetObjectOwner- und SetObjectOwner-Methoden – Beispiel (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [SetObjectOwner-Methode](../../../ado/reference/adox-api/setobjectowner-method.md)
